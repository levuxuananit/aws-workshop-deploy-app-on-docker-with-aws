---
title : "Dọn dẹp tài nguyên"
date :  "`r Sys.Date()`" 
weight : 9 
chapter : false
pre : " <b> 9. </b> "
---
### Dọn Dẹp Elastic Container Registry

Trên giao diện AWS Console:
- Tìm kiếm và chọn **Elastic Container Registry**.
- Chọn **Repositories**.
- Chọn **tablecloudpos-backend**
- Nhấn **Delete**.
![9.1](/images/9.Delete/9.1.png)

- Nhập `delete`.
- Nhấn **Delete**.
![9.2](/images/9.Delete/9.2.png)

- Thực hiện tương tự với **tablecloudpos-frontend**.

### Dọn dẹp EC2 Instance
Truy cập vào **EC2 Console**.
= Chọn **Instances**.
- Chọn Instances bạn cần terminate: `table-cloud-pos-server`
- Ấn nút **Instance state**.
- Chọn **Terminate (delete) instance**.
![alt text](/images/9.Delete/9.3.png)
- Xác nhận `delete` và ấn **Delete**.

### Dọn dẹp Database IInstance
Truy cập vàp **Aurora and RDS Console**.
= Chọn **Instances**.
- Chọn Instances bạn cần delete: `table-cloud-pos-rds-instance`.
- Ấn nút **Action**.
- Chọn **Delete**.
![alt text](/images/9.Delete/9.4.png)

Bảng xác nhận delete hiện lên.
{{% notice tip %}}
Khi xóa **RDS Instance** bạn sẽ cần xác nhận việc có **Create final snapshot** hay không? Vi đây là việc chụp một "bức ảnh" dữ liệu tại đúng thời điểm bạn bấm nút xóa. Bản sao lưu này là bản thủ công, nó sẽ tồn tại vĩnh viễn trong tài khoản của bạn cho đến khi bạn tự tay xóa nó đi. Đây là cách an toàn nhất để giữ lại dữ liệu lâu dài sau khi Instance đã biến mất.
{{% /notice %}}

{{% notice tip %}}
Khi xóa **RDS Instance** bạn sẽ cần xác nhận việc có **Retain automated backups** hay không? Thay vì xóa sạch lịch sử sao lưu tự động cùng với Instance, tùy chọn này giúp giữ lại các bản backup đó trong một vài ngày (thường là 7 ngày). Nó cho phép bạn quay ngược thời gian (Point-in-Time Recovery) về một thời điểm bất kỳ trước khi xóa, nhưng chỉ có hiệu lực trong thời gian ngắn hạn.
{{% /notice %}}

- Tuy nhiên trong workshop này chúng ta sẽ **xóa hết** nên chỉ cần xác nhận `delete me` và ấn **Delete**. 
![9.5](/images/9.Delete/9.5.png)


### Dọn dẹp Subnet Group
Truy cập vào **Aurora and RDS Console**.
- Chọn **Subnet Group**.
- Chọn Subnet của Database Instance: `table-cloud-pos-db`.
- Ấn nút **Delete**. 
![9.6](/images/9.Delete/9.6.png)

### Dọn dẹp Security Group
Truy cập **EC2 Console**:
- Chọn **Security Group**.
- Lần lượt chọn các SG để xóa: **table-cloud-sg-db** và **table-cloud-pos-sg-public**.
- Ấn nút **Action**.
- Chọn **Delete security groups**.
![9.7](/images/9.Delete/9.7.png)
![9.8](/images/9.Delete/9.8.png)

### Dọn dẹp IAM Role
Truy cập vào **IAM Console**:
- Chọn **Roles**.
- Chọn `CustomRWECRRole`.
- Ấn nút **Delete**.
![alt text](/images/9.Delete/9.9.png)