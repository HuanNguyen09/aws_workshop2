---
title: "Tạo Lambda 1"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 6.2 </b> "
---

#### Các bước thực hiện chi tiết:


1. Nhập **Lambda** ở thanh tìm kiếm service trên AWS Console sau đó chọn **Lambda**.

![0](/images/6-Lambda/1/img-55.png)

2. Chọn **Create function**.
![0](/images/6-Lambda/1/img-54.png)

3. **Function name** điền `KinesisToDynamoDB`. **Runtime** chọn **Python 3.9**. Tích chọn **Use an existing role** sau đó chọn role vừa khởi tạo ở phần trước **RoleLab2**. Cuối cùng, chọn **Create function**.
![0](/images/6-Lambda/1/img-53.png)

4. Sao chép và dán đoạn mã sau. Sau đó nhấn **Debloy**.

```
import boto3
import binascii
import json

# Initialize DynamoDB resource
dynamodb = boto3.resource('dynamodb')
table_name = 'Data-Kinesis'  # Replace with your DynamoDB table name
table = dynamodb.Table(table_name)

def lambda_handler(event, context):
    print(event)
    for record in event['Records']:
        payload = binascii.a2b_base64(record['kinesis']['data'])
        data = json.loads(payload)
       
        # Store data in DynamoDB table
        response = table.put_item(
            Item={
                'timestamp': data['timestamp'],
                'route': data['route'],
                'count': data['count']
            }
        )      
            
        print(f"Stored data in DynamoDB: {response}")

    return {
        'statusCode': 200,
        'body': json.dumps('Data stored in DynamoDB')
    }

```

![0](/images/6-Lambda/1/img-52.png)

5. Kéo xuống cuối trang, chọn **Add a layer**.

![0](/images/6-Lambda/1/img-51.png)

6. Chọn **Specify an ARN**. Điền `arn:aws:lambda:ap-southeast-1:770693421928:layer:Klayers-p39-boto3:18`. Sau đó nhần **Verify** và **Add**.

![0](/images/6-Lambda/1/img-50.png)


7. Chọn **Add trigger**.

![0](/images/6-Lambda/1/img-49.png)

8. Chọn **Kinesis**, sau đó chọn **Kinesis stream** ta đã tạo trước đó. **Starting position** chúng ta chọn **Trim horizon**. Tiếp theo, chọn **Add**.


![0](/images/6-Lambda/1/img-47.png)

9. Đợi khoảng 1 phút, khi trạng thái chuyển thành **Enabled**.


![0](/images/6-Lambda/1/img-46.png)

##### Vậy là ta đã cấu hình xong Lambda1. Chúng ta sẽ tiến hành kiểm tra khả năng hoạt động của nó.

1. Mở Visual Studio Code, chạy file **createData.py** mà chúng ta đã tạo trước đó.
![0](/images/6-Lambda/1/img-45.png)

2. Truy cập lại vào trang lambda 1, tại tab **Monitor** chúng ta chọn **View CloudWatch logs**. 

![0](/images/6-Lambda/1/img-44.png)

3. Tại cửa sổ mới, chúng ta chọn log mới nhất. Nếu log chưa xuất hiện chúng ta đợi 1 phút và nhấn **reload**.

![0](/images/6-Lambda/1/img-43.png)

4. Chúng ta có thể thấy không có thông báo lỗi (Error) xuất hiện.

![0](/images/6-Lambda/1/img-42.png)

5. Chúng ta truy cập vào bảng DynamoDB **Data-Kinesis** đã tạo trước đó. Sau đó chọn **Explore table items**.

![0](/images/6-Lambda/1/img-41.png)

6. Chúng ta có thể thấy dữ liệu gửi từ **VS Code** đã được lưu về trong bảng.

![0](/images/6-Lambda/1/img-39.png)

