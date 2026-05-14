---
title: "Deploying the application"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: "<b>6.2</b>"
---
### Copying the EC2 Instance's Public IPv4
Back in the EC2 Console, we need to copy the EC2 **Public IPv4** that we just worked on, then add the following URL to your browser: `http://public-dns-of-your-ec2:3000`
![6.2.1](/images/6-DockerImage/6.2.1.png)

### Testing the application
At this point, the application is running stably with **CRUD** functionality, and the **backend** can retrieve data from the **database** (Amazon RDS) and display it fully on the **frontend**.

![6.2.2](/images/6-DockerImage/6.2.2.png)
![6.2.3](/images/6-DockerImage/6.2.3.png)
![6.2.4](/images/6-DockerImage/6.2.4.png)
![6.2.5](/images/6-DockerImage/6.2.5.png)