---
title: "Initializing Data for Amazon RDS"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: "<b>5.3</b>"
---
To enable the application to run and display information, we need to load the initial records into the Amazon RDS database using the SQL script file available in the source code.

### Preparing the SQL Script
First, we need to determine the absolute path of the `init.sql` file to execute correctly in the MySQL environment.

- Navigate to the **database** directory:
```bash
cd database
ls
```
Get the absolute path of the `init.sql` file
- Usually it will be: `/home/ubuntu/aws-table-cloud-pos/database/init.sql`.

- Copy this path:
```bash
echo $(pwd)/init.sql
```

![5.3.1](/images/5.EC2Config/5.3.1.png)

### Connecting to RDS Instance
Use the mysql-client tool in VSCode to establish a connection from EC2 to the database server.

- Get Endpoint information: Access the **RDS Console** interface, select the **Database Instance** you created, and copy the value in the **Connectivity & Security** section.

![5.3.2](/images/5.EC2Config/5.3.2.png)

- Enter the password you set when creating the RDS to log in.

![5.3.3](/images/5.EC2Config/5.3.3.png)

### Executing the Data Loading Script
After accessing the MySQL command-line interface, use the source command with the path copied in Step 1 to run the script:
```bash
source /home/ubuntu/aws-table-cloud-pos/database/init.sql
```
![5.3.4](/images/5.EC2Config/5.3.4.png)

### Checking and Confirming the Results
Ensure that the data has been successfully structured and imported using the following query statements:
- Check if the **tablecloudpos** database and **Clients** data exist:
```sql
SHOW DATABASES;

USE fcjresbar;

SELECT * FROM Clients;
```
![5.3.5](/images/5.EC2Config/5.3.5.png)

{{% notice tip %}}
Note: If you cannot connect, please check the Inbound Rules of the Security Group assigned to RDS. Ensure that port 3306 is open to the EC2 server's Security Group.
{{% /notice %}}