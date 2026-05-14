---
title: "Deploying on Docker Compose"
date: "`r Sys.Date()`"
weight: 7
chapter: false
pre: "<b>7.</b>"
---
### Introduction
This is the most important "upgrade" step in the deployment process. Instead of running each `docker build` and `docker run` command for each service as in the previous section, we will use **Docker Compose** to manage the entire system with a single configuration file.

Below is the standard deployment method for a **Software & Cloud Engineer**:

### Contents
1. [Deploy Application](7-DockerCompose/7.1-DeployApp)
2. [Test Application](7-DockerCompose/7.2-TestApp)