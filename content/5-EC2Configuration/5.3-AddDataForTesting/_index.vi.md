---
title : "Khởi tạo Dữ liệu cho Amazon RDS"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 5.3 </b> "
---
Để ứng dụng có thể vận hành và hiển thị thông tin, chúng ta cần nạp các bản ghi ban đầu vào cơ sở dữ liệu Amazon RDS thông qua file kịch bản SQL có sẵn trong mã nguồn.

### Chuẩn bị Script SQL
Đầu tiên, chúng ta cần xác định đường dẫn tuyệt đối của file init.sql để thực thi chính xác trong môi trường MySQL.
- Di chuyển vào thư mục database:
```bash
cd ~/aws-fcj-container-app/database
```

- Lấy đường dẫn đầy đủ của file:
```bash
echo $(pwd)/init.sql
```

- Thông thường sẽ là: `/home/ubuntu/aws-fcj-container-app/database/init.sql`.
- Hãy sao chép đường dẫn này

### Kết nối tới RDS Instance
Sử dụng công cụ mysql-client để thiết lập kết nối từ EC2 đến máy chủ cơ sở dữ liệu.
- Lấy thông tin Endpoint: Truy cập giao diện RDS Console, chọn Database Instance bạn đã tạo và sao chép giá trị tại mục Endpoint.
- Thực hiện lệnh kết nối:
```bash
mysql -h <your-rds-endpoint> -u admin -p
```
- Nhập mật khẩu bạn đã thiết lập khi tạo RDS để đăng nhập

### Thực thi Script nạp dữ liệu
Sau khi đã truy cập vào giao diện dòng lệnh của MySQL, hãy sử dụng lệnh source kèm theo đường dẫn đã sao chép ở Bước 1 để chạy script:
```bash
source /home/ubuntu/aws-fcj-container-app/database/init.sql;
```

### Kiểm tra và Xác nhận Kết quả
Hãy đảm bảo rằng dữ liệu đã được cấu trúc và nhập vào thành công bằng các câu lệnh truy vấn sau:
- Kiểm tra danh sách Database:
```sql
SHOW DATABASES;
```
- Bạn sẽ thấy database fcjresbar xuất hiện trong danh sách

Kiểm tra chi tiết dữ liệu:
- Truy cập vào database:
```sql
USE fcjresbar;
```

- Truy vấn bảng dữ liệu:
```sql
SELECT * FROM Clients;
```

Lưu ý: Nếu bạn không thể kết nối, hãy kiểm tra lại Inbound Rules của Security Group gán cho RDS. Đảm bảo port 3306 đã được mở cho Security Group của máy chủ EC2.