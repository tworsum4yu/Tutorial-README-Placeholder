# ECR Commands
Below are some ECR commands and what they do. Useful fo the ECR step <br>

**FYI:** *Please refer to the other github that has details on the "deploy.yml" file. There are mentions to environmental variables in here, which may or may not be easier to see and understand from the file itself.* 

---

## Credentials

> aws configure list

List the configure values you used when configuring AWS. Useful if you want to remember what region you are using.

> aws sts get-caller-identity

Lists the account information that you are signed into. 

> aws sts get-caller-identity --query Account --output text

This line retrieves the "Account" value from the returned data and outputs it to text. Useful within the deploy to get account info without hard coding.

---

## See existing repositories and images

> aws ecr describe-repositories

Lists the current available repositories registered by the account

> aws ecr list-images --repository-name {YOUR_REPOSITORY_NAME}

List the docker image IDs of the docker images that have been pushed to a specific repository. The repository is decided through {YOUR_REPOSITORY_NAME}.

> aws ecr describe-images --repository-name {YOUR_REPOSITORY_NAME}

Does the same as list-images but gives more detail.

---

## Create new repository

> aws ecr create-repository --repository-name {REPOSITORY_NAME}

Creates a new repository in ECR with the name that you give it in {REPOSITORY_NAME}.

> aws ecr describe-repositories --repository-names {YOUR_REPOSITORY_NAME} || aws ecr create-repository --repository-name {YOUR_REPOSITORY_NAME}

Trys to describe the repositories with the name you give it and if it does not exist, it creates it.

---

## Docker signin

> aws ecr get-login-password --region <region> \
> | docker login \
> --username AWS \
> --password-stdin <account-id>.dkr.ecr.<region>.amazonaws.com

Allows docker to push the built images onto ECR. Information on what it does below.

> aws ecr get-login-password --region <region>

Tells AWS to give you a temporary password so that you can use it to sign into ECR using docker.

> |

Pushes the returned password from AWS into the command that follows it.

> docker login \
> --username AWS \
> --password-stdin <account-id>.dkr.ecr.<region>.amazonaws.com

Tells docker to sign into ECR using AWS as its username (for ECR the username will always be AWS), and the password from AWS and the ECR registry you are trying to access.

---

## Docker build and push

> REGISTRY="{ACCOUNT_ID}.dkr.ecr.{AWS_REGION}.amazonaws.com"

Above details where in AWS docker can find the repository where you want to store your image. {ACCOUNT_ID} is the account id you used to create the repository and {AWS_REGION} is the region used when creating the repository.

> IMAGE_SHA="{REGISTRY}/{REPO_NAME}:{SHA}"
> IMAGE_LATEST="{REGISTRY}/{REPO_NAME}:latest"

Examples of the images that you would build. <br>
**LATEST** represents the latest version and **SHA** represents a previous version that can be rollbacked to in case issues occur with the latest. <br>
{REPO_NAME} represents the name you gave to the repository you created. {SHA} in this case is the github.SJA value for the last deploy workflow.

> docker build -t "{IMAGE_SHA}" -t "{IMAGE_LATEST}" .

Builds the images you have defined.

> docker push "{IMAGE_SHA}"
> docker push "{IMAGE_LATEST}"

Pushes your imagesinto the ECR repository.
