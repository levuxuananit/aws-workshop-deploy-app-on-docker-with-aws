---
title : "Local Deployment"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---
Why should we containerize applications with **Docker Container** instead of running them directly on a local operating system?

For an application to operate reliably and smoothly handle user requests (CRUD operations), it must consume hardware resources from the host server. However, traditional deployment often leads to the "it works on my machine" syndrome due to environment discrepancies.

In this section, we will deploy a sample application directly on your machine to observe how Docker effectively resolves environment conflicts and optimizes resource management.

### Content
1. [Environment Setup](2-Local/2.1-Setup)
2. [Application Deployment](2-Local/2.2-Deploy)
3. [Testing the Application](2-Local/2.3-Testing)