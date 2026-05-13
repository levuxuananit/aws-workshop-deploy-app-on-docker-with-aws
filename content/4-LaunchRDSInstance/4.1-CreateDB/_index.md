---
title : "Creating a DB Subnet Group"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 4.1 </b> "
---
### Create a DB Subnet Group in Amazon RDS 
Setting up a **DB Subnet Group** is a crucial first step in defining the network space and ensuring centralized management for database resources within a VPC.

Access the **Amazon RDS** service on the **AWS Management Console**. Use the search bar to navigate to the `Amazon RDS` dashboard:
- Navigate to **Subnet groups** in the feature list on the left.
- Click **Create DB subnet group**.
![4.1.1](/images/4-LaunchRDSInstance/4.1.1.png)

Set Basic Identification Parameters:
- **Name**: `table-cloud-pos-db`
- **Description**: `Subnet Group for Order Management`
- **VPC**: Select `table-cloud-pos-vpc`

Allocate Subnet Resources:
- Select the **Availability Zones** (AZs) corresponding to your deployed infrastructure.
- Then, specify **02 Private Subnets** so the system can assign internal IP addresses to the database.
![4.1.2](/images/4-LaunchRDSInstance/4.1.2.png)

Review and Finalize Initialization:
- Review the list of selected subnets to ensure technical accuracy.
- Click **Create** to save the configuration.

{{% notice tip %}}
**Pro Tip**: Integrating multiple **Availability Zones** into a single **Subnet Group** is a prerequisite for deploying a **Multi-AZ architecture**, allowing your database to automatically maintain operations even if a data center encounters an issue.
{{% /notice %}}

{{% notice tip %}}
**Security Note**: Always prioritize placing **RDS Instances** within **Private Subnets** to completely isolate resources from the Internet, allowing only internal access to maximize data security.
{{% /notice %}}

Once the process is complete, the new **DB Subnet Group** will appear with an **Available** status in the control list.