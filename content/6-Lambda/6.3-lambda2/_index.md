---
title: "Creating Lambda 2"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 6.3 </b> "
---

#### Detailed Steps:


1. Similarly to creating Lambda 1, navigate to the **Lambda** service page and select **Create function**.

   Enter a **Function name** as `DynamoDBToS3`. Choose **Python 3.9** as the **Runtime**. Select **Use an existing role** and choose the role you created earlier, **RoleLab2**. Finally, click **Create function**.

![Create Function](/images/6-Lambda/2/img-23.png)

2. Copy and paste the following code into the editor. Then, click **Deploy**.

```python
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

Note: The above code fetches the project 1 hour before current time from **DynamoDB** and saves it to **data.json** in **S3 container**
{{% /notice %}}

![Add Layer](/images/6-Lambda/2/img-22.png)

3. Scroll down to the bottom of the page and select **Add a layer**. Choose **Specify an ARN** and enter `arn:aws:lambda:ap-southeast-1:770693421928:layer:Klayers-p39-boto3:18`. Then, click **Verify** and **Add**.

![Specify ARN](/images/6-Lambda/2/img-21.png)

4. Select **Add trigger**.

![Add Trigger](/images/6-Lambda/2/img-20.png)

5. Choose **DynamoDB** and then select the **DynamoDB table** you created earlier. Choose **Latest** as the **Starting position**. Finally, click **Add**.

![Add DynamoDB Trigger](/images/6-Lambda/2/img-19.png)

6. Wait for about a minute until the status changes to **Enabled**.

![Enabled Status](/images/6-Lambda/2/img-18.png)