---
title : "Introduction"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---
This workshop provides a comprehensive guide to the end-to-end process of containerizing and operating applications using Docker. You will gain hands-on experience managing the application lifecycle through core services: Docker Hub, Nginx, Amazon ECR, Amazon RDS, and Amazon EC2.
![cloud_docker_architect](/images/arc/cloud_docker_architect.png)

### Core Services
- **Docker Hub**: A public registry used to store and share Docker images.
- **Nginx**: Functions as a Reverse Proxy and Load Balancer to optimize traffic distribution and scalability.
- **Amazon Elastic Container Registry (Amazon ECR)**: A secure, fully-managed private registry on AWS, deeply integrated for image management and deployment.
- **Amazon Relational Database Service (Amazon RDS)**: A managed database service that automates operations and ensures data security.
- **Amazon Elastic Compute Cloud (Amazon EC2)**: Virtual server infrastructure (Compute) used to run Docker containers.

### Operational Workflow
- **Traffic Ingress**: Client requests are sent over the Internet, passing through the Internet Gateway to enter the AWS VPC environment.

- **Reverse Proxy & Routing**: Nginx receives the traffic and acts as a Reverse Proxy, routing requests to the appropriate containers: Backend and Frontend containers.

- **App Logic & Data Processing**:
  - The Frontend (React) sends requests to the Backend (Node.js) for business logic processing.
  - The Backend (Node.js) executes CRUD queries with Amazon RDS.
  - After processing, data is sent back (Response) via the reverse flow: **Backend → Nginx → Client**.

- **CI/CD & Image Management**:
  - When the source code (React/Node.js) is updated, new Docker images are built and pushed to Docker Hub or Amazon ECR.
  - From these registries, the application is deployed or updated directly onto Amazon EC2 instances.

{{% notice note %}}
Always verify **Security Groups** configurations to ensure seamless connectivity between Nginx, the Backend, and Amazon RDS.
{{% /notice %}}