---
title : "Cấu hình VPC"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 3.1 </b> "
---
### Khởi tạo VPC
Ở giao diện **AWS Management Console**
- Tìm kiếm dịch vụ VPC trên thanh tìm kiếm và chọn kết quả tương ứng.
- Chọn **Region** `ap-southeast-1` (Singapore) để giảm độ trễ.
- Tại bảng điều hướng bên trái, chọn **Your VPCs**.
- Chọn nút **Create VPC**.
![3.1](/images/3.preparation/3.1.png)

Tại trang cấu hình VPC
- Trong mục **Resources to create**, chọn tùy chọn **VPC and more**.
![3.2](/images/3.preparation/3.2.png)

- Tại mục **Name tag auto-generation**, nhập tên: `table-cloud-pos`
![3.3](/images/3.preparation/3.3.png)

- Tại mục VPC endpoint, chọn **None** để tối ưu hóa chi phí và đơn giản hóa cấu hình.
![3.4](/images/3.preparation/3.4.png)

- Kiểm tra lại các thông số và chọn **Create VPC**.

- Tạo VPC thành công.
![3.5](/images/3.preparation/3.5.png)
