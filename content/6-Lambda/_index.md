---
title: "Initializing Lambda Functions"
date: "`r Sys.Date()`"
weight: 6
chapter: false
pre: " <b> 6. </b> "
---

In this section, we will perform three important steps to build a real-time data flow:

1. **Initialize Roles for Lambda Functions:**
   First, we will create a specialized role for the Lambda Functions. This role will provide the necessary permissions for Lambda to safely and securely interact with other services such as Kinesis, DynamoDB, and S3.

2. **Configure Lambda 1: Sending Data from Kinesis to DynamoDB:**
   Next, we will configure the first Lambda Function. This Lambda will be responsible for taking data from the Kinesis stream we created earlier and storing it in DynamoDB. This process will handle and standardize the data for easier querying and analysis later.

3. **Configure Lambda 2: Sending Data from DynamoDB to S3 and Storing as JSON:**
   Finally, we will configure the second Lambda Function. This Lambda will retrieve the processed data stored in DynamoDB and send it to Amazon S3. The data will be stored as JSON files in S3, providing a foundation for data visualization and analysis.

These three steps together create a complete workflow from real-time data collection to storage and visualization.

### Contents

- [Creating Roles](6.1-role/)
- [Creating Lambda 1](6.2-lambda1/)
- [Creating Lambda 2](6.3-lambda2/)
