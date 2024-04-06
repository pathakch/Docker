## Creating Docker image+Container Uploading to ECR
This is a simple project to create a python application,dockerfile or this app , and docker image in our local machine(docker is also running in my local machine) and push this image to ECR repo for further development 
Our aim is this python application should be running in AWS BATCH for this the first step is creating python application locally , creating its docker image and pushing this image to ECR , from there we will configure, ECR+ECS+Fargate to run this image and create container and then run that container in Fargate

#### Instruction To create a Dockerfile for a python application locally
##### Steps to follow

1. Create your python application here `app.py`.
2. Create Dockerfile for this application.
3. Above both should be in same directory so that while creating image we just need to run build command no need to specify path 
4. Create docker image running this command `docker build -t <image_tag> .`
5. Create one ECR repository either from console or AWS CLI
6. Authenticate docker client locally with AWS ECR repository : ->> 
   For this, ECR repo provides command which we need to run in our local command prompt

     Command to authenticate : `aws ecr get-login-password --region ap-south-1| docker login --username AWS --password-stdin <account_id>.dkr.ecr.<region-name>.amazonaws.com`

     will get this message after successfull authentication:`Login Succeeded`
7. Tag docker image with ECR repository and any_image_name(which will be relected in ECR repo after image is pushed to ECR).

     Command : `docker tag <image_id> <aws_account_id>.dkr.ecr.ap-south-1.amazonaws.com/<ECR-repo-name>:any_image_name`
8. Push image to ECR:

     Command: `docker push <aws_account_id>.dkr.ecr.ap-south-1.amazonaws.com/<ECR-repo-name>:any_image_name` 