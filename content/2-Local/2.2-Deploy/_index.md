---
title : "Application Deployment"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2.2 </b> "
---
### Clone Source Code
Clone the application source code from GitHub to your local machine:
```bash
git clone https://github.com/levuxuananit/aws-table-cloud-pos.git
```

### Database Initialization
Navigate to the `database` directory and copy the file path from the Windows Explorer address bar. Paste this path into the **MySQL Shell**, and append the script name `init.sql` to the end of the string to execute it.
![2.2.1](/images/2.local/2.2.1.png)

Execute a few SQL queries to verify that the data has been imported correctly:
```sql
SELECT * FROM Clients;
```
![2.2.2](/images/2.local/2.2.2.png)

### Deploy the Web Server
Navigate to the `backend` directory and update your database credentials (username and password) in the `.env` file.

```yaml
# Change these information
MYSQL_USER=root
MYSQL_PASSWORD=P@ssw0rd
MYSQL_DATABASE=tablecloudpos

# Change this host
DB_HOST=localhost

DB_DIALECT=mysql
NODE_ENV=development
PORT=5000
JWT_SECRET=0bac010eca699c25c8f62ba86e319c2305beb94641b859c32518cb854addb5f4
```

Next, open the Terminal in the backend folder and install the required NPM packages: `npm install`.

Then, launch the server by running: `npm run dev`.

### Deploy the Client Application
Next, open the Terminal in the backend folder and install the required NPM packages: `npm install`.

Then, launch the server by running: `npm run dev`.

### Post-Deployment Summary (Local Environment)
After completing the manual deployment process, we can identify four major challenges for production environments:

- **High Overhead**: The manual deployment process is complex, time-consuming, and requires installing too many fragmented dependencies.

- **Platform Dependency**: Running applications on Windows makes portability to other platforms (such as Linux servers) difficult due to system environment discrepancies.

- **Low Reliability**: The current architecture lacks stability and cannot guarantee High Availability (HA) for real-world production systems.

- **Resource Conflict & Isolation**: Applications share system resources without proper isolation. A bug in third-party software or a library conflict can potentially crash your entire application.

{{% notice tip %}}
**The Solution**: To fully address these issues, in the next section, we will utilize Linux and Docker to standardize the environment, isolate resources, and automate operational workflows.
{{% /notice %}}