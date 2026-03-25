# Static Website Deployment Guide  
Deploying a static website using **S3**, **Docker**, **ECR**, and **EC2**

This guide walks through the full workflow for generating a static site, containerising it, pushing the image to AWS ECR, and running it on an EC2 instance.

---

## 1. Website Generation  
A lightweight static site is all you need for this deployment.

### Steps  
- Create a simple project structure:
/site
index.html
styles.css
script.js

- Use relative paths for all assets (e.g., `./images/logo.png`).
- Test locally by opening `index.html` in your browser.
- Confirm the site works without any backend dependencies.

---
## 2. Deployment file  
This section will give some quick details on getting started with the deployment file for the project.

### Steps  
![BeginningStepsOfDeploy](./assets/Deploy1.png)

## S3
The aim here is to push our static website onto S3 to be stored.


### What is S3?
Amazon S3 (Simple Storage Service) is AWS’s scalable object‑storage service used to store and retrieve any amount of data at any time. Instead of thinking in terms of folders on a server, S3 stores files as objects inside buckets.

##### Key points
- Object storage — stores files like HTML, CSS, JS, images, videos, logs, backups, etc.
- Highly durable — designed for 11 nines of durability (99.999999999%).
- Infinitely scalable — you never run out of space.
- Pay‑as‑you‑go — you only pay for what you store and transfer.
- Static website hosting — can serve HTML/CSS/JS directly over the web.
- Integrates with AWS services — CloudFront, EC2, Lambda, ECR, and more.


---

## 3. Docker Containerisation  
Package your static site into a portable Docker image.

### Steps  
- Create a `Dockerfile`:
FROM nginx:alpine
COPY site/ /usr/share/nginx/html
