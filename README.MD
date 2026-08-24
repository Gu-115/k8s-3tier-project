# Kubernetes 3-Tier Application

A containerized 3-tier web application deployed on Kubernetes using Docker and AWS EC2.

## Architecture

User
  |
  v
Frontend (Nginx)
  |
  v
Backend (Flask)
  |
  v
Kubernetes Services

## Technologies Used

- AWS EC2
- Linux / Ubuntu
- Docker
- Kubernetes
- Minikube
- Nginx
- Python Flask
- Git & GitHub
- kubectl

## Project Structure

k8s-3tier-project/
├── frontend/
│   ├── Dockerfile
│   └── index.html
├── backend/
│   ├── Dockerfile
│   ├── app.py
│   └── requirements.txt
├── k8s/
│   ├── backend-deployment.yaml
│   ├── backend-service.yaml
│   ├── frontend-deployment.yaml
│   └── frontend-service.yaml
└── README.md

## Kubernetes Components

### Backend

- Deployment: backend
- Service: backend-service
- Type: ClusterIP
- Port: 5000

### Frontend

- Deployment: frontend
- Service: frontend-service
- Type: NodePort
- NodePort: 31130
- Port: 80

## Deployment

Start Minikube:

minikube start --driver=docker

Check cluster:

kubectl get nodes

Apply Kubernetes manifests:

kubectl apply -f k8s/

Check deployments:

kubectl get deployments

Check pods:

kubectl get pods

Check services:

kubectl get svc

Access frontend:

minikube service frontend-service --url

## Verification

Backend and frontend pods should show:

1/1 Running

Services:

backend-service     ClusterIP
frontend-service    NodePort

## Docker

Build backend image:

docker build -t k8s-backend:v1 ./backend

Build frontend image:

docker build -t frontend:v1 ./frontend

## Project Highlights

- Containerized frontend and backend applications using Docker
- Deployed application on Kubernetes
- Configured Kubernetes Deployments and Services
- Used ClusterIP for internal backend communication
- Used NodePort for frontend access
- Managed Kubernetes cluster using kubectl
- Hosted development environment on AWS EC2

## Author

AWS DevOps / Cloud Engineer
