---
title : "Cấu hình EC2"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 5.1 </b> "
---
### Khởi tạo và Cấu hình EC2 Instance
Tại bước này, chúng ta sẽ thiết lập một máy chủ ảo đóng vai trò là môi trường vận hành ứng dụng trên nền tảng đám mây.
- Ở giao diện **AWS Management Console**.
- Tìm kiếm và chọn dịch vụ **EC2**.
![5.1.1](/images/5.EC2Config/5.1.1.png)

Tại giao diện quản lý **EC2 Dashboard**
- Chọn mục **Instances**.
- Nhấn nút **Launch Instances** để bắt đầu quy trình khởi tạo.
![5.1.2](/images/5.EC2Config/5.1.2.png)

Thiết lập thông số máy chủ
- Name: Đặt tên máy chủ là `table-cloud-pos-server`.
- Application and OS Images (AMI): Chọn hệ điều hành **Ubuntu**, phiên bản **Ubuntu Server 24.04 LTS**.
![5.1.3](/images/5.EC2Config/5.1.3.png)

- Key pair (login): **Chọn Create new key pair**.
- Key pair name: `pos-key`.
- Loại key: Chọn **RSA**
- Tích chọn định dạng key: `.pem` 
- Nhấn Create key pair và lưu file `.pem` an toàn để sử dụng truy cập SSH sau này.
![5.1.4](/images/5.EC2Config/5.1.4.png)

- Instance type: Chọn loại `t3.medium` để đảm bảo đủ tài nguyên vận hành Docker.
![5.1.5](/images/5.EC2Config/5.1.5.png)

Chỉnh sửa cấu hình mạng và bảo mật:
- Nhấn **Edit** tại phần **Network settings**.
![5.1.6](/images/5.EC2Config/5.1.6.png)

Thông số cấu hình:
- VPC: Chọn  `table-cloud-pos-vpc`
- Subnet: Chọn một trong các Public Subnet của Lab.
- Auto-assign public IP: Đảm bảo trạng thái là **Enable**.
- Firewall (Security Groups): Chọn **Select existing security group**.
- Common security groups: Tích chọn **table-cloud-pos-sg-public**.
![5.1.7](/images/5.EC2Config/5.1.7.png)

Hoàn tất khởi tạo

Kiểm tra lại các thông số và nhấn **Launch instance**.

### Gán IAM Role kết nối ECR cho EC2
Để EC2 có quyền tương tác an toàn với kho lưu trữ container (ECR) mà không cần cấu hình Access Key, chúng ta cần đính kèm Role đã tạo.

Tại giao diện danh sách Instances. Tìm và tích chọn vào máy chủ `table-cloud-pos-server` vừa khởi chạy.
- Chọn nút **Actions** ở góc trên.
- Chuyển đến mục **Security** và chọn **Modify IAM role**.
![5.1.8](/images/5.EC2Config/5.1.8.png)

### Cập nhật quyền hạn

Tại mục **IAM role**
- Tìm và chọn đúng Role: `CustomRWECRRole`.
- Nhấn **Update IAM role** để áp dụng thay đổi.
![5.1.9](/images/5.EC2Config/5.1.9.png)

### Kết quả
Máy chủ của bạn hiện đã được bảo mật bởi **Key Pair**, nằm trong vùng mạng an toàn của VPC và sở hữu "chứng chỉ" IAM Role để sẵn sàng đẩy/kéo các **Docker Images** từ **Amazon ECR**.