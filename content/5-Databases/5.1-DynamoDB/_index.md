---
title: "Initializing DynamoDB"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 5.1 </b> "
---

#### Initializing DynamoDB

1. Enter **DynamoDB** in the service search bar on the AWS Console, then select **DynamoDB**.

   ![VPC](/images/5-Databases/dy/img-68.png)

2. Choose **Create table**.

   ![VPC](/images/5-Databases/dy/create.png)

3. In the **Table name** field, enter `Data-Kinesis`. For the **Partition key**, enter `timestamp`. Leave the rest as default.

   ![VPC](/images/5-Databases/dy/img-67.png)

4. Select **Create table**.

   ![VPC](/images/5-Databases/dy/img-66.png)

5. Wait for about 2 minutes until the status changes to **Active**, indicating completion.

   ![VPC](/images/5-Databases/dy/img-65.png)
