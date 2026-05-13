---
title : "Creating IAM Roles for ECR Access"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 3.3 </b> "
---
### Create IAM Policies for ECR
We will create two separate **Policies**: one for reading (Pull) and one for writing (Push) data to the **container repository**.

#### Create Policy: ReadECRRepositoryContent (Read Access)
In the **IAM (Identity and Access Management)** console:
- In the left navigation pane, select **Policies** and click **Create policy**.
![3.12](/static/images/3.preparation/3.12.png)

In the **Policy editor**:
- Select the service: **Elastic Container Registry**.
- Click **Next**. 
![3.13](/static/images/3.preparation/3.13.png)

Configure Actions:
- **List group**: Select `DescribeImages` and `ListImages`.
- **Read group**: Select `BatchGetImage`, `DescribeRepositories`, `GetAccountSettings`, and `GetAuthorizationToken`.
![3.14](/static/images/3.preparation/3.14.png)

- **Resources section**: Select **Specific**, then check **Any in this account** (to allow access to all repositories within this account).
- Click **Next**.
![3.15](/static/images/3.preparation/3.15.png)

Finalize Policy Details:
- **Policy name**: `ReadECRRepositoryContent`
- **Description**: `Allow pull images and describe repositories`.
- Click **Create policy**.
![3.16](/static/images/3.preparation/3.16.png)

#### Create Policy: WriteECRRepositoryContent (Write Access)
In the **Policies** interface:
- Click **Create policy** again.
- Select the service: **Elastic Container Registry**.

Configure Actions:
- **Read group**: Select `BatchCheckLayerAvailability` and `GetAuthorizationToken`.
- **Write group**: Select `CompleteLayerUpload`, `InitiateLayerUpload`, `PutImage`, and `UploadLayerPart`.
![3.17](/static/images/3.preparation/3.17.png)

- **Resources section**: Select **Any in this account**.
- Click **Next**.
![3.18](/static/images/3.preparation/3.18.png)

Finalize Policy Details:
- **Policy name**: `WriteECRRepositoryContent`
- **Description**: `Allow push images to ECR`.
- Click **Create policy**.
![3.19](/static/images/3.preparation/3.19.png)

### Create IAM Role for EC2 Instance
With the policies created, we now need a **Role** to assign to the EC2 server. This allows the server to interact with ECR securely without requiring manual Access Keys.

In the **IAM** management console:
- In the left navigation pane, select **Roles**.
- Click the **Create role** button.

Set Trusted Entity:
- **Trusted entity type**: Select **AWS service**.
- **Service or use case**: Select **EC2**.
- Click **Next**.

Attach Policies:
- In the search box, set the **Filter by Type** to: `Customer managed`.
- Find and check both policies: `ReadECRRepositoryContent` and `WriteECRRepositoryContent`.
- Click **Next**.

Name and Finalize:
- **Role name**: `CustomRWECRRole`
- **Description**: `Custom Role for EC2 to Read and Write to ECR`.
- Review the attached policy list and click **Create role**.

### Summary
**Enhanced Security**: Instead of storing credentials directly on the EC2 server, we use an **IAM Role**. AWS automatically issues **Temporary Credentials** to the server, significantly reducing the risk of credential leakage.

**Principle of Least Privilege**: Splitting policies into Read and Write ensures tight control:
- Only servers responsible for building and pushing images are granted **Write** permissions.
- Production servers running the application only require **Read** permissions.