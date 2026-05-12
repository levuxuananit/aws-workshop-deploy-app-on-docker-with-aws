---
title : "Triên khai ứng dụng trên Docker với AWS"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
---
### Giới thiệu
Hướng dẫn triển khai ứng dụng trên Docker sử dụng các dịch vụ AWS như EC2, RDS, và Amazon ECR.

{{% notice tip %}}
- **Triển khai**: Sử dụng **Amazon ECS** hoặc **Amazon EKS** để quản lý **Container** tối ưu cho môi trường **Production**.
- **Bảo mật**: Thiết lập **VPC** và **Security Groups** theo đúng **AWS Shared Responsibility Model**.
- **Chi phí**: Kiểm soát tài nguyên trên **AWS Billing** và thực hiện **Cleanup** ngay sau khi sử dụng.
{{% /notice %}}

[kiến trúc hệ thống]()

### Nội dung
 1. [Giới thiệu](1-introduce/)
 2. [Các bước chuẩn bị](2-Prerequiste/)
 3. [Tạo kết nối đến máy chủ EC2](3-Accessibilitytoinstance/)
 4. [Quản lý session logs](4-s3log/)
 5. [Port Forwarding](5-Portfwd/)
 6. [Dọn dẹp tài nguyên](6-cleanup/)
