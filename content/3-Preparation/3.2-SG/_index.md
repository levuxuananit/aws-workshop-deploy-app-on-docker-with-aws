---
title : "Security Group Configuration"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 3.2 </b> "
---
### Configure Security Group for EC2 Instances (Public Access)
This **Security Group** acts as a virtual firewall for Web or Application servers that need to communicate with the Internet.

In the **EC2** management console:
- In the left navigation pane, locate the **Network & Security** section.
- Select **Security Groups**.
- Click the **Create security group** button.
![3.9](/images/3.preparation/3.9.png)

Set Basic Information:
- **Security group name**: `table-cloud-pos-sg-public`
- **Description**: `SG for Table Cloud POS`
- **VPC**: Select `table-cloud-pos` (Ensure you select the VPC created in the previous step, not the default VPC).

Configure **Inbound rules**:
- Select **Add rule**.
- **Rule 1**: Type `SSH`, Source `Anywhere-IPv4` (0.0.0.0/0) — allows administrators to access the server remotely via command line.
- **Rule 2**: Type `HTTP`, Source `Anywhere-IPv4` (0.0.0.0/0) — allows users to access the website via standard web protocol.
- **Rule 3**: Type `HTTPS`, Source `Anywhere-IPv4` (0.0.0.0/0) — allows secure web access via SSL/TLS certificates.
- **Rule 4**: Type `Custom TCP`, Port range `3000`, Source `Anywhere-IPv4` (0.0.0.0/0) — opens a specific port for applications (e.g., Node.js or React) commonly running on port 3000.
![3.10](/images/3.preparation/3.10.png)

Leave **Outbound rules** as default so the server can freely download updates from the Internet. Click **Create security group**.

### Configure Security Group for Database Instances (Private Access)
This **Security Group** is designed to protect the database by only allowing access from internal servers, maximizing security.

In the **Security Groups** interface, click **Create security group** again.

Set Basic Information:
- **Security group name**: `table-cloud-sg-db`
- **Description**: `SG for Table Cloud POS database`
- **VPC**: Select `table-cloud-pos`

Configure **Inbound rules**:
- Select **Add rule**.
- **Type**: `MySQL/Aurora` (Default port 3306).
- **Source**: Instead of an IP address, search for and select the `table-cloud-pos-sg-public` security group itself.
- This rule only permits EC2 instances associated with the **table-cloud-pos-sg-public** group to connect to the Database. All access attempts from the public Internet will be completely blocked.
- **Outbound rules**: Leave as default.
- Click **Create security group**.
![3.11](/images/3.preparation/3.11.png)

You have successfully created a two-tier security architecture: a Web tier (Public SG) open to the Internet, and a Database tier (Private SG) open only to the Web tier. This is a standard security best practice on AWS.