---
title: "Using ECR"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: "<b>8.1</b>"
---
### Creating an ECR Repository to Store Docker Images
Search for **Amazon Elastic Container Registry**.

- Select **Create**.

![8.1.1](../../../static/images/8.PushImage/8.1.1.png)

We will create **2 different repositories** to contain the **Docker Images**:

- Repository name: `tablecloudpos-frontend` and `tablecloudpos-backtend`
- Image tag mutability: select **Mutable**.

- Encryption configuration: leave as default.

![8.1.2](../../../static/images/8.PushImage/8.1.2.png)

![8.1.3](../../../static/images/8.PushImage/8.1.3.png)

The result you get is a **repository** containing two different **Docker Images**.

![8.1.4](../../../static/images/8.PushImage/8.1.4.png)

{{% notice tip %}}
We need to create a separate repository for each application to manage Docker image versions more easily, especially for implementing [CI/CD](https://aws.amazon.com/vi/what-is/ci-cd-pipeline/) later.

{{% /notice %}}

### Install AWS CLI
By default (October 15, 2024), AWS CLI is not installed by default in Ubuntu. First, we need to download the **unzip**: `sudo apt install unzip`
![8.1.5](../../../static/images/8.PushImage/8.1.5.png)

Then we will use the commands below to install AWS CLI.

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

### Push Docker Images to Repository
To push the Docker Image of the **frontend** to ECR (similarly for the **backend**). - First, go back to the **ECR Console**.

- Select `tablecloudpos-frontend` (If it's a backend: select `tablecloudpos-backend`).
- Press the **View push commands** button.
![8.1.6](../../../static/images/8.PushImage/8.1.6.png)

- A dialog box will then pop up, and we can see a series of commands.

![8.1.7](../../../static/images/8.PushImage/8.1.7.png)

Returning to the EC2 Instance, we need to use the Root User to log into ECR with Docker.

- In the AWS console of **Push commands for tablecloudpos-frontend**

- Select the first command to authenticate logging into the **Amazon Elastic Container Registry** (ECR) from your **Docker local** environment. Beforehand, make sure you have configured **AWS Configure**.

{{% notice tip %}}
Because when a user uses sudo to log into ECR with Docker, the credentials are stored in that user's HOME directory. But when performing a push or pull command, it will look for the credentials in the Root directory instead of the HOME directory that was saved during the previous login.

{{% /notice %}}

In the previous sections, we created images for each application, so now we just need to tag them appropriately and push them to the corresponding **Registry**.

In the AWS console for **Push commands for tablecloudpos-frontend**:

- Select the third command to perform tagging, replacing the resource image names you created earlier.

{{% notice tip %}}
General format `<Account_ID>.dkr.ecr.<region>.amazonaws.com/<Repository_Name>:<Name_tag>`
{{% /notice %}}

After creation, proceed to push the **Image** to **ECR**.

- In the AWS console for **Push commands for tablecloudpos-frontend**:

- Select the `push` command.

Proceed similarly with the **Image** of the **backend**. Remember to copy the login command. But log out first.

### Results
After the push is complete, we can see the images that have been pushed to each **repository**.

![8.1.8](/images/8.PushImage/8.1.8.png)