# Static Website Deployment Guide  
This document will highlight the code used and what the code means and does for reference.

All the work mentioned here can be found at: https://github.com/tworsum4yu/mthree_website_practice

---

### 1. Website Generation  
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

## Deployment file
This section will give some quick details on getting started with the deployment file for the project.

Please find the deploy file used in this tutorial here: https://github.com/tworsum4yu/mthree_website_practice/blob/main/.github/workflows/deploy.yml

Following will be a breakdown on what exactly is going on for clarity sake.

--- 

![BeginningStepsOfDeploy](./assets/Deploy1.png) <br>
*Figure 1: Intial Setup*

> name: *your_deployment_name*

Sets the name of the deployment workflow. This will be presented within the actions tab in github.

> on: <br>
> ├── push: <br>
> │     └── branches: ['main'] <br>
> └── workfow_dispatch: {}

Tells github that this workflow should be run everytime new code is pushed to the main branch. In addition, the workflow_dispatch line allows the workflow to be run manually in the action tab in the repository.

![StartOfJobs](./assets/Deploy2.png) <br>
*Figure 2: Intial Jobs to ensure code is correct*

> jobs: <br>
> └── deploy:

The jobs tag tells Github that what follows below are jobs to be run by Github. The deploy tag is just a name assigned to the following tasks, so that it is easier to track what jobs are running during the workflow.

> runs-on: ubuntu-latest

Simple line that tells Github that the latest version of ubuntu is being used to run the commands in this jobn.

> env: <br>
> ├── host: ... <br>
> ├── username: ... <br>
> └── key: ...

These are environmental variables. This means variables that are live and accessible throughout the jobs runtime. 

These variables look at the values stored in the labelled secrets in the repository and essentially assign the value to the environment variable. If the secret doesn't exist, then this returns null.

> steps: <br>
> └── uses: actions/checkout@v4

***Steps*** tells github the different steps to follow.<br>
This first ***uses*** is extremely important as it tells github to pull in the repositories code for use during the workflow. Without this line, Github would be operating on nothing.

***The following steps of the deployment file are extra steps that may not be necessary for your project right now, but is still good to know about.***

> name: Node setup<br>
> ├── uses: actions/setup-node@v4<br>
> └── with: <br>
> &nbsp;&nbsp;&nbsp;&nbsp;├── node-version: 24.13.0 <br>
> &nbsp;&nbsp;&nbsp;&nbsp;└── cache: npm

The above step sets up node so that the GitHub Actions runner (the thing running this workflow) can use Node to run the later steps. The specific node version is specified to keep consistencies between different runs and ***cache: npm*** tells Github to cache the generate ***node_modules*** folder, ensuring that following runs are faster as no repeated dependencies will be installed.

> name: Install Dependencies<br>
> └── uses: npm ci

Simple step that installs the required dependencies. <br>
**Important Note:** we are using ***npm ci*** instead of ***npm install*** as ***ci*** will install the exact versions that are present in the ***package-lock.json*** file, rather than ***install*** which will just install the latest version. This will prevent compatability issues across the versions of each dependancy, increasing the consistency of the workflow.

> name: Prettier check <br>
> └── uses: npm run format:check

Simple line that just runs the *format:check* script from the *package.json* file. This script that is run is *prettier . --check* and all this does is check that the source code is formatted in the standardised way set with prettier.

> name: Eslint check <br>
> └── uses: npm run lint

Simple line that just runs the *lint* script from the *package.json* file. This script that is run is *eslint .* which does a check to ensure that there are no issues with the code (for example; syntax issues, or unused variables).

### S3

---

## 3. Docker Containerisation  
Package your static site into a portable Docker image.

**Steps**  
- Create a `Dockerfile`:
FROM nginx:alpine
COPY site/ /usr/share/nginx/html

## 4. Terraform

## Glossary

### S3
Amazon S3 (Simple Storage Service) is AWS’s scalable object‑storage service used to store and retrieve any amount of data at any time. Instead of thinking in terms of folders on a server, S3 stores files as objects inside buckets.

**Key points**
- Object storage — stores files like HTML, CSS, JS, images, videos, logs, backups, etc.
- Highly durable — designed for 11 nines of durability (99.999999999%).
- Infinitely scalable — you never run out of space.
- Pay‑as‑you‑go — you only pay for what you store and transfer.
- Static website hosting — can serve HTML/CSS/JS directly over the web.
- Integrates with AWS services — CloudFront, EC2, Lambda, ECR, and more.

### ECR
Amazon ECR (Elastic Container Registry) is AWS’s fully managed Docker container registry. It stores, manages, and version‑controls your container images so they can be pulled by services like EC2, ECS, EKS, or Lambda.

**Key points**
- Private or public registry for Docker images
- Integrates seamlessly with AWS IAM for secure access
- Supports versioning and tagging of images
- Works directly with Docker CLI (docker push, docker pull)
- Often used with CI/CD pipelines for automated deployments
- Highly available and scalable — no registry servers to manage

### Docker
Docker is a platform that lets you package applications into containers — lightweight, portable environments that include everything the app needs to run.

**Key points**
- Containers bundle code + dependencies into a single unit
- Ensures consistent behavior across machines (“works on my machine” solved)
- Much lighter than virtual machines
- Uses Dockerfiles to define how images are built
- Integrates with registries like Docker Hub and AWS ECR
- Ideal for microservices, deployments, and reproducible environments

### EC2
Amazon EC2 (Elastic Compute Cloud) provides virtual servers in the cloud. You choose the OS, CPU, memory, storage, and networking, and AWS runs the machine for you.

**Key points**
- Virtual machines you can start, stop, and scale
- Supports Linux, Windows, and custom AMIs
- Works well for hosting apps, APIs, containers, and background jobs
- Integrates with ECR to run Docker containers
- Security groups act as virtual firewalls
- You pay only for the compute time you use

### Terraform
Terraform is an Infrastructure as Code (IaC) tool that lets you define cloud resources using configuration files instead of clicking around in the AWS console.

**Key points**
- Declarative language (HCL) describes your infrastructure
- Supports AWS, Azure, GCP, and many other providers
- Enables version‑controlled infrastructure
- terraform plan shows changes before applying
- terraform apply creates or updates resources
- Great for reproducible, automated, and team‑friendly cloud setups

### Prettier
Prettier is an opinionated code formatter that automatically enforces consistent styling across your project. Instead of manually fixing spacing, quotes, or indentation, Prettier reformats your code for you every time you save or run it.

**Key points**
- Automatically formats code for consistency
- Removes debates about style (tabs vs spaces, quotes, etc.)
- Supports JavaScript, TypeScript, HTML, CSS, JSON, Markdown, and more
- Integrates with editors, Git hooks, and CI pipelines
- Works alongside ESLint to handle formatting while ESLint handles logic and quality

### ESLint
ESLint is a static analysis tool that scans your JavaScript or TypeScript code for errors, bad patterns, and violations of best practices. It helps catch bugs early and keeps your codebase clean and maintainable.

**Key points**
- Detects syntax errors, unused variables, and risky patterns
- Enforces coding standards and best practices
- Highly configurable with plugins and rule sets
- Integrates with editors and CI pipelines
- Complements Prettier by focusing on code quality rather than formatting