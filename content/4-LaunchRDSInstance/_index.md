---
title : "Launching an RDS Instance"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 4. </b> "
---
### RDS Overview
Amazon RDS (Relational Database Service) is a managed database service on AWS. We manage the database at the RDBMS level, while AWS handles the underlying operating system access and management. Supported engines include Aurora, MySQL, PostgreSQL, MSSQL, Oracle, and MariaDB[cite: 1]. Amazon RDS offers the following features[cite: 1]:

- **Automated Backups**: Supports both transaction logs and database backups for up to 35 days[cite: 1].
- **Read Replicas**: Provides read-only copies to handle heavy read workloads (such as reporting)[cite: 1].
- **Promotion**: Read Replicas can be promoted to a standalone Primary node[cite: 1].
- **Multi-AZ Deployment**: Operates with an automatic failover mechanism (Primary/Standby) for high availability[cite: 1].
- **OLTP Focused**: Typically used for Online Transactional Processing (OLTP) applications[cite: 1].
- **Encryption**: Provides data encryption both at rest and in transit[cite: 1].
- **Network Security**: Protected by firewall features similar to EC2, including Security Groups and NACLs[cite: 1].
- **Scalability**: Easily modify the instance size to scale compute resources[cite: 1].
- **Storage Auto Scaling**: Automatically increases storage capacity as data grows[cite: 1].

### Content
1. [Create a DB Subnet Group]()
2. [Launch an RDS Instance]()