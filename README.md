# Flask on AWS Fargate

Deploy a containerized Flask application to AWS Fargate (Amazon ECS). This guide explains the project’s architecture, setup instructions, and how to run the application locally and in the cloud.

## Prerequisites

- AWS Account with appropriate permissions.
- AWS CLI installed and configured on your machine (aws configure).
- Docker installed and running locally.
- Python 3.9+ (for local testing) if you want to run Flask outside Docker.


## Local Setup and Testing

1. Clone or download the repository to your local machine.
```
git clone git@github.com:szymonHtf/flask-on-fargate.git
cd flask-on-fargate
```

2. (Optional) Run flask Directly (without Docker)
```
pip install -r requirements.txt
python app.py
```
Access the app at http://localhost:5000

3. Build Docker Image Locally:

```
docker build -t flask-on-fargate .
```

4. Run Docker Container

```
docker run -d -p 5000:5000 --name flask-on-fargate-container flask-on-fargate
```
Access the app at http://localhost:5000

## AWS Setup and Deployment

1. Create an ECR Repository
You can do this either in the AWS Management Console or using CLI:
```
aws ecr create-repository --repository-name flask-on-fargate
```

2. Authenticate Docker to ECR (Replace the placeholders with your values)
```
aws ecr get-login-password --region <region> | docker login --username AWS --password-stdin <account_id>.dkr.ecr.<region>.amazonaws.com
```

3. Tag and Push Image (Replace the placeholders with your values)
```
docker tag flask-on-fargate:latest <aws_account_id>.dkr.ecr.<region>.amazonaws.com/flask-on-fargate:latest
docker push <aws_account_id>.dkr.ecr.<region>.amazonaws.com/flask-on-fargate:latest
```

4. Rest of the steps are shown in the video tutorial. Please refer to the video for detailed instructions.

https://www.youtube.com/watch?v=fhRBNjYYY9k