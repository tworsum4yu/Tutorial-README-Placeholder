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
## 2. S3 (Static Hosting)  
The aim here is to push our static website onto S3 to be stored.

### Steps  
- Create a new S3 bucket (name must be globally unique).
- If hosting directly from S3:
- Disable “Block all public access”.
- Enable **Static Website Hosting**.
- Set `index.html` as the index document.
- Add a bucket policy allowing public read access.
- Upload your site files.
- Test using the bucket’s website endpoint.

---

## 3. Docker Containerisation  
Package your static site into a portable Docker image.

### Steps  
- Create a `Dockerfile`:
FROM nginx:alpine
COPY site/ /usr/share/nginx/html
