---
title: "Creating Lambda 1"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 6.2 </b> "
---

#### Setting Up Lambda Function 1

In this step, we will set up the first Lambda function that will be responsible for processing data from the Kinesis stream and storing it in DynamoDB.

##### Detailed Steps:

1. Navigate to the **Lambda** service in the AWS Console.

   ![Navigate to Lambda](/images/6-Lambda/1/img-55.png)

2. Click **Create function**.

   ![Create function](/images/6-Lambda/1/img-54.png)

3. Configure the function as follows:
   - **Function name**: Enter `KinesisToDynamoDB`.
   - **Runtime**: Choose **Python 3.9**.
   - **Use an existing role**: Select the role you created earlier (e.g., `LambdaRolesWorkshop`).
   - Click **Create function**.

   ![Function configuration](/images/6-Lambda/1/img-53.png)

4. Copy and paste the following code into the editor. Then click **Deploy**.
   
   ```python
   import boto3
   import binascii
   import json

   dynamodb = boto3.resource('dynamodb')
   table_name = 'Data-Kinesis'  # Replace with your DynamoDB table name
   table = dynamodb.Table(table_name)

   def lambda_handler(event, context):
       print(event)
       for record in event['Records']:
           payload = binascii.a2b_base64(record['kinesis']['data'])
           data = json.loads(payload)

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
   
   ![Code editor](/images/6-Lambda/1/img-52.png)

5. Scroll down to the **Add a layer** section.

   ![Add a layer](/images/6-Lambda/1/img-51.png)

6. Choose **Specify an ARN**, and enter `arn:aws:lambda:ap-southeast-1:770693421928:layer:Klayers-p39-boto3:18`. Then click **Verify** and **Add**.

   ![Specify ARN](/images/6-Lambda/1/img-50.png)

7. Click **Add trigger**.

   ![Add trigger](/images/6-Lambda/1/img-49.png)

8. Select **Kinesis** as the trigger type. Choose the Kinesis stream you created earlier. Set **Starting position** to **Trim horizon**. Then click **Add**.

   ![Configure Kinesis trigger](/images/6-Lambda/1/img-47.png)

9. Wait for a minute until the trigger status becomes **Enabled**.

   ![Enabled trigger](/images/6-Lambda/1/img-46.png)

##### Testing Lambda Function 1

1. Open Visual Studio Code and run the **createData.py** script you created earlier.

   ![Run createData.py](/images/6-Lambda/1/img-45.png)

2. Go back to the Lambda function page, navigate to the **Monitor** tab, and click on **View CloudWatch logs**.

   ![Monitor tab](/images/6-Lambda/1/img-44.png)

3. In the new window, select the latest log stream. If the logs are not yet visible, wait a minute and click **Reload**.

   ![Log stream](/images/6-Lambda/1/img-43.png)

4. You should see that there are no error messages.

   ![No errors](/images/6-Lambda/1/img-42.png)

5. Access the DynamoDB table (`Data-Kinesis`) you created earlier. Click **Explore table items**.

   ![Explore table items](/images/6-Lambda/1/img-41.png)

6. You can see that the data sent from Visual Studio Code has been successfully stored in the table.

   ![Stored data](/images/6-Lambda/1/img-39.png)

Now you have successfully set up Lambda function 1 to process data from the Kinesis stream and store it in DynamoDB.
