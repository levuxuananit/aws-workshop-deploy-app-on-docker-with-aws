---
title : "Testing the Application"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 2.3 </b> "
---
### Verification of Deployment
Access `http://localhost:5173`. You should see the following interface:

![2.3.1](/images/2.local/2.3.1.png)

### User Authentication
Use one of the following accounts to log in to the application:
**User**: `user@example.com` / `123456`.
**Admin**: `admin@example.com` / `123456`.

{{% notice tip %}}
In a real-world production environment, it is recommended to use **AWS IAM Identity Center** or **Amazon Cognito** for more secure authentication.
{{% /notice %}}

### Interface Testing
Confirm a successful login and verify the consistency of the displayed data. Then, navigate through different routes to ensure the system's navigation works smoothly.

![2.3.2](images/2.local/2.3.2.png)
![2.3.3](images/2.local/2.3.3.png)
![2.3.4](images/2.local/2.3.4.png)
![2.3.5](images/2.local/2.3.5.png)
![2.3.6](images/2.local/2.3.6.png)

### Preparing for AWS Deployment
A stable local operation is a critical milestone confirming that the source code is ready. In the next chapter, we will perform **Cloud Migration** to move the application to the **AWS Cloud**. By combining **Docker** with **Amazon ECS** (Elastic Container Service), you will master how to leverage **Auto-scaling** capabilities and centralized container management according to **Enterprise** standards.