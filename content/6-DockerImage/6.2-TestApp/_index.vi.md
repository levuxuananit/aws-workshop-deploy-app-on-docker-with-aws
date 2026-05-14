---
title : "Triển khai ứng dụng"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 6.2 </b> "
---
###  Sao chép Public IPv4 của EC2 Instance
Quay lại trong EC2 Console, chúng ta cần sẽ sao chép lại **Public IPv4** của EC2 mà nãy giờ chúng ta đã thao tác, sau đó là thêm vào trình duyệt URL như sau: `http://public-dns-of-your-ec2:3000`
![6.2.1](/images/6-DockerImage/6.2.1.png)

### Kiểm tra ứng dụng
Đến đây ứng dụng đã chạy ổn định với các chức năng **CRUD**, và **backend** đã có thể lấy dữ liệu từ **database** (Amazon RDS) và hiển thị đầy đủ trên **frontend**.
![6.2.2](/images/6-DockerImage/6.2.2.png)
![6.2.3](/images/6-DockerImage/6.2.3.png)
![6.2.4](/images/6-DockerImage/6.2.4.png)s
