# Static Website Deployment Guide  
Deploying a static website using **S3**, **Docker**, **ECR**, and **EC2**

This guide walks through the full workflow for generating a static site, containerising it, pushing the image to AWS ECR, and running it on an EC2 instance.

## Information

### What is S3?
Amazon S3 (Simple Storage Service) is AWS’s scalable object‑storage service used to store and retrieve any amount of data at any time. Instead of thinking in terms of folders on a server, S3 stores files as objects inside buckets.

**Key points**
- Object storage — stores files like HTML, CSS, JS, images, videos, logs, backups, etc.
- Highly durable — designed for 11 nines of durability (99.999999999%).
- Infinitely scalable — you never run out of space.
- Pay‑as‑you‑go — you only pay for what you store and transfer.
- Static website hosting — can serve HTML/CSS/JS directly over the web.
- Integrates with AWS services — CloudFront, EC2, Lambda, ECR, and more.

### What is ECR?

**Key points**

### What is Docker?

**Key points**

### What is EC2?

**Key points**

### What is Terraform?

**Key points**

---

## Steps to follow

### 1. Website Generation  
A lightweight static site is all you need for this deployment.

**Steps**  
Create a simple project structure:
> /site <br>
>   index.html <br>
>   styles.css <br>
>   script.js

- Use relative paths for all assets (e.g., `./images/logo.png`).
- Test locally by opening `index.html` in your browser.
- Confirm the site works without any backend dependencies.

---
## 2. Deployment file  
This section will give some quick details on getting started with the deployment file for the project.

![BeginningStepsOfDeploy](./assets/Deploy1.png)
*Figure 1: Intial Setup*

- name: *your_deployment_name* - Sets the name of the deployment workflow. This will be presented within the actions tab in github.
- 
- 
- 
---

## 3. Docker Containerisation  
Package your static site into a portable Docker image.

**Steps**  
- Create a `Dockerfile`:
FROM nginx:alpine
COPY site/ /usr/share/nginx/html

## 4. Terraform
