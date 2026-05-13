---
title : "Khởi chạy RDS Instance"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 4.2 </b> "
---
### Tạo RDS Instance
Tìm đến trang quản lý của **Aurora và RDS**, tại thanh điều hướng bên trái
- Chọn **Databases**
- Chọn **Create Database**
- Chọn **Full configuration**
![4.2.1](/images/4-LaunchRDSInstance/4.2.1.png)

Tại trang **Create database**:
- Chọn loại: **MySQL**
- Chọn phương thức tạo: **Full configuration**
- Chọn template: **Dev/Test**
![4.2.2](/images/4-LaunchRDSInstance/4.2.2.png)

Tại phần **Deployment optionals**
- Chọn: **Multi-AZ DB deployment (2 instances)**
![4.2.3](/images/4-LaunchRDSInstance/4.2.3.png)

{{% notice tip %}}
Tùy chọn **Multi-AZ DB deployment (2 instances)** được sử dụng để đảm bảo tính sẵn sàng cao (High Availability) và khả năng tự động phục hồi cho hệ thống.

Cụ thể, AWS sẽ duy trì một bản sao dự phòng (Standby) tại một vùng sẵn sàng khác và tự động thực hiện failover (chuyển hướng kết nối) nếu bản chính gặp sự cố, giúp giảm thiểu tối đa thời gian gián đoạn (Downtime) mà không cần thay đổi cấu hình ứng dụng.
{{% /notice %}}

- Nhập tên DB instance: `table-cloud-pos-rds-instance`
- Nhập username: `admin`
- Nhập mật khẩu: `tablecloudpos2026`
![4.2.4](/images/4-LaunchRDSInstance/4.2.4.png)

- Chọn **Stand Classes (includes m classes)**
- Chọn loại instance: **db.m6gd.large(support Amazon RDS Optimized Writes)**
![4.2.5](/images/4-LaunchRDSInstance/4.2.5.png)

- Tài nguyên tính toán: Tích chọn **Don't connect to an EC2 Instance resource**
- Kết nối tới VPC **table-cloud-pos-vpc**
- Chọn Subnet **table-cloud-pos-db**
- Public Access: Tích chọn **No**
![4.2.6](/images/4-LaunchRDSInstance/4.2.6.png)

- Chọn **Security group** đã tạo cho DB: **table-cloud-pos-sg**
- Certificate authority: Chọn chứng chỉ mặc định **rds-ca-rsa2048-1**
![4.2.7](/images/4-LaunchRDSInstance/4.2.7.png)

- Kiểm tra kĩ lại các cấu hình và chọn **Create**
- Hoàn tất tạo DB instance và quá trình này phải chờ khoảng 15 phút để hiện Available