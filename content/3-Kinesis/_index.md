---
title: "Initializing Kinesis"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

In this section, we will proceed to initialize a data stream in Amazon Kinesis, laying the foundation for real-time data collection and processing from various sources.

#### Implementation Steps:
1. Enter **Kinesis** in the service search bar on the AWS Console, then select **Kinesis**.
   ![0](/images/3-Kinesis/img-77.png)

2. Choose **Create data stream**.
   ![0](/images/3-Kinesis/img-76.png)

3. In the **Data stream name** section, enter `KinesisDataStream`. Then select **Provisioned** and input **1**. Finally, choose **Create data stream**.
   ![0](/images/3-Kinesis/img-75.png)

4. Wait for about 2 minutes, and when the status changes to **Active**, the setup is complete.
   ![0](/images/3-Kinesis/img-74.png)
