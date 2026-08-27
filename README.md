DevOps Project 2 — Nginx Application Deployment

Project Overview

This project demonstrates the deployment of an Nginx-based web application using Docker and Kubernetes, with a GitHub Actions CI pipeline for automated Docker image building and application testing.

The project covers the complete flow from source code to containerization, automated CI testing, and Kubernetes deployment.

Architecture

GitHub Repository
       ↓
GitHub Actions
       ↓
Docker Image Build
       ↓
Docker Container Test
       ↓
Kind Kubernetes Cluster
       ↓
Kubernetes Deployment
       ↓
2 Nginx Pods
       ↓
Kubernetes Service
       ↓
Nginx Web Application

Technologies Used

- Git
- GitHub
- GitHub Actions
- Docker
- Nginx
- Kubernetes
- Kind
- Linux

Project Structure

nginx-kubernetes-project/
│
├── Dockerfile
├── README.md
├── index.html
│
└── k8s/
    ├── deployment.yaml
    └── service.yaml

Application

The project contains a custom HTML page served using Nginx.

The application displays:

DevOps Project 2

DevOps application deployed using Docker and Kubernetes

Docker

The application is containerized using Docker.

Build the Docker Image

docker build -t nginx-devops-project:1.0 .

Run the Container

docker run -d -p 8081:80 --name nginx-devops-app nginx-devops-project:1.0

The application can then be tested locally using:

curl.exe http://localhost:8081

GitHub Actions CI

A GitHub Actions workflow automatically runs when code is pushed to the repository.

The CI pipeline performs the following steps:

1. Checks out the source code.
2. Builds the Docker image.
3. Starts an Nginx container.
4. Waits for the Nginx service to start.
5. Tests the application using "curl".

Successful execution of the workflow confirms that the Docker image can be built and the application can run successfully.

Kubernetes Deployment

The application is deployed to a local Kubernetes cluster created using Kind.

The Kubernetes Deployment runs 2 replicas of the Nginx application.

Apply the Deployment:

kubectl apply -f k8s/deployment.yaml

Check the Pods:

kubectl get pods

Expected result:

2 Pods
STATUS: Running

Loading the Docker Image into Kind

Because the Docker image is built locally, it needs to be loaded into the Kind cluster before Kubernetes can use it.

kind load docker-image nginx-devops-project:1.0 --name devops-cluster

The Deployment uses:

image: nginx-devops-project:1.0
imagePullPolicy: IfNotPresent

This allows Kubernetes to use the locally loaded image.

Kubernetes Service

A Kubernetes NodePort Service exposes the Nginx application.

Apply the Service:

kubectl apply -f k8s/service.yaml

Check the Service:

kubectl get svc nginx-devops-service

The Service uses:

Service Port: 80
Target Port: 80
NodePort: 30080

The traffic flow is:

NodePort 30080
      ↓
Service Port 80
      ↓
Nginx Container Port 80

Testing the Kubernetes Application

For local testing with Kind, port-forwarding can be used:

kubectl port-forward service/nginx-devops-service 8082:80

In another terminal:

curl.exe http://localhost:8082

The response should display the custom Project 2 HTML page.

Key DevOps Concepts Demonstrated

- Source code management with Git and GitHub
- GitHub Actions CI automation
- Docker image creation
- Docker container execution
- Automated application testing with "curl"
- Nginx containerization
- Kubernetes Deployments
- Kubernetes Pods and replicas
- Kubernetes Services
- NodePort networking
- Kind Kubernetes clusters
- Loading local Docker images into Kubernetes
- Deploying a custom container image to Kubernetes
- Basic troubleshooting of Docker, Kubernetes, ports, and services

Project Outcome

The project successfully demonstrates a complete containerized application workflow:

Source Code
    ↓
GitHub
    ↓
GitHub Actions CI
    ↓
Docker Image
    ↓
Docker Container
    ↓
Kind Kubernetes Cluster
    ↓
Kubernetes Deployment
    ↓
2 Running Pods
    ↓
NodePort Service
    ↓
Custom Nginx Web Application

Skills Demonstrated

Git | GitHub | GitHub Actions | Docker | Kubernetes | Kind | Nginx | Linux | CI/CD

Author

Syed Yakub
