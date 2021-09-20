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
