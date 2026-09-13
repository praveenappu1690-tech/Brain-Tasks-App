# Brain Tasks App — AWS Deployment

## Overview

This project deploys a React application using AWS DevOps services.

**Flow:**

```text
GitHub → CodePipeline → CodeBuild → ECR → EKS → Browser
```

## Technologies

* GitHub
* Docker
* Nginx
* Amazon ECR
* Amazon EKS
* Kubernetes
* AWS CodeBuild
* AWS CodePipeline
* CloudWatch

## Project Structure

```text
Brain-Tasks-App/
├── dist/
├── kubes/
│   ├── deployment.yaml
│   └── service.yaml
├── Dockerfile
├── buildspec.yml
└── README.md
```

## Docker

Build the Docker image:

```bash
docker build -t brain-tasks-app .
```

Run the application:

```bash
docker run -d -p 3000:80 brain-tasks-app
```

Open:

```text
http://EC2-PUBLIC-IP:3000
```

## Amazon ECR

The Docker image is stored in Amazon ECR:

```text
ACCOUNT_ID.dkr.ecr.ap-south-1.amazonaws.com/brain-tasks-app
```

## Amazon EKS

Configure the EKS cluster:

```bash
aws eks update-kubeconfig --region ap-south-1 --name CLUSTER_NAME
```

Check nodes:

```bash
kubectl get nodes
```

Deploy the application:

```bash
kubectl apply -f kubes/deployment.yaml
kubectl apply -f kubes/service.yaml
```

Check the application:

```bash
kubectl get pods
kubectl get svc
```

The application is exposed using a Kubernetes **LoadBalancer**.

```text
http://LOAD-BALANCER-DNS:3000
```

## CI/CD

AWS CodePipeline automates the deployment:

```text
GitHub
   ↓
CodePipeline
   ↓
CodeBuild
   ↓
Docker Build
   ↓
Amazon ECR
   ↓
Amazon EKS
```

CodeBuild uses `buildspec.yml` to build and push the Docker image.

CloudWatch is used to view CodeBuild logs.

## Useful Commands

```bash
kubectl get pods
kubectl get svc
kubectl get deployments
kubectl get all
kubectl logs deployment/brain-tasks-app
```

## Screenshots

Add screenshots of:

* GitHub Repository
* Docker Application
* ECR Image
* EKS Cluster
* Running Application
* CodeBuild Success
* CodePipeline Success
* CloudWatch Logs
* Load Balancer

## Conclusion

The Brain Tasks React application was successfully deployed using **Docker, Amazon ECR, Amazon EKS, Kubernetes, CodeBuild, and CodePipeline**.
