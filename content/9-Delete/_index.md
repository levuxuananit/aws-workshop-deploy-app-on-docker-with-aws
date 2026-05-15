---
title: "Clean up resources"
date: "`r Sys.Date()`"
weight: 9
chapter: false
pre: " <b> 9. </b> "
---
### Cleaning up the Elastic Container Registry

On the AWS Console interface:

- Search for and select **Elastic Container Registry**.

- Select **Repositories**.

- Select **tablecloudpos-backend**.

- Click **Delete**.

![9.1](/images/9.Delete/9.1.png)

- Type `delete`.

- Click **Delete**.

![9.2](/images/9.Delete/9.2.png)

- Do the same for **tablecloudpos-frontend**.

### Cleaning up EC2 Instance
Access the **EC2 Console**.

= Select **Instances**.

- Select the instance you want to terminate: `table-cloud-pos-server`
- Press the **Instance state** button.

- Select **Terminate (delete) instance**.

![alt text](/images/9.Delete/9.3.png)

- Confirm `delete` and press **Delete**.

### Cleaning up Database Instance
Access the **Aurora and RDS Console**.

= Select **Instances**.

- Select the instance you want to delete: `table-cloud-pos-rds-instance`.

- Press the **Action** button.

- Select **Delete**.

![alt text](/images/9.Delete/9.4.png)

A delete confirmation window will appear.

{{% notice tip %}}
When deleting an **RDS Instance**, you will need to confirm whether or not to **Create final snapshot**. This is like taking a "picture" of the data at the exact moment you click the delete button. This backup is manual and will remain permanently in your account until you manually delete it. This is the safest way to retain data long-term after the Instance is gone.

{{% /notice %}}

{{% notice tip %}}
When deleting an **RDS Instance**, you will need to confirm whether you have **Retain automated backups**. Instead of completely erasing the automatic backup history along with the Instance, this option keeps those backups for a few days (usually 7 days). It allows you to go back in time (Point-in-Time Recovery) to any point before deletion, but this is only effective for a short period.

{{% /notice %}}

- However, in this workshop we will **delete everything**, so just confirm `delete me` and press **Delete**.

![9.5](/images/9.Delete/9.5.png)

### Cleaning up Subnet Groups
Access the **Aurora and RDS Console**.

- Select **Subnet Group**.

- Select the Subnet of the Database Instance: `table-cloud-pos-db`.

- Press the **Delete** button.

![9.6](/images/9.Delete/9.6.png)

### Cleaning up Security Groups
Access the **EC2 Console**:

- Select **Security Group**.

- Select the SGs to delete in turn: **table-cloud-sg-db** and **table-cloud-pos-sg-public**.

- Press the **Action** button.

- Select **Delete security groups**.

![9.7](/images/9.Delete/9.7.png)

![9.8](/images/9.Delete/9.8.png)

### Cleaning up IAM Roles
Access the **IAM Console**:

- Select **Roles**.

- Select `CustomRWECRRole`.

- Press the **Delete** button.

![alt text](/images/9.Delete/9.9.png)