---
title : "Triển khai ứng dụng"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2.2 </b> "
---
### Tải mã nguồn
Clone mã nguồn của ứng dụng từ trên Github về máy
```bash
git clone https://github.com/levuxuananit/aws-table-cloud-pos.git
```

### Thêm dữ liệu
Vào trong thư mục `database` và sao chép đường dẫn ở trên thanh Browse của window. Dán đường dẫn vào trong **MySQL Shell**, thêm tên của script `init.sql` vào trong chuỗi mới dán vào.
![2.2.1](/images/2.local/2.2.1.png)

Thực hiện một số truy vấn để kiểm tra
```sql
SELECT * FROM Clients;
```
![2.2.2](/images/2.local/2.2.2.png)

### Triển khai Web Server
Vào trong thư mục `backend` sửa đổi username, password của bạn trong file `.env`.
```yaml
# Change these information
MYSQL_USER=root
MYSQL_PASSWORD=P@ssw0rd
MYSQL_DATABASE=tablecloudpos

# Change this host
DB_HOST=localhost

DB_DIALECT=mysql
NODE_ENV=development
PORT=5000
JWT_SECRET=0bac010eca699c25c8f62ba86e319c2305beb94641b859c32518cb854addb5f4
```

Sau đó là mở Terminal trong thư mục `backend`, tiến hành cài đặt các **NPM packages** để chạy server `npm install`

Sau đó là khởi chạy server `npm run dev`

### Triển khai Client Application
Mở Terminal trong thư mục `frontend` và cài đặt các **NPM Packages** `npm install`

Sau đó là khởi chạy server `npm run dev`

### Kết luận sau khi triển khai trên local
Sau khi hoàn tất quy trình triển khai thủ công, chúng ta có thể nhận thấy 4 thách thức lớn đối với môi trường thực tế:

- **High Overhead**: Quy trình triển khai thủ công phức tạp, tốn thời gian và đòi hỏi phải cài đặt quá nhiều phụ thuộc (Dependencies) rời rạc.

- **Platform Dependency**: Ứng dụng chạy trên Windows gây khó khăn cho việc di chuyển (Portability) sang các nền tảng khác (như Linux Server) do sự khác biệt về môi trường hệ thống.

- **Low Reliability**: Kiến trúc hiện tại thiếu tính ổn định và không đảm bảo khả năng sẵn sàng cao (High Availability) cho các hệ thống thực tế.

- **Resource Conflict & Isolation**: Các ứng dụng dùng chung tài nguyên hệ thống mà không có sự cô lập (Isolation). Lỗi từ một phần mềm bên thứ ba hoặc xung đột thư viện có thể trực tiếp làm sập toàn bộ ứng dụng của bạn.
  
{{% notice tip %}}
**Giải pháp**: Để khắc phục triệt để các vấn đề trên, trong phần tiếp theo chúng ta sẽ sử dụng Linux và Docker để chuẩn hóa môi trường, cô lập tài nguyên và tự động hóa quy trình vận hành.
{{% /notice %}}
