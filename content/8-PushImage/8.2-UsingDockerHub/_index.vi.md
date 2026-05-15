---
title : "Sử dụng Docker Hub"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 8.2 </b> "
---
### Tạo repository trên Docker Hub
Vào **Docker Hub** đã được chuẩn bị sẵn và tạo một **repository** trong đó.
- Chọn **Create a Repository**
![8.2.1](/images/8.PushImage/8.2.1.png)

Cấu hình cho Repository của **frontend**:
- Nhập tên repository: `tablecloudpos-frontend`
- Nhập mô tả: `Frontend Image of Table Cloud POS`
- Chọn **public**.
- Kiểm tra lại và chọn **Create**.
![8.2.2](/images/8.PushImage/8.2.2.png)

Tương tự, bạn cấu hình cho Repository của **backend**:
- Nhập tên repository: `tablecloudpos-backend`
- Nhập mô tả: `Backend Image of Table Cloud POS`
- Chọn **public**.
- Kiểm tra lại và chọn **Create**.
![8.2.3](/images/8.PushImage/8.2.3.png)

Hoàn tất tạo 2 **Repository** để cửa 2 **Image** của **web server** và **application** trên **Docker Hub**.
![8.2.4](/images/8.PushImage/8.2.4.png)

### Push Image lên Repository trên Docker Hub
Giờ thì chúng ta đã sẵn sàng đẩy các **image** lên trên từng **repositories**.
- Logout và đăng nhập vào Docker Hub.
- Nhờ là đăng nhập đúng tài khoản và mật khẩu của tài khoản mà bạn đã tạo các repositories ở bước vừa rồi.
![8.2.5](/images/8.PushImage/8.2.5.png)

- Thay đổi tag cho **backend image** và **frontend image**.
![8.2.6](/images/8.PushImage/8.2.6.png)

- Đẩy **backend image** và **frontend image** lên Docker Hub.
![8.2.7](/images/8.PushImage/8.2.7.png)

### Kết quả
Sau khi push xong, thì chúng ta có thể thấy được các image đã được đẩy lên trên từng **repository**.
![8.2.8](/images/8.PushImage/8.2.8.png)
![8.2.9](/images/8.PushImage/8.2.9.png)
