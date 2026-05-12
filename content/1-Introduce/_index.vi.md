---
title : "Giới thiệu"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---
Workshop này hướng dẫn quy trình toàn diện từ đóng gói đến vận hành ứng dụng trên Docker Container. Bạn sẽ thực hành quản lý vòng đời ứng dụng thông qua các dịch vụ cốt lõi: Docker Hub, Nginx, Amazon ECR, Amazon RDS và Amazon EC2.

### Hệ thống dịch vụ sử dụng
- **Docker Hub**: Public Registry để lưu trữ và chia sẻ Docker Images.
- **Nginx**: Đóng vai trò Reverse Proxy và Load Balancer, tối ưu hóa phân phối lưu lượng và khả năng mở rộng.
- **Amazon ECR (Elastic Container Registry)**: Private Registry bảo mật trên AWS, tích hợp sâu để quản lý và triển khai Images.
- **Amazon RDS (Relational Database Service)**: Dịch vụ Managed Database, tự động hóa vận hành và đảm bảo an toàn dữ liệu.
- **Amazon EC2 (Elastic Compute Cloud)**: Hạ tầng máy chủ ảo (Compute) để chạy các Docker Containers.

### Quy trình vận hành
- **Traffic Ingress:**: Request từ Client được gửi qua Internet, đi qua Internet Gateway để tiến vào hệ thống VPC trên AWS.
 
**Reverse Proxy & Routing:**: Nginx tiếp nhận traffic và đóng vai trò Reverse Proxy, điều phối các yêu cầu đến đúng Container: Backend Container, frontend Container

- **App Logic & Data Processing:**
  - Frontend (React) gửi yêu cầu đến Backend (Node.js) để xử lý nghiệp vụ.
  - Backend (Node.js) thực hiện các truy vấn CRUD với Amazon RDS.
  - Dữ liệu sau khi xử lý được trả về (Response) theo luồng ngược lại: **Backend → Nginx → Client**.

- **CI/CD & Image Management:**
    - Khi cập nhật mã nguồn (React/Node.js), các Docker Images mới được đóng gói và Push lên Docker Hub hoặc Amazon ECR.
  - Từ các Registry này, ứng dụng sẽ được Deploy hoặc cập nhật trực tiếp lên các instance Amazon EC2.
  
{{% notice note %}}
Luôn kiểm tra cấu hình **Security Groups** để đảm bảo kết nối thông suốt giữa Nginx, Backend và RDS.
{{% /notice %}}
