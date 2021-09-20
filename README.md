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

docker pull gokulpch/angular-ssr-universal:v1
https://hub.docker.com/r/gokulpch/angular-ssr-universal

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

## Deploying it on AWS ECS
