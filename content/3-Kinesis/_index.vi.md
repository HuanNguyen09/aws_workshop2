---
title: "Khởi tạo Kinesis"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 3. </b> "
---


Trong phần này, chúng ta sẽ tiến hành khởi tạo một luồng dữ liệu trong Amazon Kinesis, tạo nền tảng cho việc thu thập và xử lý dữ liệu thời gian thực từ các nguồn khác nhau.

#### Các bước thực hiện:
1. Nhập **Kinesis** ở thanh tìm kiếm service trên AWS Console sau đó chọn **Kinesis**.
![0](/images/3-Kinesis/img-77.png)

2. Chọn **Create data stream**.
![0](/images/3-Kinesis/img-76.png)


3. Phần **Dât stream name**, chúng ta điền `KinesisDataStream`. Sau đó chọn **Provisioned**, nhập **1**. Cuối cùng chọn  **Create data stream**.
![0](/images/3-Kinesis/img-75.png)

4. Đợi khoảng 2 phút, trạng thái chuyển thành **Active** là hoàn thành.
![0](/images/3-Kinesis/img-74.png)
