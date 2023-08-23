---
title: "Tạo Role"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 6.1 </b> "
---
#### Trước tiên, ta tạo role trong **AIM**
1. Nhập **AIM** ở thanh tìm kiếm service trên AWS Console sau đó chọn **AIM**.

![0](/images/6-Lambda/role/img-64.png)
2. Ở thanh điều hướng bên trái, chọn **Rules** Chọn **Create role**
![0](/images/6-Lambda/role/img-63.png)

3. Chọn **AWS service** và **Lambda**. Sau đó nhấn **Next**.
![0](/images/6-Lambda/role/img-62.png)

4. Lần lượt tìm kiếm với các từ khóa và tích chọn policy tương ứng:
    - `CloudWatch`: **CloudWatchFullAccess**
    - `S3` : **AmazonS3FullAccess**
    - `DynamoDB`: **AmazonDynamoDBFullAccess**
    - `Kinesis` : **AmazonKinesisFullAccess**
{{% notice warning %}}
Lưu ý: Trong môi trường của bài thực hành, để đơn giản và tiện lợi, chúng ta sẽ sử dụng một vai trò (role) cho cả hai Lambda Function và trao quyền **FullAccess** trên tất cả các dịch vụ. Tuy nhiên, khi triển khai vào sản phẩm thực tế, chúng ta cần cấu hình từng vai trò với các chính sách (policy) đủ để đảm bảo tính an toàn và bảo mật.

Trong tình huống thực tế, việc chia nhỏ vai trò và thiết lập các chính sách cụ thể sẽ giúp hạn chế quyền truy cập dựa trên nhiệm vụ và nguy cơ bảo mật. Điều này giúp bảo vệ tài nguyên của bạn khỏi truy cập trái phép và tiềm ẩn các rủi ro an ninh.
{{% /notice %}}


![0](/images/6-Lambda/role/img-61.png)


![0](/images/6-Lambda/role/img-60.png)

![0](/images/6-Lambda/role/img-59.png)

Sau khi thêm đủ policy, ta chọn **Next**.

![0](/images/6-Lambda/role/img-58.png)

5. **Role name** điền `RoleLab2`.

![0](/images/6-Lambda/role/img-57.png)

6. Kiểm tra lại và chọn **Create role**.

![0](/images/6-Lambda/role/img-56.png)



