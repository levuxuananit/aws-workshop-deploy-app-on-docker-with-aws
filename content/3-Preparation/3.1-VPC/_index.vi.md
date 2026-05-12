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

### Cấu hình Public Subnet cho Subnet
Sau khi khởi tạo VPC, chúng ta cần cấu hình để các Subnet công cộng tự động cấp phát địa chỉ IP cho các tài nguyên bên trong.

Tại giao diện quản lý VPC
- Ở danh mục điều hướng bên trái, kéo xuống mục **Virtual private cloud**, chọn **Subnets**.
- Tại thanh tìm kiếm, nhập từ khóa `table-cloud-pos` để lọc các Subnet liên quan.
![3.6](/images/3.preparation/3.6.png)

Cấu hình cho **public subnet 1**
- Tìm và tích chọn vào Subnet có tên: `table-cloud-pos-subnet-public1-ap-southeast-1a`
- Chọn nút **Actions** ở phía trên bên phải giao diện.
- Chọn mục **Edit subnet settings**.
![3.7](/images/3.preparation/3.7.png)

Tại bảng cấu hình, tìm đến phần **Auto-assign IP settings**
- Tích chọn vào ô **Enable auto-assign public IPv4 address**.
- Kéo xuống dưới cùng và chọn **Save** để lưu thay đổi.
![3.8](/images/3.preparation/3.8.png)

Cấu hình tương tự cho Cấu hình cho **public subnet 2**
- Tìm và tích chọn vào Subnet có tên: `table-cloud-pos-subnet-public2-ap-southeast-1b`
- Chọn nút **Actions** ở phía trên bên phải giao diện.
- Chọn mục **Edit subnet settings**.
  
Tại bảng cấu hình, tìm đến phần **Auto-assign IP settings**
- Tích chọn vào ô **Enable auto-assign public IPv4 address**.
- Kéo xuống dưới cùng và chọn **Save** để lưu thay đổi.
![3.8](/images/3.preparation/3.8.png)

Hoàn tất việc cấu hình VPC và kích hoạt tính năng tự động cấp phát **Public IPv4** cho các Public Subnet. Giờ đây, bất kỳ tài nguyên nào (như EC2 Instance) khi được triển khai vào các Subnet này sẽ mặc định có địa chỉ IP công cộng để giao tiếp với Internet.

