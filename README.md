# angular-ssr-example

A simple example of a Dockerized Angular app that uses Angular Universal for server-side rendering.

Building and deploying the application on EKS and ECS for public consumption

# Quick start

## Build Docker image with Express SSR (server side rendering)

```bash
docker build . --file Dockerfile.ssr --build-arg ENV=dev --tag angular-ssr-example:latest
docker run -p 8080:80 angular-ssr-example:latest
```

## Image available at

https://hub.docker.com/r/gokulpch/angular-ssr-universal

```
docker pull gokulpch/angular-ssr-universal:v1
```

## Deploying it on AWS EKS

Need a running EKS cluster. Create a EKS Cluster using: https://docs.aws.amazon.com/eks/latest/userguide/create-cluster.html

Deploy the manifest from kubernetes-manifest directory:

```
kubectl create -f kubernetes-manifests/
```

Access the Application using the LoadBalancer IP

```
kubectl get svc
NAME             TYPE           CLUSTER-IP      EXTERNAL-IP                                                              PORT(S)        AGE
angular-webapp   LoadBalancer   10.100.22.114   a71decbhsdbuuewjcndnjncjdnjcjndd-651101815.us-west-1.elb.amazonaws.com   80:30231/TCP   3m58s
```

### Application Runnng on EKS as a Deployment
![ScreenShot](/images/ang-app-eks-1.png)

### Application - Pod on EKS
![ScreenShot](/images/ang-app-eks-2.png)

### Accessing Application using AWS LoadBalancer created by type:LoadBalancer
![ScreenShot](/images/ang-web.png)

## Deploying it on AWS ECS



## Using ECR as Image Repository

Docker build the image and push it to your ECR.


Get password and login to ECR:
```
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin aws_account_id.dkr.ecr.us-east-1.amazonaws.com
```

Create a Repository on the default repo or as required:
```
aws ecr create-repository \     
     --repository-name angular-universal/angular-ssr\     
     --image-scanning-configuration scanOnPush=true \
     --image-tag-mutability IMMUTABLE     
     --region us-east-2
```

Tag and Push the image to ECR:

```
docker tag angular-universal-ssr:latest 900488099787.dkr.ecr.us-east-2.amazonaws.com/frontend/angular-node:v1
```

```
docker push 900488099787.dkr.ecr.us-east-2.amazonaws.com/frontend/angular-universal-ssr:v1
```
