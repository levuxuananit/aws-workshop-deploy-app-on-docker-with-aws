---
title : "Kiểm tra ứng dụng"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 2.3 </b> "
---
### Kiểm tra kết quả triển khai
Truy cập `http://localhost:5173`. Khi đó chúng ta sẽ nhận được giao diện như sau:

![2.3.1](/images/2.local/2.3.1.png)

### Xác thực người dùng
Dùng một trong hai tài khoản sau để đăng nhập vào ứng dụng:
**User**: `user@example.com` / `123456`.
**Admin**: `admin@example.com` / `123456`.

{{% notice tip %}}
Trong môi trường sản xuất thực tế, cần sử dụng **AWS IAM Identity Center** hoặc **Amazon Cognito** cho xác thực an toàn hơn.
{{% /notice %}}

### Kiểm tra giao diện
Xác nhận đăng nhập thành công và kiểm tra tính nhất quán của dữ liệu hiển thị, sau đó thao tác trên các Route khác nhau để đảm bảo hệ thống điều hướng (Navigation) hoạt động ổn định.

![2.3.2](/images/2.local/2.3.2.png)
![2.3.3](/images/2.local/2.3.3.png)
![2.3.4](/images/2.local/2.3.4.png)
![2.3.5](/images/2.local/2.3.5.png)
![2.3.6](/images/2.local/2.3.6.png)

### Chuẩn bị cho triển khai AWS
Hệ thống vận hành ổn định trên Local là nền tảng quan trọng khẳng định mã nguồn đã sẵn sàng. Ở chương tiếp theo, chúng ta sẽ thực hiện **Cloud Migration** để đưa ứng dụng lên **AWS Cloud**. Bằng cách kết hợp **Docker** và **Amazon ECS** (Elastic Container Service), bạn sẽ nắm vững cách tận dụng khả năng tự động mở rộng (Auto-scaling) và quản lý Containers tập trung theo tiêu chuẩn **Enterprise**.