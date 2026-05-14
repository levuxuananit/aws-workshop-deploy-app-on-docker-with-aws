---
title: "Deploying the Application"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: "<b>6.1</b>"
---
### Advantages of the Cloud-Native Model
In the previous Deploy on Local section, we manually deployed the Database Server, Web Server, and End User Application. This method revealed many limitations in dependency management and consistency. In this section, we will move the entire infrastructure to the Cloud using Docker.

Using Docker completely eliminates the worry of manual "download and install." As long as you master the basic concepts of Docker (especially Network), this part will become extremely simple.

- **Database**: In the previous step, we configured the Database with **Amazon RDS**. AWS has optimized all maintenance, availability, and data security issues, allowing us to focus entirely on packaging the application using Docker Images.

- **Environment**: If local deployment is considered the **development environment**, then using Docker on the cloud is the stepping stone to the **testing environment** (Staging) or **production**.

### Deploying the Web Server (Backend)
First, access the cloned **aws-table-cloud-pos** source code directory. In the **backend** directory, we need to configure the connection to the database on the cloud:
- In the **Terminal**, type the following command to open the `.env` file.

```bash
ls

cd backend

vim .env
```
![6.1.1](/images/6-DockerImage/6.1.1.png)

Update the **DB_HOST** variable with the Amazon RDS Endpoint that you initialized.

- Press the **i** key (short for Insert).

- The word **-- INSERT --** will appear in the bottom left corner of the terminal screen.

- You can now use the arrow keys to move and enter/delete data as usual.

- Move to the **DB_HOST** line and change its value to the RDS Endpoint as instructed.

![6.1.2](/images/6-DockerImage/6.1.2.png)

Exit and Save File
- After editing, follow these steps:

- Press the **Esc** key to exit **Insert** mode (the -- INSERT -- text will disappear).

- Type the command `:wq` and press **Enter**.

: : Start entering commands for Vim.

w : Write/Save.

q : Quit.

![6.1.3](/images/6-DockerImage/6.1.3.png)

### Packaging the Web Server into a Docker Image (Build Image)
Now our **web server** is ready to run. Next, proceed to package the application into a **Docker Image**
```bash
sudo docker build . -t backend-image
```
![6.1.4](/images/6-DockerImage/6.1.4.png)

Before starting to run the **Container** for the **web server**, we need to create a **network** for the containers in the environment to communicate with each other.

```bash
sudo docker network create my-network
```
Then proceed to run the **Docker Container** with the newly created **Docker Image**
```bash
sudo docker run -p 5000:5000 --network my-network --name backend backend-image
```
![6.1.5](/images/6-DockerImage/6.1.5.png)

### Deploying the Application (Frontend)
Now, open a new SSH Session to deploy the user interface. The steps are similar to the Backend section:
- Navigate to the `frontend` directory.

```bash
cd aws-table-cloud-pos
cd frontend
```

### Packaging the Application into a Docker Image (Build Image)
Enter the following command to package the **Application** into a **Docker Image**:
```bash
sudo docker build . -t frontend-image
```
![6.1.6](/images/6-DockerImage/6.1.6.png)

Then proceed to run the **Docker Container** with the newly created **Docker Image**. We will map **port 80** inside the container to **port 3000** so that users can access it:
```bash
sudo docker run -d -p 3000:80 --network my-network --name frontend frontend-image
```
![6.1.7](/images/6-DockerImage/6.1.7.png)

### Troubleshooting Version Errors
Specifically, for the project being deployed, Vite requires the Crypto Web API, which is only fully and stably supported from Node.js version **18 or 20 and above**. In your Docker Container environment, if your Node.js version is lower than this, you will receive an error like this:
![6.1.8](/images/6-DockerImage/6.1.8.png)

Solution:

- Access the **DockerFile** of the **frontend**

- Change FROM to `node-20-alpine` (upgrade to a higher version to ensure the **Crypto Web API** runs stably)
![6.1.9](/images/6-DockerImage/6.1.9.png)

![6.1.10](/images/6-DockerImage/6.1.10.png)

![6.1.11](/images/6-DockerImage/6.1.11.png)

### Summary

At this point, you have completed the transition from manual deployment to using **Docker Images** on the Cloud. You can see the process has become much more streamlined.

However, running the `docker run` command for each service is still quite disjointed. In the next section, we will upgrade to **Docker Compose** to manage the entire technology stack with just a single configuration file.

You will clearly see the difference between: **Deploy Local** vs. **Docker Image** vs. **Docker Compose**.