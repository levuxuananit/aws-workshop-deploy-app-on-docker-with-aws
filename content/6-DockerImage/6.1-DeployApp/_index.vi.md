---
title : "Triển khai ứng dụng"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 6.1 </b> "
---
### Lợi thế của mô hình Cloud-Native
Ở phần Deploy on Local trước đó, chúng ta đã triển khai thủ công lần lượt Database Server, Web Server và End User Application. Cách làm này bộc lộ nhiều hạn chế về quản lý phụ thuộc và tính nhất quán. Trong phần này, chúng ta sẽ đưa toàn bộ hạ tầng lên Cloud bằng Docker.

Việc sử dụng Docker giúp loại bỏ hoàn toàn nỗi lo về "tải về và cài đặt" thủ công. Chỉ cần bạn nắm vững các khái niệm cơ bản về Docker (đặc biệt là Network), phần này sẽ trở nên cực kỳ đơn giản.

- **Database**: Ở bước trước, chúng ta đã cấu hình Database với** Amazon RDS**. Mọi vấn đề về bảo trì, tính sẵn sàng và an toàn dữ liệu đã được AWS tối ưu, giúp chúng ta tập trung hoàn toàn vào việc đóng gói ứng dụng bằng Docker Image.

- **Môi trường**: Nếu triển khai tại Local được xem là **môi trường phát triển** (Development), thì việc sử dụng Docker trên Cloud chính là bước đệm tiến tới **môi trường kiểm thử** (Staging) hoặc **sản phẩm** (Production) thực tế.

### Triển khai Web Server (Backend)
Đầu tiên, hãy truy cập vào thư mục mã nguồn **aws-table-cloud-pos** đã clone. Tại thư mục **backend**, chúng ta cần điều chỉnh cấu hình để kết nối tới Database trên Cloud:
- Trên **Terminal**, gõ lệnh sau để mở  `file .env`.
```bash
ls

cd backend

vim .env
```
![6.1.1](/images/6-DockerImage/6.1.1.png)

Cập nhật biến **DB_HOST** bằng Endpoint của **Amazon RDS** mà bạn đã khởi tạo.
- Nhấn phím **i** (viết tắt của Insert).
- Lúc này, ở dưới cùng góc trái màn hình terminal sẽ hiện chữ **-- INSERT --**.
- Bây giờ bạn có thể dùng các phím mũi tên để di chuyển và nhập liệu/xóa như bình thường.
- Bạn di chuyển đến dòng **DB_HOST** và thay đổi giá trị thành Endpoint của RDS như hướng dẫn.
![6.1.2](/images/6-DockerImage/6.1.2.png)

Thoát và lưu file
- Sau khi sửa xong, bạn thực hiện trình tự:
- Nhấn phím **Esc** để thoát khỏi chế độ **Insert** (chữ -- INSERT -- sẽ biến mất).
- Gõ lệnh `:wq` rồi nhấn **Enter**.
    : : Bắt đầu nhập lệnh cho Vim.
    w : Ghi lại (Write/Save).
    q : Thoát (Quit).
![6.1.3](/images/6-DockerImage/6.1.3.png)



### Đóng gói Web Server thành Docker Image (Build Image)
Giờ thì **web serve**r của chúng ta cũng đã sẵn sàng để chạy. Tiếp theo, tiến hành đóng gói ứng dụng thành **Docker Image**
```bash
sudo docker build . -t backend-image
```
![6.1.4](/images/6-DockerImage/6.1.4.png)

Trước khi bắt đầu chạy **Container** cho **web server**, thì mình sẽ cần phải tạo một **network** cho các container trong môi trường giao tiếp với nhau.
```bash
sudo docker network create my-network
```

Sau đó là tiến hành chạy **Docker Container** với **Docker Image** vừa mới tạo
```bash
sudo docker run -p 5000:5000 --network my-network --name backend backend-image
```
![6.1.5](/images/6-DockerImage/6.1.5.png)


### Triển khai Application (Frontend)
Bây giờ, hãy mở một SSH Session mới để triển khai phần giao diện người dùng. Các bước thực hiện tương tự như phần Backend:
- Di chuyển vào thư mục `frontend`.
```bash
cd aws-table-cloud-pos
cd frontend
```

### Đóng gói Application thành Docker Image (Build Image)
Nhập dòng lệnh sau để đóng gói **Application** thành **Docker Image**:
```bash
    sudo docker build . -t frontend-image
```
![6.1.6](/images/6-DockerImage/6.1.6.png)

Sau đó là tiến hành chạy **Docker Container** với **Docker Image** vừa mới tạo. Chúng ta sẽ map **port 80** bên trong container ra **port 3000** để người dùng có thể truy cập: 
```bash
    sudo docker run -d -p 3000:80 --network my-network --name frontend frontend-image
 ```
![6.1.7](/images/6-DockerImage/6.1.7.png)

### Khắc phục sự cố lỗi phiên bản
Cụ thể, đối với dự án đang triển khai, Vite yêu cầu bộ API Web Crypto vốn chỉ được hỗ trợ đầy đủ và ổn định từ Node.js phiên bản **18 hoặc 20 trở lên**. Trong môi trường Docker Container của bạn nếu phiên bản Node.js có thể đang thấp hơn mức này thì sẽ nhận được lỗi như hình:
![6.1.8](/images/6-DockerImage/6.1.8.png)

Các khắc phục:
  - Truy cập vào **DockerFile** của **frontend**
  - Sửa FROM thành `node-20-alpine` (nâng lên phiên bản cao hơn để đảm bảo **API Web Crypto** chạy ổn định)
![6.1.9](/images/6-DockerImage/6.1.9.png)
![6.1.10](/images/6-DockerImage/6.1.10.png)
![6.1.11](/images/6-DockerImage/6.1.11.png)

### Tổng kết

Đến đây, bạn đã hoàn tất việc chuyển đổi từ triển khai thủ công sang sử dụng **Docker Image** trên Cloud. Bạn có thể thấy quy trình đã gọn gàng hơn rất nhiều. 

Tuy nhiên, việc chạy từng lệnh `docker run` cho từng dịch vụ vẫn còn khá rời rạc. Trong phần tiếp theo, chúng ta sẽ nâng cấp lên **Docker Compose** để quản lý toàn bộ stack công nghệ chỉ với một file cấu hình duy nhất.

Bạn sẽ thấy rõ sự khác biệt giữa: **Deploy Local** vs. **Docker Image** vs. **Docker Compose**.