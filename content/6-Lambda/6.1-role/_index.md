---
title: "Creating a Role"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 6.1 </b> "
---

#### Creating a Role in IAM

1. To begin, let's create a role in **IAM**. Enter **IAM** in the service search bar on the AWS Console and select **IAM**.

![IAM Service Search](/images/6-Lambda/role/img-64.png)

2. In the left navigation pane, choose **Roles**, then select **Create role**.

![Create Role](/images/6-Lambda/role/img-63.png)

3. Choose **AWS service** and **Lambda**. Then, click **Next**.

![Choose AWS Service](/images/6-Lambda/role/img-62.png)

4. Search for the following keywords and select the corresponding policies:
    - `CloudWatch`: **CloudWatchFullAccess**
    - `S3`: **AmazonS3FullAccess**
    - `DynamoDB`: **AmazonDynamoDBFullAccess**
    - `Kinesis`: **AmazonKinesisFullAccess**
    
{{% notice warning %}}
Note: In the context of this lab, for simplicity and convenience, we are using a single role for both Lambda Functions and granting **FullAccess** permissions to all services. However, in a real-world scenario, you should configure roles with specific policies to ensure security and proper access control.

In actual deployments, breaking down roles and setting up specific policies will help limit access rights based on tasks and security risks. This helps protect your resources from unauthorized access and potential security vulnerabilities.
{{% /notice %}}

![Select Policies](/images/6-Lambda/role/img-61.png)

![Attach Policies](/images/6-Lambda/role/img-60.png)

![Policies Added](/images/6-Lambda/role/img-59.png)

Once all policies are added, click **Next**.

![Review](/images/6-Lambda/role/img-58.png)

5. Enter the **Role name** as `RoleLab2`.

![Role Name](/images/6-Lambda/role/img-57.png)

6. Review the settings and choose **Create role**.

![Create Role](/images/6-Lambda/role/img-56.png)
