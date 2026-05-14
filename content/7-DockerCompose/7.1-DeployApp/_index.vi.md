---
title : "Triển khai ứng dụng"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 7.1 </b> "
---
### Triển khai với Docker Compose
Trước khi triển khai với **Docker Compose**, thì chúng ta dừng lại 2 Docker Containers (`Ctrl + C`) vừa rồi đã chạy.
- Chạy lệnh: `sudo docker compose -f docker-compose.app.yaml up`
  - `sudo`: Chạy câu lệnh với quyền quản trị cao nhất (root). Điều này cần thiết vì Docker thường yêu cầu quyền hệ thống để quản lý các tài nguyên như mạng (network) và container.
  - `docker compose`: Đây là công cụ giúp bạn định nghĩa và vận hành ứng dụng gồm nhiều container (như Frontend, Backend, Database) cùng một lúc dựa trên một file cấu hình.
  - `-f docker-compose.app.yaml`:
    - `-f` là viết tắt của file.
    - Mặc định, Docker Compose sẽ tìm file có tên là **docker-compose.yaml**.
    - Tuy nhiên, vì file của bạn có tên riêng là **docker-compose.app.yaml**, bạn phải dùng tham số `-f` để chỉ định chính xác file mà **Docker** cần đọc.

Khi bạn nhấn **Enter**, **Docker Compose**s ẽ thực hiện các bước sau:
- Đọc file: Kiểm tra nội dung **docker-compose.app.yaml** để biết có bao nhiêu dịch vụ cần chạy.
- Tạo hạ tầng: Tự động tạo **Network** (như `my-network`) để các **container** giao tiếp với nhau mà bạn không cần gõ lệnh create network thủ công.
- Build/Pull Image: Nếu image chưa có sẵn hoặc có thay đổi trong code, nó sẽ tự động build lại.
- Khởi tạo Container: Chạy Backend và Frontend theo đúng thứ tự (ví dụ: chạy Backend trước nếu có thiết lập depends_on).
- up: Lệnh này yêu cầu Docker thực hiện một chuỗi hành động: đọc file cấu hình, tạo mạng, build/tải image và khởi chạy tất cả các dịch vụ (services) được định nghĩa trong file đó.

File **docker-compose.app.yaml** của dự án được triển khai như sau:
```yaml
version: "3"
services:
  nginx:
    restart: always
    depends_on:
      - backend
      - frontend
    build:
      dockerfile: Dockerfile
      context: ./nginx
    ports:
      - "3000:80"
  backend:
    env_file:
      - path: "./docker-compose-env/backend.app.env"
    build:
      dockerfile: Dockerfile
      context: backend
    volumes:
      - /app/node_modules
      - ./backend:/app
    ports:
      - "5000:5000"
  frontend:
    stdin_open: true
    build:
      dockerfile: Dockerfile
      context: ./frontend
    volumes:
      - /app/node_modules
      - ./frontend:/app
```

![7.1.1](/images/7.DockerCompose/7.1.1.png).

Ok vậy là ứng dụng của chúng ta có vẻ như đã hoạt động được, ở bước sau thì tiến hành kiểm tra ứng dụng.