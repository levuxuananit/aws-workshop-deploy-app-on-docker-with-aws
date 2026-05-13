---
title : "VPC Configuration"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 3.1 </b> "
---
### Create VPC
In the **AWS Management Console**:
- Search for the **VPC** service in the search bar and select the corresponding result.
- Select the **Region** `ap-southeast-1` (Singapore) to minimize latency.
- In the left navigation pane, select **Your VPCs**.
- Click the **Create VPC** button.
![3.1](/images/3.preparation/3.1.png)

On the VPC configuration page:
- Under **Resources to create**, select the **VPC and more** option.
![3.2](/images/3.preparation/3.2.png)

- Under **Name tag auto-generation**, enter the name: `table-cloud-pos`
![3.3](/images/3.preparation/3.3.png)

- For **VPC endpoints**, select **None** to optimize costs and simplify the configuration.
![3.4](/images/3.preparation/3.4.png)

- Review the settings and click **Create VPC**.

- VPC created successfully.
![3.5](/images/3.preparation/3.5.png)

### Configure Public Subnets
After creating the VPC, we need to configure the public subnets to automatically assign public IP addresses to the resources launched within them.

In the VPC management interface:
- In the left navigation pane, scroll down to the **Virtual private cloud** section and select **Subnets**.
- In the search bar, enter the keyword `table-cloud-pos` to filter the relevant subnets.
![3.6](/images/3.preparation/3.6.png)

Configure **Public Subnet 1**:
- Find and select the subnet named: `table-cloud-pos-subnet-public1-ap-southeast-1a`
- Click the **Actions** button at the top right of the interface.
- Select **Edit subnet settings**.
![3.7](/images/3.preparation/3.7.png)

In the configuration panel, locate the **Auto-assign IP settings** section:
- Check the box **Enable auto-assign public IPv4 address**.
- Scroll to the bottom and click **Save** to apply the changes.
![3.8](/images/3.preparation/3.8.png)

Repeat the process for **Public Subnet 2**:
- Find and select the subnet named: `table-cloud-pos-subnet-public2-ap-southeast-1b`
- Click the **Actions** button at the top right of the interface.
- Select **Edit subnet settings**.
  
In the configuration panel, locate the **Auto-assign IP settings** section:
- Check the box **Enable auto-assign public IPv4 address**.
- Scroll to the bottom and click **Save** to apply the changes.
![3.8](/images/3.preparation/3.8.png)

You have completed the VPC configuration and enabled **Auto-assign Public IPv4** for the Public Subnets. Now, any resource (such as an EC2 Instance) deployed into these subnets will have a public IP address by default to communicate with the Internet.