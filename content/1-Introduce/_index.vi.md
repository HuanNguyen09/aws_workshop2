---
title: "Giới thiệu"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1. </b> "
---

**Đường ống dữ liệu thời gian thực (RealTime Data Pipeline)** sử dụng **AWS Kinesis, AWS Lambda, Amazon DynamoDB, Amazon S3 (Simple Storage Service)**. 

**Mục Tiêu và Giá Trị:**
Dự án "Đường Ống Dữ liệu Thời Gian Thực" đã được thiết kế để thu thập, xử lý và trực quan hóa dữ liệu từ các phương tiện di chuyển trên tuyến đường. Mục tiêu của dự án là tạo ra một hệ thống linh hoạt, đáng tin cậy và mở rộng có khả năng phân tích dữ liệu thời gian thực, từ đó mang lại giá trị quan trọng cho quản lý giao thông, phân tích dữ liệu đường xá và dự báo tình trạng giao thông.

**Kế Hoạch Triển Khai:**
Dự án sẽ được triển khai theo từng bước, bắt đầu từ tạo dữ liệu mô phỏng với Visual Studio Code. Sau khi dữ liệu được tạo, nó sẽ được gửi đến luồng Amazon Kinesis để thu thập. Các hàm Lambda sẽ xử lý dữ liệu và lưu trữ nó vào Amazon DynamoDB. Dữ liệu cuối cùng sau khi đã qua xử lý sẽ được lưu trữ trên Amazon S3 và hiển thị trực quan qua trang web.

#### Sơ đồ dưới đây minh họa kiến trúc đường ống dữ liệu:

![0](/images/demo4.png)

### Nội dung

1.  [Giới thiệu](1-introduce/)
2.  [Tạo accessKeys ](2-AccessKeys/)
3.  [Khởi tạo Kinesis](3-Kinesis/)
4.  [Tạo dữ liệu mô phỏng](4-IDE/)
5.  [Khởi tạo các databases](5-Databases/)
6.  [Khởi tạo các lambda function](6-Lambda/)
7.  [Kiểm tra](7-test/)
8.  [Dọn dẹp tài nguyên](8-terminate/)


