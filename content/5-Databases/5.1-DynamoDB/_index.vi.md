---
title: "Khởi tạo DynamoDB"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 5.1 </b> "
---
#### Khởi tạo DynamoDB
1. Nhập **DynamoDB** ở thanh tìm kiếm service trên AWS Console sau đó chọn **DynamoDB**.

![VPC](/images/5-Databases/dy/img-68.png)
2. Chọn **Create table**

![VPC](/images/5-Databases/dy/create.png)

3. **Table name**, điền `Data-Kinesis`.**Partition key** điền `timestamp`. Còn lại để mặc định.

![VPC](/images/5-Databases/dy/img-67.png)

4. Chọn **Create table**

![VPC](/images/5-Databases/dy/img-66.png)

5. Đợi khoảng 2 phút đến khi trạng thái chuyển thành **Active** là hoàn thành.

![VPC](/images/5-Databases/dy/img-65.png)


