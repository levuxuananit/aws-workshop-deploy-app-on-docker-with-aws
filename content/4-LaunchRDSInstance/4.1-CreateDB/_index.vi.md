---
title : "Tạo DB Subnet Group"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 4.1 </b> "
---
### Tạo Subnet Group DB trong Amazon RDS 
Việc thiết lập **DB Subnet Group** là bước khởi đầu quan trọng để định nghĩa không gian mạng và đảm bảo tính quản trị tập trung cho các tài nguyên cơ sở dữ liệu bên trong VPC.

Truy cập dịch vụ **Amazon RDS** trên **AWS Management Console**. Sử dụng thanh tìm kiếm để truy cập vào dashboard của `Amazon RDS`:
- Tìm đến mục **Subnet groups** ở danh sách tính năng bên trái.
- Nhấn **Create DB subnet group**.
![4.1.1](/images/4-LaunchRDSInstance/4.1.1.png)

Thiết lập thông số định danh cơ bản:
- Tên nhóm là `table-cloud-pos-db`
- Mô tả mục đích sử dụng là `Subnet Group for Order Managment`
- Chọn VPC là `table-cloud-pos-vpc`

Phân bổ tài nguyên Subnet:
- Lựa chọn các **Availability Zones** (AZs) tương ứng với kiến trúc hạ tầng đã triển khai.
- Sau đó chỉ định **02 Private Subnets** để hệ thống có thể cấp phát địa chỉ IP nội bộ cho database.
![4.1.2](/images/4-LaunchRDSInstance/4.1.2.png)

Kiểm tra và hoàn tất khởi tạo:
- Thực hiện rà soát lại danh sách các subnet đã chọn nhằm đảm bảo tính chính xác về mặt kỹ thuật.
- Nhấn **Create** để hệ thống ghi nhận cấu hình.

{{% notice tip %}}
**Pro Tip**: Việc tích hợp nhiều **Availability Zones** vào một **Subnet Group** là điều kiện tiên quyết để triển khai **kiến trúc Multi-AZ**, giúp cơ sở dữ liệu của bạn tự động duy trì hoạt động ngay cả khi một trung tâm dữ liệu gặp sự cố.

**Security Note**: Luôn ưu tiên đặt các **RDS Instance** bên trong **Private Subnet** nhằm cô lập hoàn toàn tài nguyên khỏi môi trường Internet, chỉ cho phép truy xuất nội bộ để tối đa hóa tính bảo mật cho dữ liệu.
{{% /notice %}}

Sau khi quy trình kết thúc, **DB Subnet Group** mới sẽ hiển thị trong trạng thái **Available** trên bảng danh sách điều khiển.