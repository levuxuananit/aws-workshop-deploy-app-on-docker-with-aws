---
title : "Triển khai ứng dụng"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 5.1 </b> "
---
### Lợi thế của mô hình Cloud-Native
Ở phần Deploy on Local trước đó, chúng ta đã triển khai thủ công lần lượt Database Server, Web Server và End User Application. Cách làm này bộc lộ nhiều hạn chế về quản lý phụ thuộc và tính nhất quán. Trong phần này, chúng ta sẽ đưa toàn bộ hạ tầng lên Cloud bằng Docker.

Việc sử dụng Docker giúp loại bỏ hoàn toàn nỗi lo về "tải về và cài đặt" thủ công. Chỉ cần bạn nắm vững các khái niệm cơ bản về Docker (đặc biệt là Network), phần này sẽ trở nên cực kỳ đơn giản.

- **Database**: Ở bước trước, chúng ta đã cấu hình Database với** Amazon RDS**. Mọi vấn đề về bảo trì, tính sẵn sàng và an toàn dữ liệu đã được AWS tối ưu, giúp chúng ta tập trung hoàn toàn vào việc đóng gói ứng dụng bằng Docker Image.

- **Môi trường**: Nếu triển khai tại Local được xem là **môi trường phát triển** (Development), thì việc sử dụng Docker trên Cloud chính là bước đệm tiến tới **môi trường kiểm thử** (Staging) hoặc **sản phẩm** (Production) thực tế.

### Triển khai Web Server (Backend)
Đầu tiên, hãy truy cập vào thư mục mã nguồn aws-fcj-container-app đã clone. Tại thư mục backend, chúng ta cần điều chỉnh cấu hình để kết nối tới Database trên Cloud:

Mở file .env và cập nhật biến DB_HOST bằng Endpoint của Amazon RDS mà bạn đã khởi tạo.