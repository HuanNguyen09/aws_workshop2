---
title: "Khởi tạo các lambda function"
date: "`r Sys.Date()`"
weight: 6
chapter: false
pre: " <b> 6. </b> "
---
Trong phần này, chúng ta sẽ tiến hành ba bước quan trọng để xây dựng dòng chảy dữ liệu thời gian thực:

1. **Khởi tạo Vai Trò (Role) cho Lambda Function:**
   Trước hết, chúng ta sẽ khởi tạo một vai trò (role) đặc biệt cho các Lambda Function. Vai trò này sẽ cung cấp các quyền cần thiết để Lambda có thể tương tác với các dịch vụ khác như Kinesis, DynamoDB và S3 một cách an toàn và bảo mật.

2. **Cấu hình Lambda 1: Gửi Dữ Liệu từ Kinesis đến DynamoDB:**
   Bước tiếp theo, chúng ta sẽ cấu hình Lambda Function đầu tiên. Lambda này sẽ thực hiện nhiệm vụ đưa dữ liệu từ luồng Kinesis mà chúng ta đã tạo trước đó và lưu trữ vào DynamoDB. Quá trình này sẽ xử lý và chuẩn hóa dữ liệu để tiện cho việc truy vấn và phân tích sau này.

3. **Cấu hình Lambda 2: Gửi Dữ Liệu từ DynamoDB đến S3 và Lưu Dưới Dạng JSON:**
   Cuối cùng, chúng ta sẽ cấu hình Lambda Function thứ hai. Lambda này sẽ lấy dữ liệu đã được xử lý và lưu trữ trong DynamoDB và gửi chúng đến Amazon S3. Dữ liệu sẽ được lưu dưới dạng các tệp tin JSON trong S3, tạo nền tảng cho việc trực quan hóa và phân tích dữ liệu.

Ba bước trên cùng nhau tạo nên một quy trình hoàn chỉnh từ việc thu thập dữ liệu thời gian thực tới lưu trữ và trực quan hóa.
### Nội dung

- [Tạo Role](6.1-role/)
- [Tạo Lambda 1](6.2-lambda1/)
- [Tạo Lambda 2](6.3-lambda2/)

