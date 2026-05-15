---
title : "Push Image"
date :  "`r Sys.Date()`" 
weight : 8 
chapter : false
pre : " <b> 8. </b> "
---
### Push Docker Image lên Amazon ECR
**Amazon Elastic Container Registry** (ECR) là một dịch vụ quản lý **Docker container images** được tích hợp với Amazon Web Services (AWS). Quá trình push image lên ECR là một phần quan trọng trong quy trình triển khai **container** trên AWS, giúp lưu trữ các **image** trong môi trường an toàn và dễ dàng tích hợp với các dịch vụ khác như **ECS** (Elastic Container Service) hoặc **EKS** (Elastic Kubernetes Service). 

### Push Docker Image lên Docker Hub
**Docker Hub** là một **registry container** phổ biến và công khai cho phép các nhà phát triển lưu trữ và phân phối Docker images trên toàn thế giới. Khi bạn push image lên Docker Hub, điều này giúp bạn dễ dàng chia sẻ ứng dụng container của mình với cộng đồng, các nhóm phát triển khác, hoặc cho mục đích sử dụng cá nhân.
![docker_images](/images/arc/docker_images.png)

### Nội dung
1. [Sử dụng ECR](8-PushImage/8.1-UsingECR)
2. [Sử dụng Docker Hub](8-PushImage/8.2-UsingDockerHub)