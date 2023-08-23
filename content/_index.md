---
title: "Serverless Application"
date: "`r Sys.Date()`"
weight: 1
chapter: false
---

# Real-time Data Pipeline Deployment

### Overview

In this workshop, we utilize several key services of Amazon Web Services (AWS) to build a system for real-time collection, processing, and visualization of traffic data. Below is an introduction to the services used in the project, along with the concepts and purposes of each service:

1. **Amazon Kinesis**:
   - **Concept**: Amazon Kinesis is a service for real-time data collection, processing, and streaming.
   - **Purpose**: In the project, Amazon Kinesis is used to receive and collect data from vehicles moving on the road. It enables us to process real-time data and normalize the format before forwarding it to subsequent processing steps.

2. **AWS Lambda**:
   - **Concept**: AWS Lambda is a serverless compute service that allows you to run code without managing servers.
   - **Purpose**: In the data pipeline, AWS Lambda is used to process data collected from Kinesis. Upon receiving data, Lambda can perform tasks such as statistical computation, format conversion, data filtering, or complex analytics.

3. **Amazon DynamoDB**:
   - **Concept**: Amazon DynamoDB is a scalable NoSQL database service that uses key-value storage.
   - **Purpose**: Data processed by Lambda is stored in Amazon DynamoDB. DynamoDB provides high-performance and scalable storage, suitable for storing and querying real-time traffic data.

4. **Amazon S3 (Simple Storage Service)**:
   - **Concept**: Amazon S3 is a cloud storage service known for its scalability and reliability.
   - **Purpose**: Processed data is fully stored in Amazon S3. This service allows us to store visualized data, such as charts, graphs, and interactive maps, for easy access and understanding by users.

By combining these services, the "Real-time Data Pipeline" project creates a complete system from real-time data collection to processing and visualization, as well as the deployment timeline of the ETL process.

![0](/images/demo4.png)
