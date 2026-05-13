---
title : "EC2 Configuration"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 5.1 </b> "
---
### Initialize and Configure EC2 Instance
In this step, we will set up a virtual server that will serve as the cloud environment for running the application.
- In the **AWS Management Console**.
- Search for and select the **EC2** service.
![5.1.1](/images/5.EC2Config/5.1.1.png)

In the **EC2 Dashboard** interface:
- Select **Instances**.
- Click the **Launch Instances** button to begin the initialization process.
![5.1.2](/images/5.EC2Config/5.1.2.png)

Set Server Parameters:
- **Name**: Name the server `table-cloud-pos-server`.
- **Application and OS Images (AMI)**: Select the **Ubuntu** operating system, version **Ubuntu Server 24.04 LTS**.
![5.1.3](/images/5.EC2Config/5.1.3.png)

- **Key pair (login)**: Select **Create new key pair**.
- **Key pair name**: `pos-key`.
- **Key pair type**: Select **RSA**.
- **Private key file format**: Select `.pem`.
- Click **Create key pair** and securely save the `.pem` file for future SSH access.
![5.1.4](/images/5.EC2Config/5.1.4.png)

- **Instance type**: Select `t3.medium` to ensure sufficient resources for running Docker.
![5.1.5](/images/5.EC2Config/5.1.5.png)

Edit Network and Security Settings:
- Click **Edit** in the **Network settings** section.
![5.1.6](/images/5.EC2Config/5.1.6.png)

Configuration Details:
- **VPC**: Select `table-cloud-pos-vpc`.
- **Subnet**: Select one of the Public Subnets from the lab setup.
- **Auto-assign public IP**: Ensure this is set to **Enable**.
- **Firewall (Security Groups)**: Select **Select existing security group**.
- **Common security groups**: Check **table-cloud-pos-sg-public**.
![5.1.7](/images/5.EC2Config/5.1.7.png)

Finalize Initialization:
Review the parameters and click **Launch instance**.

### Assign IAM Role for ECR Access to EC2
To allow the EC2 instance to interact securely with the container registry (ECR) without manual Access Key configuration, we need to attach the previously created Role.

In the Instances list interface, find and select the `table-cloud-pos-server` you just launched.
- Click the **Actions** button at the top.
- Navigate to **Security** and select **Modify IAM role**.
![5.1.8](/images/5.EC2Config/5.1.8.png)

### Update Permissions
In the **IAM role** section:
- Search for and select the correct Role: `CustomRWECRRole`.
- Click **Update IAM role** to apply the changes.
![5.1.9](/images/5.EC2Config/5.1.9.png)

### Summary
Your server is now secured by a **Key Pair**, resides within a secure VPC network zone, and possesses an IAM Role "credential" ready to push/pull **Docker Images** from **Amazon ECR**.