---
title : "Sử dụng ECR"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 8.1 </b> "
---
### Tạo ECR Repository để lưu các Docker Image
Tìm kiếm **Amazon Elastic Container Registry**.
- Chọn **Create**.
![8.1.1](/images/8.PushImage/8.1.1.png)

Chúng ta sẽ tạo **2 repositories** khác nhau để chứa các **Docker Image**:
- Repository name: `tablecloudpos-frontend` và `tablecloudpos-backtend`
- Image tag mutability: chọn **Mutable**.
- Encryption configuration: để mặc định.
![8.1.2](/images/8.PushImage/8.1.2.png)
![8.1.3](/images/8.PushImage/8.1.3.png)

Kết quả bạn bạn nhận được **repository** cho chứa 2 **Docker Image** khác nhau.
![8.1.4](/images/8.PushImage/8.1.4.png)

{{% notice tip %}}
Chúng ta cần phải tạo mỗi một repository cho mỗi một ứng dụng khác nhau để quản lý version của các Docker image dễ dàng hơn, đặc biệt là dùng để thực hiện [CI/CD](https://aws.amazon.com/vi/what-is/ci-cd-pipeline/) sau này.
{{% /notice %}}

### Cài AWS CLI
Theo mặc định (15/10/2024) thì AWS CLI không được cài đặt mặc định ở trong Ubuntu. Trước tiên thì chúng ta cần phải tải **unzip** trước: `sudo apt install unzip`
![8.1.5](/images/8.PushImage/8.1.5.png)

Sau đó thì chúng ta sẽ dùng các câu lệnh ở bên dưới để có thể cài đặt được AWS CLI.
```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

### Push các Docker Iamge lên Repository
Để push Docker Image của **frontend** lên ECR (tương tự cho **backend**).
- Đầu tiên vào lại **ECR Console**
- Chọn `tablecloudpos-frontend` (Nếu là backend: chọn `tablecloudpos-backend`)
- Ấn nút **View push commands**
![8.1.6](/images/8.PushImage/8.1.6.png)

- Khi đó một hộp thoại sẽ nhảy lên và chúng ta có thể thấy được một chuỗi các câu lệnh.
![8.1.7](/images/8.PushImage/8.1.7.png)

Trở lại với EC2 Instance, chúng ta cần phải dùng Root User để có thể đăng nhập vào trong ECR với Docker.
- Ở AWS console của **Push commands for tablecloudpos-frontend**

- Chọn câu lệnh thứ nhất để xác thực đăng nhập vào **Amazon Elastic Container Registry** (ECR) từ môi trường **Docker local** của bạn. Trước đó hay đảm bảo rằng bạn đã cấu hình **AWS Configure**.


{{% notice tip %}}
Bởi vì khi mà người dùng sử dụng sudo để đăng nhập vào ECR với Docker, thì credential được lưu ở trong HOME Dir của người dùng đó. Nhưng khi thực hiện lệnh push hoặc pull, thì nó sẽ xem credential ở trong Root thay vì là ở trong HOME Dir đã được lưu khi đăng nhập trước đó.
{{% /notice %}}

Ở các phần trước đó thì chúng ta đã tạo ra các Images cho từng ứng dụng rồi, nên là giờ chỉ cần gắn tag lại cho phù hợp rồi đẩy lên trên các **Registry** tương ứng.

Ở AWS console của **Push commands for tablecloudpos-frontend**
- Chọn dòng lệnh thứ 3 để thực hiện gắn tag, thay thế các tên resource image mà bạn tạo trước đó

{{% notice tip %}}
Format chung `<Account_ID>.dkr.ecr.<region>.amazonaws.com/<Repository_Name>:<Name_tag>`
{{% /notice %}}

Sau khi tạo xong thì tiến hành đẩy **Image** lên **ECR**
- Ở AWS console của **Push commands for tablecloudpos-frontend**
- Chọn lệnh `push`

Bạn tiến hành tương tự với **Image** của **backend**. Nhớ sao chép lại lệnh đăng nhập. Nhưng logout ra trước.

### Kết quả
Sau khi push xong, thì chúng ta có thể thấy được các image đã được đẩy lên trên từng **repository**.
![8.1.8](/images/8.PushImage/8.1.8.png)