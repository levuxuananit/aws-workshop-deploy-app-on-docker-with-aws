---
title: "Push Image"
date: "`r Sys.Date()`"
weight: 8
chapter: false
pre: "<b> 8. </b> "
---
### Push Docker Image to Amazon ECR
**Amazon Elastic Container Registry** (ECR) is a service for managing **Docker container images** integrated with Amazon Web Services (AWS). Pushing images to ECR is a crucial part of the **container** deployment process on AWS, helping to store **images** in a secure environment and easily integrate with other services such as **ECS** (Elastic Container Service) or **EKS** (Elastic Kubernetes Service).

### Push Docker Image to Docker Hub
**Docker Hub** is a popular and publicly accessible **container registry** that allows developers to store and distribute Docker images worldwide. When you push an image to Docker Hub, it makes it easy to share your containerized application with the community, other development teams, or for personal use.
![docker_images](/images/arc/docker_images.png)

### Contents
1. [Using ECR](8-PushImage/8.1-UsingECR)
2. [Using Docker Hub](8-PushImage/8.2-UsingDockerHub)