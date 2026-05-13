---
title : "Tạo IAM Roles để truy cập vào ECR"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 3.3 </b> "
---
### Khởi tạo IAM Policies cho ECR
Chúng ta sẽ tạo hai **policy** riêng biệt: một để đọc (Pull) và một để ghi (Push) dữ liệu vào kho lưu trữ **container**.

#### Tạo Policy: ReadECRRepositoryContent (Quyền Đọc)
Ở giao diện **IAM (Identity and Access Management)**
- Tại danh mục bên trái, chọn **Policies** và nhấn **Create policy**.
![3.12](/images/3.preparation/3.12.png)

Trong phần **Policy editor**:
- Chọn service là **Elastic Container Registry**.
- Chọn **Next**. 
![3.13](/images/3.preparation/3.13.png)

Cấu hình các quyền (Actions)
- Nhóm List: Chọn `DescribeImages` và `ListImages`.
- Nhóm Read: Chọn `BatchGetImage`, `DescribeRepositories`, `GetAccountSettings`, `GetAuthorizationToken`.
![3.14](/images/3.preparation/3.14.png)

- Phần Resources: Chọn **Specific**, sau đó tích chọn **Any in this account** (cho phép áp dụng với mọi Repository trong tài khoản này).
- Chọn **Next**.
![3.15](/images/3.preparation/3.15.png)

Hoàn tất Policy chi tiết
- Policy name: `ReadECRRepositoryContent`
- Description: `Allow pull images and describe repositories`.
- Nhấn **Create policy**.
![3.16](/images/3.preparation/3.16.png)

#### Tạo Policy: WriteECRRepositoryContent (Quyền Ghi)
Tại giao diện **Policies**,
- Nhấn tiếp **Create policy**
- Chọn service **Elastic Container Registry**.

Cấu hình các quyền (Actions)
- Nhóm Read: Chọn `BatchCheckLayerAvailabilit`y và `GetAuthorizationToken`.
- Nhóm Write: Chọn `CompleteLayerUpload`, `InitiateLayerUpload`, `PutImage`, và `UploadLayerPart`.
![3.17](/images/3.preparation/3.17.png)

- Phần Resources: Chọn **Any in this account**.
- Chọn **Next**.
![3.18](/images/3.preparation/3.18.png)

Hoàn tất Policy chi tiết
- Policy name: `WriteECRRepositoryContent`
- Description: `Allow push images to ECR`.
- Nhấn **Create policy**.
![3.19](/images/3.preparation/3.19.png)

### Khởi tạo IAM Role cho EC2 Instance
Sau khi có các Policy, chúng ta cần tạo một Role để gán cho máy chủ EC2, giúp máy chủ có quyền tương tác với ECR mà không cần dùng Access Key thủ công.

Tại giao diện quản lý **IAM**
- Ở danh mục bên trái, chọn **Roles**.
- Nhấn nút **Create role**.

Thiết lập thực thể tin cậy
- Trusted entity type: Chọn **AWS service**.
- Service or use case: Chọn **EC2**.
- Nhấn **Next**.

Gán chính sách
- Tại ô tìm kiếm, lọc theo Filter by Type: chọn `Customer managed`.
- Tìm và tích chọn cả 2 policy vừa tạo: `ReadECRRepositoryContent` và `WriteECRRepositoryContent`.
- Nhấn **Next**.

Đặt tên và Hoàn tất
- Role name: `CustomRWECRRole`
- Description: `Custom Role for EC2 to Read and Write to ECR`.
- Kiểm tra lại danh sách các policy đã đính kèm và nhấn **Create role**.

### Kết quả
**Tính bảo mật cao**: Thay vì lưu tài khoản/mật khẩu trực tiếp trên máy chủ EC2, chúng ta dùng IAM Role. AWS sẽ tự động cấp một "vé thông hành" (Temporary Credentials) tạm thời cho máy chủ, giúp giảm rủi ro bị lộ lọt thông tin.

**Nguyên tắc đặc quyền tối thiểu (Least Privilege)**: Việc chia nhỏ Policy thành Read và Write giúp bạn kiểm soát chặt chẽ:
- Chỉ những Server cần đẩy ảnh lên mạng mới được cấp quyền Write.
- Còn Server chỉ chạy ứng dụng thì chỉ cần quyền Read.