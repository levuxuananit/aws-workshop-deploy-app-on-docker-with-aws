---
title : "Cấu hình Security Group"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 3.2 </b> "
---
### Cấu hình Security Group cho EC2 Instance (Public Access)
**Security Group** này đóng vai trò như một tường lửa ảo cho các máy chủ Web hoặc Application có nhu cầu giao tiếp với Internet.

Tại giao diện quản lý **EC2**:
- Ở danh mục điều hướng bên trái, tìm đến mục **Network & Security**.
- Chọn **Security Groups**.
- Nhấn nút **Create security group**.
![3.9](/images/3.preparation/3.9.png)

Thiết lập thông tin cơ bản:
- Security group name: `table-cloud-pos-sg-public`
- Description: `SG for Table Cloud POS`
- VPC: Chọn `table-cloud-pos` (Đảm bảo chọn đúng VPC đã tạo ở bước trước thay vì VPC mặc định).

Cấu hình **Inbound rules**:
- Chọn **Add rule**.
- **Quy tắc 1**: Chọn Type `SSH`, Source `Anywhere-IPv4` (0.0.0.0/0), cho phép quản trị viên truy cập từ xa vào server qua dòng lệnh.
- **Quy tắc 2**: Chọn Type `HTTP`, Source `Anywhere-IPv4` (0.0.0.0/0), cho phép người dùng truy cập vào website qua giao thức web không bảo mật.
- **Quy tắc 3**: Chọn Type `HTTPS`, Source `Anywhere-IPv4` (0.0.0.0/0), cho phép truy cập web an toàn qua chứng chỉ SSL/TLS.
- **Quy tắc 4**: Chọn Type `Custom TCP`, Port range `3000`, Source `Anywhere-IPv4` (0.0.0.0/0), mở cổng đặc thù cho ứng dụng (ví dụ: Node.js hoặc React) thường chạy ở port 3000.
![3.10](/images/3.preparation/3.10.png)

Giữ nguyên mặc định của **Outbound rules** để server có thể tự do tải cập nhật từ Internet.
- Nhấn **Create security group**.

### Cấu hình Security Group cho Database Instance (Private Access)
**Security Group** này được thiết lập để bảo vệ cơ sở dữ liệu, chỉ cho phép các máy chủ nội bộ truy cập, giúp tăng tối đa tính bảo mật.

Tại giao diện **Security Groups**, tiếp tục nhấn chọn **Create security group**.

Thiết lập thông tin cơ bản
- Security group name: `table-cloud-sg-db`
- Description: `SG for Table Cloud POS database`
- VPC: Chọn `table-cloud-pos`

Cấu hình quy tắc đầu vào (Inbound rules)
- Chọn **.Add rule**
- Type: `MySQL/Aurora` (Mặc định mở port 3306).
- Source: Thay vì chọn IP, hãy tìm và chọn chính `table-cloud-pos-sg-public`.
- Quy tắc này chỉ cho phép các EC2 Instance nào được gán nhãn **table-cloud-pos-sg-public** mới có quyền kết nối đến Database. Mọi truy cập từ bên ngoài Internet vào Database sẽ bị chặn hoàn toàn.
- **Outbound rules**: Giữ nguyên mặc định.
- Nhấn **Create security group**.
![3.11](/images/3.preparation/3.11.png)

Bạn đã tạo ra một kiến trúc bảo mật 2 lớp: Lớp Web (Public SG) mở cửa cho Internet, và lớp Database (Private SG) chỉ mở cửa cho lớp Web. Đây là mô hình bảo mật tiêu chuẩn trên AWS.