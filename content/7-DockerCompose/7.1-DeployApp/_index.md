---
title: "Deploying the Application"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: "<b>7.1</b>"
---
### Deployment with Docker Compose
Before deploying with **Docker Compose**, let's stop the two Docker Containers (`Ctrl + C`) that were just running.

- Run the command: `sudo docker compose -f docker-compose.app.yaml up`

- `sudo`: Runs the command with the highest administrative privileges (root). This is necessary because Docker often requires system privileges to manage resources such as networks and containers.

- `docker compose`: This is a tool that helps you define and run applications consisting of multiple containers (such as Frontend, Backend, Database) at the same time based on a single configuration file.

- `-f docker-compose.app.yaml`:

- `-f` is an abbreviation for file.

- By default, Docker Compose will look for a file named **docker-compose.yaml**.

- However, since your file has a unique name, **docker-compose.app.yaml**, you must use the `-f` parameter to specify the exact file that Docker needs to read.

When you press Enter, Docker Compose will perform the following steps:

- Read file: Checks the contents of **docker-compose.app.yaml** to determine how many services need to run.

- Create infrastructure: Automatically creates a **Network** (like `my-network`) so that the **containers** can communicate with each other without you having to manually type the `create network` command.

- Build/Pull Image: If the image is not available or there are changes in the code, it will automatically rebuild it.

- Initialize Container: Run the Backend and Frontend in the correct order (e.g., run the Backend first if there is a `depends_on` setting).

- up: This command instructs Docker to perform a series of actions: read the configuration file, create the network, build/load the image, and launch all the services defined in that file.

The project's **docker-compose.app.yaml** file is deployed as follows:
```yaml
version: "3"
services: 
nginx: 
restart: always 
depends_on: 
- backend 
- frontend 
build: 
dockerfile: Dockerfile 
context: ./nginx 
ports: 
- "3000:80" 
backend: 
env_file: 
- path: "./docker-compose-env/backend.app.env" 
build: 
dockerfile: Dockerfile 
context: backend 
volumes: 
- /app/node_modules 
- ./backend:/app 
ports: 
- "5000:5000" 
frontend: 
stdin_open: true 
build: 
dockerfile: Dockerfile 
context: ./frontend 
volumes: 
- /app/node_modules 
- ./frontend:/app
```

![7.1.1](/images/7.DockerCompose/7.1.1.png).

Okay, so our application seems to be working. In the next step, we'll test the application.