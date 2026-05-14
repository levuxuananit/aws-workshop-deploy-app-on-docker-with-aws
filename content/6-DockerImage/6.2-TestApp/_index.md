---
title : "Environment and Source Code Preparation on EC2"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 5.2 </b> "
---
### System Update and Connection
First, use the Secure Shell (SSH) protocol to access your EC2 Instance.
- In **VSCode**, to SSH to EC2 on AWS, you can install the `Remote-SSH` extension.
- Once installed, click the **><** icon at the bottom left of the screen to open the connection mode.
- Select **Connect to host...**
- Next, you can choose one of the following two options:
  - **+Add New SSH Host...**: Paste the command `ssh -i "C/Users/Legion/Downloads/pos-key.pem" ubuntu@18.143.134.165` where:
    - Copy the SSH command by: selecting the **EC2 Instance** you want to connect to, selecting **Connect**, choosing **SSH client**, and copying the command.
    - SSH command structure: **ssh -i "`path-to-key.pem-on-your-machine`" `username`@`Public-IP`**
![5.2.1](/images/5.EC2Config/5.2.2.png)
![5.2.2](/images/5.EC2Config/5.2.1.png)
  - **Configure SSH Hosts...**: Select the **config file** on your machine and configure it as shown in the template below:

  ```yaml
  Host table-cloud-pos-ec2                                # Host Name: table-cloud-pos-ec2
    HostName 18.143.134.165                               # Public-IP: 18.143.134.165
    User ubuntu                                           # username: ubuntu
    IdentityFile "C:/Users/Legion/Downloads/pos-key.pem"  # path to key.pem on your machine
    ```

- Select **table-cloud-pos-ec2** to connect to the EC2 Instance on AWS.
- Select **Linux**.
- A successful connection is confirmed when the host name you connected to appears in the bottom left corner.
![5.2.3](/images/5.EC2Config/5.2.3.png)

### System Update
Immediately after a successful login, the first task is to update the software package list to ensure the system is in its most stable and secure state.
- Enter the following commands into the terminal:
```bash
sudo apt update -y
sudo apt upgrade -y
```

![5.2.4](/images/5.EC2Config/5.2.4.png)

### Install Docker Engine
**Docker** is the core component for deploying applications as **Containers**. We will proceed with installing the official version from the **Docker Repository**.

Set up the GPG Key and Repository, and add Docker's official GPG key:
```bash
# Update the package list
sudo apt-get update
# Install necessary certificates and curl
sudo apt-get install ca-certificates curl
# Create a directory for the GPG keyrings
sudo install -m 0755 -d /etc/apt/keyrings
# Download Docker's official GPG key
sudo curl -fsSL [https://download.docker.com/linux/ubuntu/gpg](https://download.docker.com/linux/ubuntu/gpg) -o /etc/apt/keyrings/docker.asc
# Set read permissions for the GPG key
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

{{% notice tip %}}
Installing directly from the official Docker Repository ensures you have the latest version, optimized performance, and full support for Docker Compose V2.
{{% /notice %}}

Add the repository to Apt sources:

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

Install Docker components and Docker Compose:

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```

![5.2.6](/images/5.EC2Config/5.2.6.png)

### Install MySQL Client
To interact with, verify, and manage data on the remote Amazon RDS service, we need to install the MySQL Client tool.

```bash
sudo apt install mysql-client -y
```

![5.2.7](/images/5.EC2Config/5.2.7.png)

Verify Status and Clone Source Code
Before beginning deployment, ensure that all tools are correctly installed by checking their versions:
- Docker: `docker --version`
- MySQL Client: `mysql --version`
- Git: `git --version` (Usually pre-installed on Ubuntu 24.04).
![5.2.8](/images/5.EC2Config/5.2.8.png)
![5.2.9](/images/5.EC2Config/5.2.9.png)

Once everything is ready, proceed to download the project source code from GitHub to the server. Use the ls command to inspect the files inside.
```bash
git clone https://github.com/levuxuananit/aws-table-cloud-pos.git
ls
cd aws-table-cloud-pos
ls
```
![5.2.10](/images/5.EC2Config/5.2.10.png)

The environment setup is now complete, and the source code has been successfully prepared on your EC2 instance. You are ready to proceed with the next steps of the deployment.