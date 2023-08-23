---
title: "Serverless Application"
date: "`r Sys.Date()`"
weight: 1
chapter: false
---

# Triển khai đường ống dữ liệu theo thời gian thực

### Tổng quan

Trong bài workshop này, chúng ta sử dụng một số dịch vụ quan trọng của Amazon Web Services (AWS) để tạo nên một hệ thống thu thập, xử lý và trực quan hóa dữ liệu giao thông thời gian thực. Dưới đây là một giới thiệu về các dịch vụ được sử dụng trong dự án và khái niệm cũng như công dụng của mỗi dịch vụ:

1. **Amazon Kinesis**:
   - **Khái Niệm**: Amazon Kinesis là một dịch vụ thu thập, xử lý và truyền dữ liệu thời gian thực.
   - **Công Dụng**: Trong dự án, Amazon Kinesis được sử dụng để nhận và thu thập dữ liệu từ các phương tiện đang di chuyển trên tuyến đường. Nó cho phép chúng ta xử lý dữ liệu thời gian thực và định dạng chuẩn hóa trước khi chuyển tiếp vào các bước xử lý tiếp theo.

2. **AWS Lambda**:
   - **Khái Niệm**: AWS Lambda là một dịch vụ tính toán "serverless" cho phép bạn thực hiện mã nguồn mà không cần phải quản lý máy chủ.
   - **Công Dụng**: Trong đường ống dữ liệu, AWS Lambda được sử dụng để xử lý dữ liệu thu thập từ Kinesis. Mỗi lần dữ liệu được gửi đến, Lambda có thể thực hiện các xử lý như tính toán thống kê, chuyển đổi định dạng, lọc dữ liệu, hoặc thực hiện các phân tích phức tạp.

3. **Amazon DynamoDB**:
   - **Khái Niệm**: Amazon DynamoDB là một dịch vụ cơ sở dữ liệu NoSQL có khả năng mở rộng, sử dụng kiểu lưu trữ khóa và giá trị.
   - **Công Dụng**: Dữ liệu sau khi đã qua xử lý bởi Lambda được lưu trữ vào Amazon DynamoDB. DynamoDB cung cấp tính năng lưu trữ hiệu suất cao và có khả năng mở rộng, phù hợp cho việc lưu trữ và truy vấn dữ liệu giao thông thời gian thực.

4. **Amazon S3 (Simple Storage Service)**:
   - **Khái Niệm**: Amazon S3 là dịch vụ lưu trữ đám mây với khả năng mở rộng và tin cậy.
   - **Công Dụng**: Dữ liệu đã qua xử lý hoàn toàn sẽ được lưu trữ vào Amazon S3. Dịch vụ này cho phép chúng ta lưu trữ dữ liệu trực quan hoá, như biểu đồ, đồ thị và bản đồ tương tác, để người dùng có thể truy cập và tìm hiểu dữ liệu một cách dễ dàng.

Bằng cách kết hợp các dịch vụ trên, dự án "Đường Ống Dữ liệu Thời Gian Thực" tạo nên một hệ thống hoàn chỉnh từ việc thu thập dữ liệu thời gian thực tới xử lý và trực quan hóa.việc và thời gian triển khai quy trình ETL.

![0](/images/demo4.png)





