---
title : "Triển khai trên local"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---
Tại sao chúng ta nên đóng gói ứng dụng trong **Docker Container** thay vì chạy trực tiếp trên hệ điều hành máy tính cá nhân?

Để một ứng dụng hoạt động ổn định và xử lý mượt mà các yêu cầu từ người dùng (thêm, sửa, xóa dữ liệu...), hệ thống cần tiêu tốn tài nguyên phần cứng từ máy chủ (Host). Tuy nhiên, việc triển khai truyền thống thường gặp lỗi "máy tôi chạy được nhưng máy khác thì không" do sự khác biệt về môi trường.

Trong phần này, chúng ta sẽ bắt đầu triển khai một ứng dụng mẫu ngay trên máy tính của bạn để quan sát cách Docker giải quyết vấn đề xung đột môi trường và quản lý tài nguyên hiệu quả như thế nào.

### Nội dung
1. [Cài đặt môi trường](2-Local/2.1-Setup)
2. [Triển khai ứng dụng](2-Local/2.2-Deploy)
3. [Kiểm tra ứng dụng](2-Local/2.3-Testing)