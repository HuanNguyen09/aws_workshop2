---
title: "Tạo Lambda 2"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 6.3 </b> "
---

#### Các bước thực hiện chi tiết:



1. Tương tự như tạo lambda 1, chúng ta truy cập vào trang dịch vụ **Lambda** và chọn **Create function**.

    **Function name** điền `DynamoDBToS3`. **Runtime** chọn **Python 3.9**. Tích chọn **Use an existing role** sau đó chọn role vừa khởi tạo ở phần trước **RoleLab2**. Cuối cùng, chọn **Create function**.

![0](/images/6-Lambda/2/img-23.png)

2. Sao chép và dán đoạn mã sau. Sau đó nhấn **Debloy**.

```
import boto3
import json
from datetime import datetime, timedelta, timezone

# Initialize DynamoDB and S3 clients
dynamodb = boto3.client('dynamodb')
s3_client = boto3.client('s3')

def get_data_from_dynamodb(start_time, end_time):
    # Retrieve all data from DynamoDB
    response = dynamodb.scan(
        TableName='Data-Kinesis'
    )
    
    # Filter data within the specified time range
    filtered_data = []
    for item in response['Items']:
        timestamp = item['timestamp']['S']
        count = item['count']['N']
        route = item['route']['S']
        
        if start_time <= timestamp <= end_time:
            filtered_data.append({
                "timestamp": timestamp,
                "count": int(count),
                "route": route
            })
    
    return filtered_data

def upload_json_to_s3(data):
    # Save data to a JSON file in memory
    json_data = json.dumps(data)
    
    # Upload the JSON file to Amazon S3
    s3_client.put_object(
        Bucket='webanalytics-huannguyen',
        Key='data.json',  # Path and filename on S3
        Body=json_data.encode('utf-8')
    )

def lambda_handler(event, context):
    # Get current time and the time one hour ago in Vietnamese timezone (GMT+7)
    vn_timezone = timezone(timedelta(hours=7))
    end_time = (datetime.now(vn_timezone)).strftime('%Y-%m-%d %H:%M:%S')
    start_time = (datetime.now(vn_timezone) - timedelta(hours=1)).strftime('%Y-%m-%d %H:%M:%S')

    # Get data from DynamoDB
    data = get_data_from_dynamodb(start_time, end_time)

    # Upload JSON data to Amazon S3
    upload_json_to_s3(data)

    return {
        'statusCode': 200,
        'body': json.dumps('Data updated and uploaded to S3 successfully.')
    }

```
{{% notice note %}}
Ghi chú: Đoạn mã trên thực hiện lấy dự liệu trước thời điểm hiện tại 1 giờ từ **DynamoDB** và lưu thành file **data.json** trong **bucket S3**
{{% /notice %}}

![0](/images/6-Lambda/2/img-22.png)

3. Kéo xuống cuối trang, chọn **Add a layer**. Chọn **Specify an ARN**. Điền `arn:aws:lambda:ap-southeast-1:770693421928:layer:Klayers-p39-boto3:18`. Sau đó nhần **Verify** và **Add**.

![0](/images/6-Lambda/2/img-21.png)

4. Chọn **Add trigger**.

![0](/images/6-Lambda/2/img-20.png)

5. Chọn **DynamoDB**, sau đó chọn **DynamoDB table** ta đã tạo trước đó. **Starting position** chúng ta chọn **Latest**. Tiếp theo, chọn **Add**.



![0](/images/6-Lambda/2/img-19.png)

6. Đợi khoảng 1 phút, khi trạng thái chuyển thành **Enabled**.

![0](/images/6-Lambda/2/img-18.png)

