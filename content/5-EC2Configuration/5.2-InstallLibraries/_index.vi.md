---
title : "Chuẩn bị Môi trường và Mã nguồn trên EC2"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 5.2 </b> "
---
### Cập nhật hệ thống và Kết nối
Đầu tiên, hãy sử dụng giao thức Secure Shell (SSH) để truy cập vào EC2 Instance của bạn.
- Trên **VSCode**, để SSH đến EC2 trên AWS bạn có thể cài đặt extension: `Remote-SSH`
- Sau khi cài đặt thành công, tại góc dưới bên trái màn hình, bấm chọn biểu tượng **><** để mở chế độ kết nối.
- Chọn **Connect to host...**
- Tiếp theo, bạn có thể chọn 1 trong 2 options sau:
  - **+Add New SSH Host...**: Dán câu lệnh `ssh -i "C/Users/Legion/Downloads/pos-key.pem" ubuntu@18.143.134.165 ` trong đó:
    - Copy câu lệnh SSH bằng cách: chọn **EC2 Instance** muốn kết nối, chọn **Connect**, chọn **SSH client**, copy câu lệnh.
    - Cấu trúc câu lệnh SSH: **ssh -i "`địa-chỉ-key.pem-trên-máy-bạn`" `username`@`IP-Public`**
![5.2.1](/images/5.EC2Config/5.2.2.png)
![5.2.2](/images/5.EC2Config/5.2.1.png)
  - **Configure SSH Hosts...**: Chọn **file config** trên máy bạn, Cấu hình như mẫu bên dưới:
  ```yaml
  Host table-cloud-pos-ec2                               # Name host: table-cloud-pos-ec2
    HostName 18.143.134.165                              # IP-Public: 18.143.134.165
    User ubuntu                                          # username: ubuntu
    IdentityFile "C:/Users/Legion/Downloads/pos-key.pem" # địa chỉ key.pem trên máy
  ```

- Chọn **table-cloud-pos-ec2** để kết nối đến EC2 Instance trên AWS.
- Chọn **Linux**.
- Kết quả thành công khi góc dưới bên trái sẽ hiện thị tên host bạn kết nối.
![5.2.3](/images/5.EC2Config/5.2.3.png)
 
### Cập nhật hệ thống
Ngay khi đăng nhập thành công, việc đầu tiên cần làm là cập nhật danh sách gói phần mềm để đảm bảo hệ thống luôn ở trạng thái ổn định và bảo mật nhất.
- Gõ lệnh dưới đây vào terminal:
```bash
sudo apt update -y
sudo apt upgrade -y
```
![5.2.4](/images/5.EC2Config/5.2.4.png)

### Cài đặt Docker Engine
**Docker** là thành phần cốt lõi để triển khai ứng dụng dưới dạng **Container**. Chúng ta sẽ tiến hành cài đặt phiên bản chính thức từ **Docker Repository**.

Thiết lập GPG Key và Repository, Thêm GPG key chính thức của Docker:
```bash
# 
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

{{% notice tip %}}
Việc cài đặt trực tiếp từ **Repository** chính thức của **Docker** giúp bạn sở hữu phiên bản mới nhất, tối ưu hiệu suất và hỗ trợ đầy đủ các tính năng của **Docker Compose V2**.
{{% /notice %}}

Thêm repository vào Apt sources:
```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```
![5.2.5](/images/5.EC2Config/5.2.5.png)

Cài đặt các thành phần Docker và Docker Compose:
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```
![5.2.6](/images/5.EC2Config/5.2.6.png)

### Cài đặt MySQL Client
Để có thể tương tác, kiểm tra và quản trị dữ liệu trên dịch vụ Amazon RDS từ xa, chúng ta cần cài đặt công cụ MySQL Client.
```bash
sudo apt install mysql-client -y
```
![5.2.7](/images/5.EC2Config/5.2.7.png)

### Kiểm tra trạng thái và Clone mã nguồn
Trước khi bắt đầu triển khai, hãy đảm bảo các công cụ đã được cài đặt chính xác bằng cách kiểm tra phiên bản:
- Docker: `docker --version`
- MySQL Client: `mysql --version`
- Git: git `--version` (Thường đã có sẵn trên Ubuntu 24.04).
![5.2.8](/images/5.EC2Config/5.2.8.png)
![5.2.9](/images/5.EC2Config/5.2.9.png)

Khi mọi thứ đã sẵn sàng, tiến hành tải mã nguồn dự án từ GitHub về máy chủ. Dùng lệnh **ls** để kiểm tra thông tin các tệp tin bên trong.
```bash
git clone https://github.com/levuxuananit/aws-table-cloud-pos.git
ls
cd aws-table-cloud-pos
ls
```
![5.2.10](/images/5.EC2Config/5.2.10.png)

Cài đặt thành công môi trường cần thiết để triển khai các bước tiếp theo.