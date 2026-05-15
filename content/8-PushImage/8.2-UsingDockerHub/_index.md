---
title: "Using Docker Hub"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: "<b>8.2</b>"
---
### Creating a repository on Docker Hub
Go to the prepared **Docker Hub** and create a **repository** in it.

- Select **Create a Repository**
![8.2.1](/images/8.PushImage/8.2.1.png)

Configure the **frontend** repository:

- Enter the repository name: `tablecloudpos-frontend`
- Enter the description: `Frontend Image of Table Cloud POS`
- Select **public**.

- Check again and select **Create**.

![8.2.2](/images/8.PushImage/8.2.2.png)

Similarly, you configure the **backend** repository:

- Enter the repository name: `tablecloudpos-backend`
- Enter the description: `Backend Image of Table Cloud POS`
- Select **public**.

- Check again and select **Create**.

![8.2.3](/images/8.PushImage/8.2.3.png)

Complete creation of 2 **Repositories** to hold 2 **Images** of the **web server** and **application** on **Docker Hub**.

![8.2.4](/images/8.PushImage/8.2.4.png)

### Push Images to Repositories on Docker Hub
Now we are ready to push the **images** to each **repository**.

- Log out and log in to Docker Hub.

- Please log in with the correct username and password for the account you used to create the repositories in the previous step.

![8.2.5](/images/8.PushImage/8.2.5.png)

- Change the tags for the **backend image** and **frontend image**.

![8.2.6](/images/8.PushImage/8.2.6.png)

- Push the **backend image** and **frontend image** to Docker Hub.

![8.2.7](/images/8.PushImage/8.2.7.png)

### Results

After pushing, we can see that the images have been pushed to each **repository**.

![8.2.8](/images/8.PushImage/8.2.8.png)
![8.2.9](/images/8.PushImage/8.2.9.png)