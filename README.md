# Static Website Deployment Guide  
Deploying a static website using **S3**, **Docker**, **ECR**, and **EC2**

This guide walks through the full workflow for generating a static site, containerising it, pushing the image to AWS ECR, and running it on an EC2 instance.

---

## Steps to follow

## 1. Website Generation  
A lightweight static site is all you need for this deployment.

**Steps**  
Create a simple project structure:
> site <br>
> ├── index.html <br>
> ├── styles.css <br>
> └── script.js

- Use relative paths for all assets (e.g., `./images/logo.png`).
- Test locally by opening `index.html` in your browser.
- Confirm the site works without any backend dependencies.

---

## 2. Deployment file (deploy.yml)
This is the file that will run everytime you do a commit to the main branch in your github. 

**What the should happen during deployment:**
- **Upload your static site to S3** <br>
Ensures your latest HTML, CSS, JS, and assets are stored in your S3 bucket for hosting or distribution. <br>
***Please look below at S3 for more information***

- **Build and push a Docker image to ECR** <br>
Packages your site into a Docker image and stores it in Amazon ECR so EC2 (or other services) can pull and run it.
***Please look below at docker and ECR for more information***

- **Deploy the site to EC2**  <br> 
Connects to your EC2 instance and updates the running application using the latest code or Docker image.
***Please look below at EC2 for more information***

--- 

## S3
Here we are going to learn how to push our source code into S3. 

***IMPORANT: For the S3 step, we will be using the first bucket*** <br>
***IMPORANT:*** *The credentials sent are necessary for the deployment step.*

***Setup AWS credentials in local terminal:***<br>
aws configure

***Test Listing Buckets***<br>
aws s3 ls s3://mthree-peregrine-s3-# *(# represents a number)*

***Test Uplaod***<br>
aws s3 cp *{YOUR_FILE}* s3://mthree-peregrine-s3-1/

***Test Download***<br>
aws s3 cp s3://mthree-peregrine-s3-1/*{YOUR_FILE}*

***Test Delete***<br>
aws s3 rm s3://mthree-peregrine-s3-1/*{YOUR_FILE}*

---

## Docker
Here you just need to learn how to containerise your application locally. <br>
Two things you will need to look into. Dockerfiles and docker-compose.yml 

## ECR
After completing the Docker containerisation locally. You need to figure out how to utilise the deployment file you have created to generate a docker image of your code and push it to ECR.

## EC2

