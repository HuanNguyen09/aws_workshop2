---
title: "Cleaning Up Resources"
date: "`r Sys.Date()`"
weight: 8
chapter: false
pre: " <b> 8. </b> "
---

#### Cleaning Up Resources

Before concluding this workshop, it's important to clean up the resources to avoid incurring unnecessary charges.

#### S3

1. Access **S3** and select the S3 bucket that was created during this lab. Then, choose **Empty**.

![Empty S3 Bucket](/images/8-terminate/img-15.png)

2. Enter `permanently delete` and choose **Empty**.

![Confirm Empty S3 Bucket](/images/8-terminate/img-14.png)

3. Select the S3 bucket and choose **Delete**.

![Delete S3 Bucket](/images/8-terminate/img-13.png)

4. Enter the bucket name `webanalytics-huannguyen` and choose **Delete bucket**.

![Confirm Delete S3 Bucket](/images/8-terminate/img-12.png)


#### Lambda

1. Access **Lambda** and select the Lambda functions that were created during this lab. Then, choose **Action** --> **Delete**.

![Delete Lambda Function](/images/8-terminate/img-11.png)

2. Enter `delete` and choose **Delete**.

![Confirm Delete Lambda Function](/images/8-terminate/img-10.png)

#### DynamoDB

1. Access **DynamoDB** and select the tables that were created during this lab. Then, choose **Delete**.

![Delete DynamoDB Table](/images/8-terminate/img-09.png)

2. Enter `confirm` and choose **Delete**.

![Confirm Delete DynamoDB Table](/images/8-terminate/img-08.png)

#### Kinesis

1. Access **Kinesis** and select the Data stream that was created during this lab. Then, choose **Action** --> **Delete**.

![Delete Kinesis Data Stream](/images/8-terminate/img-07.png)

2. Enter `delete` and choose **Delete**.

![Confirm Delete Kinesis Data Stream](/images/8-terminate/img-06.png)

#### Role

1. Access **IAM**, go to the **Role** tab, select the role that was created during this lab, and then choose **Delete**.

![Delete IAM Role](/images/8-terminate/img-05.png)

2. Enter the role name `RoleLab2` and choose **Delete**.

![Confirm Delete IAM Role](/images/8-terminate/img-04.png)

#### Access Keys

1. In the AWS Management Console, select your account name in the top right corner. Then choose **Security credentials**.

![Access Security Credentials](/images/8-terminate/img-03.png)

2. Select the Access Key that was created during this lab. Then, choose **Action** --> **Delete**.

![Delete Access Key](/images/8-terminate/img-02.png)

3. Choose **Deactivate**.

![Deactivate Access Key](/images/8-terminate/img-01.png)

4. Enter the **Access Key** name and choose **Delete**.

![Confirm Delete Access Key](/images/8-terminate/img-00.png)

By following these steps, you have successfully cleaned up all the resources used in this workshop. Thank you for your participation and attention.
