---
title: "Introduction"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1. </b> "
---

The **RealTime Data Pipeline** utilizes **AWS Kinesis, AWS Lambda, Amazon DynamoDB, Amazon S3 (Simple Storage Service)**.

**Objectives and Value:**
The "Real-time Data Pipeline" project is designed to collect, process, and visualize data from vehicles moving on the road. The project aims to create a flexible, reliable, and scalable system capable of analyzing real-time data, thereby providing significant value to traffic management, road data analysis, and traffic condition forecasting.

**Deployment Plan:**
The project will be deployed in multiple stages, starting with generating simulated data using Visual Studio Code. Once the data is generated, it will be sent to the Amazon Kinesis stream for collection. Lambda functions will process the data and store it in Amazon DynamoDB. The final processed data will be stored on Amazon S3 and visualized through a web page.

#### The diagram below illustrates the architecture of the data pipeline:

![0](/images/demo4.png)

### Table of Contents

1. [Introduction](1-introduce/)
2. [Creating Access Keys](2-AccessKeys/)
3. [Initializing Kinesis](3-Kinesis/)
4. [Generating Simulated Data](4-IDE/)
5. [Creating Databases](5-Databases/)
6. [Creating Lambda Functions](6-Lambda/)
7. [Testing](7-test/)
8. [Resource Cleanup](8-terminate/)
