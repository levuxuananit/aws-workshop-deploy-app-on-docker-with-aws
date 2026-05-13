---
title : "Launching an RDS Instance"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 4.2 </b> "
---
### Create RDS Instance
Navigate to the **Aurora and RDS** management page. From the left navigation bar:
- Select **Databases**.
- Click **Create Database**.
- Select **Standard create**.
![4.2.1](/images/4-LaunchRDSInstance/4.2.1.png)

On the **Create database** page:
- **Engine type**: Select **MySQL**.
- **Creation method**: Select **Standard create**.
- **Templates**: Select **Dev/Test**.
![4.2.2](/images/4-LaunchRDSInstance/4.2.2.png)

In the **Deployment options** section:
- Select: **Multi-AZ DB deployment (2 instances)**.
![4.2.3](/images/4-LaunchRDSInstance/4.2.3.png)

{{% notice tip %}}
The **Multi-AZ DB deployment (2 instances)** option is used to ensure **High Availability** and automated recovery for the system. 

Specifically, AWS maintains a standby replica in a different Availability Zone and automatically performs a **failover** (re-routing connections) if the primary instance fails. This minimizes downtime without requiring changes to the application configuration.
{{% /notice %}}

- **DB instance identifier**: `table-cloud-pos-rds-instance`
- **Master username**: `admin`
- **Master password**: `tablecloudpos2026`
![4.2.4](/images/4-LaunchRDSInstance/4.2.4.png)

- Select **Standard Classes (includes m classes)**.
- **Instance configuration**: Select **db.m6gd.large (supports Amazon RDS Optimized Writes)**.
![4.2.5](/images/4-LaunchRDSInstance/4.2.5.png)

- **Connectivity**: Select **Don't connect to an EC2 compute resource**.
- **Virtual Private Cloud (VPC)**: Select `table-cloud-pos-vpc`.
- **DB Subnet group**: Select `table-cloud-pos-db`.
- **Public access**: Select **No**.
![4.2.6](/images/4-LaunchRDSInstance/4.2.6.png)

- **Existing VPC security groups**: Select the DB security group created earlier: `table-cloud-pos-sg`.
- **Certificate authority**: Select the default certificate **rds-ca-rsa2048-1**.
![4.2.7](/images/4-LaunchRDSInstance/4.2.7.png)

- Review all configurations carefully and click **Create database**.
- The initialization process is complete. It typically takes about 15 minutes for the status to show as **Available**.