# Docker Compose MERN Stack with Nginx example

Dockerize fullstack: React, Nodejs Express and MongoDB (MERN stack application) example using Docker Compose with Nginx.

## Run the System
We can easily run the whole with only a single command:
```bash
docker-compose up
```

Docker will pull the MongoDB and Node.js images (if our machine does not have it before).

The services can be run on the background with command:
```bash
docker-compose up -d
```

## Stop the System
Stopping all the running containers is also simple with a single command:
```bash
docker-compose down
```

# MERN Stack DevOps Project

## Overview
Full-stack MERN application with complete CI/CD pipeline using Jenkins, Docker, and Kubernetes.

## Technologies Used
- **Frontend:** React.js
- **Backend:** Node.js + Express
- **Database:** MongoDB
- **CI/CD:** Jenkins
- **Containerization:** Docker
- **Orchestration:** Kubernetes (Minikube)
- **Version Control:** Git/GitHub

## Architecture
```
GitHub → Webhook → Jenkins → Docker Build → Docker Hub → Kubernetes Deployment
```

## Features
- Automated CI/CD pipeline with Jenkins
- GitHub webhook integration for automatic builds
- Docker containerization of all services
- Kubernetes orchestration with multiple replicas
- Persistent storage for MongoDB

## Deployment

### Prerequisites
- Docker Desktop
- Minikube
- kubectl
- Jenkins

### Kubernetes Deployment
```bash
kubectl apply -f k8s/mongodb-deployment.yaml
kubectl apply -f k8s/backend-deployment.yaml
kubectl apply -f k8s/frontend-deployment.yaml
```

### Access Application
```bash
kubectl port-forward service/frontend 8888:80
```
Then visit: http://localhost:8888

## Jenkins Pipeline Stages
1. **Checkout** - Pull code from GitHub
2. **Build** - Create Docker images for frontend and backend
3. **Push** - Upload images to Docker Hub
4. **Cleanup** - Logout from Docker Hub

## Project Structure
```
├── bezkoder-api/          # Backend Node.js application
├── bezkoder-ui/           # Frontend React application
├── k8s/                   # Kubernetes manifests
├── nginx/                 # Nginx configuration
├── Jenkinsfile            # Jenkins pipeline definition
└── docker-compose.yml     # Docker Compose configuration
```
