# WORKSHOP DEPLOYING DOCKERIZED APPS ON AWS

Master the end-to-end process of containerizing and deploying a fullstack application (React & Node.js) on AWS infrastructure.

---

### Core Services
- **Docker Hub / Amazon ECR**: Public and Private registries for managing Docker Images.
- **Nginx**: Functions as a Reverse Proxy and Load Balancer for efficient traffic routing.
- **Amazon RDS**: Managed relational database for automated maintenance and high security.
- **Amazon EC2**: Scalable compute instances to host and run your containers.

---

### System Architecture
- **Ingress**: Client Requests enter the VPC via the Internet Gateway.
- **Routing**: Nginx proxies traffic to either the Frontend (React) or Backend (Node.js) containers.
- **Data**: The Backend performs CRUD operations on Amazon RDS and returns the Response through Nginx.
- **CI/CD**: New Images are Pushed to ECR/Docker Hub and Deployed onto EC2 instances.

---

### Quick Notes
- **Best Practice**: For production, leverage Amazon ECS or EKS for advanced orchestration.
- **Security**: Configure Security Groups strictly to authorize traffic between Nginx, Backend, and RDS.
- **Cost**: Use the AWS Billing Dashboard and perform a Cleanup of all resources after the workshop to avoid unnecessary charges.

---