---
title: "Tạo dữ liệu mô phỏng"
date: "`r Sys.Date()`"
weight: 4
chapter: false
pre: " <b> 4. </b> "
---

Trong workshop lần này, do chúng ta không có dữ liệu trực tiếp từ các cảm biến gửi về, nên chúng ta sẽ sử dụng Visual Studio Code để tạo dữ liệu mô phỏng về số lượng xe lưu thông trên bốn tuyến đường khác nhau: "Route A," "Route B," "Route C," và "Route D." Sau đó, chúng ta sẽ gửi dữ liệu này đến luồng dữ liệu Kinesis để tiếp tục quá trình xử lý và phân tích.

{{% notice note %}}
Ghi chú: Dữ liệu gửi đi dưới định dạng json như sau: **{
  "timestamp": "2023-08-15 19:22:02",
  "route": "Route B",
  "speed": 75
}**
{{% /notice %}}

### Các bước thực hiện: 

#### Phần 1- Gửi dữ liệu.
1. Mở **Visual Studio Code** và tạo file mới **createData.py**. Sau đó mở **Terminal** để thực hiện kết nối với AWS thông qua **Access Key** đã tạo từ phần trước.
    - Sử dụng lệnh 
``` 
aws configure
```
  
- Lần lượt điền **Access Key - Secret access key - region name - output format**
    - **Access Key - Secret access key**: lấy thông tin từ phần 2.
    - **region name**: region mà bạn đang làm workshop `ap-southeast-1`
    - **output format**: `json`

![0](/images/4-IDE/img-78.png)
2. Sao chép và dán đoạn mã sau vào file vừa tạo.
```
import random
import json
import boto3
import time
from datetime import datetime

# Create a connection to Kinesis Data Streams
client = boto3.client('kinesis', region_name='ap-southeast-1')
stream_name = 'demo'

# List of routes
routes = ["Route A", "Route B", "Route C", "Route D"]

# Function to generate simulated traffic events for all routes
def generate_traffic_event(route):
    count = random.randint(30, 100)  # Number of vehicles on the route, 30-100
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    event_data = {
        'timestamp': timestamp,
        'route': route,
        'count': count
    }
    return json.dumps(event_data)

# Send simulated data to the data stream for all routes
while True:
    for route in routes:
        event_data = generate_traffic_event(route)
        response = client.put_record(
            StreamName=stream_name,
            Data=bytes(event_data, 'utf-8'),
            PartitionKey='123'
        )
        print(f"Sent: {event_data}")
        time.sleep(1)
    time.sleep(30)

```


![0](/images/4-IDE/img-73.png)

3. Chọn biểu tượng hình tam giác ở góc trên bên phải (Run code) để thực thi. Sau đó, tại cửa sổ terminal chúng ta nhập được thông báo dữ liệu gửi đi.
![0](/images/4-IDE/img-71.png)

#### Phần 2 - Kiểm tra dữ liệu có gửi đến Kinesis:

1. Mở dịch vụ Kinesis. Chọn **Data Stream** chúng ta đã tạo trước đó.
![0](/images/4-IDE/img-70.png)

2. Tại tab **Data viewer**. **Shard** chọn **Shardld-00000000000**, **Starting position** chọn **Trim horizon**. Cuối cùng chọn **Get records**. 
![0](/images/4-IDE/img-69.png)

Tại đây, chúng ta thấy 4 dòng dữ liệu mà lúc nãy đã gửi đi. Vậy là Kinesis đã nhận được dữ liệu.

