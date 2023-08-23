---
title: "Khởi tạo các databases"
date: "`r Sys.Date()`"
weight: 5
chapter: false
pre: " <b> 5. </b> "
---


Trong workshop này, chúng ta sẽ tận dụng hai dịch vụ lưu trữ quan trọng từ Amazon Web Services (AWS): **Amazon DynamoDB** và **Amazon S3**.

**DynamoDB** dùng để lưu trữ dữ liệu đã qua xử lý từ Amazon Kinesis. Nó là một cơ sở dữ liệu NoSQL có khả năng mở rộng, cho phép lưu trữ và truy vấn dữ liệu một cách hiệu quả, đồng thời hỗ trợ quản lý dữ liệu phức tạp và phân tích dữ liệu trong thời gian thực.

![0](/images/5-Databases/download1.png)

**S3** dùng để lưu trữ dữ liệu đã qua xử lý và trực quan hóa từ dự án. Amazon S3 là dịch vụ lưu trữ đám mây với khả năng mở rộng, cho phép lưu trữ các loại dữ liệu như tệp tin, hình ảnh, video và dữ liệu cấu trúc. Dữ liệu này có thể được truy cập và chia sẻ dễ dàng thông qua các liên kết và tích hợp với các dịch vụ và ứng dụng khác trên nền tảng AWS.

![0](/images/5-Databases/download.png)
