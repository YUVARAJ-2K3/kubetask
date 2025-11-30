# 🚀 Kubernetes Microservices Deployment – Auth | Users | Tasks | Frontend

This project demonstrates a complete **microservices architecture** deployed on **Kubernetes**, featuring independent services for Authentication, Users, Tasks, and a React Frontend.  
All services are fully containerized using Docker and orchestrated using Minikube.

## 📌 Architecture Overview

The system consists of **four microservices**, each running independently inside the Kubernetes cluster:

### 🔹 Frontend (React)
- Public entrypoint using **LoadBalancer**
- Communicates with backend via REST APIs

### 🔹 Auth API
- JWT authentication and token validation  
- Internal-only access via **ClusterIP**

### 🔹 Users API
- Stores and serves user identity & metadata

### 🔹 Tasks API
- Handles task creation, storage, updating, and retrieval  
- Validates JWT via Auth API internally

## ☸️ Kubernetes Components Used

| Component | Purpose |
|----------|---------|
| **Deployments** | Manage replicas for each microservice |
| **ClusterIP Services** | Internal communication (Auth, Users, Tasks) |
| **LoadBalancer Service** | Public access to the Frontend |
| **Pods** | Containers running inside the cluster |
| **ConfigMaps / Secrets** | Store configs & sensitive data |
| **DNS Service Discovery** | Internal URLs like `auth-service`, `tasks-service` |

## 📡 High-Level Architecture Flow

1. User ↠ **Frontend LoadBalancer**
2. Frontend ↠ **Tasks API**
3. Tasks API ↠ **Auth API** (JWT verification)
4. Tasks API ↠ **Users API** (user details)
5. Backend services communicate internally using **ClusterIP**

Internal DNS resolves services automatically:

```
http://auth-service:3001
http://users-service:3002
http://tasks-service:3003
```

## 🐳 Docker Image Workflow

Each microservice is built and pushed to Docker Hub.

```bash
docker build -t <username>/<service-name> .
docker push <username>/<service-name>
```

Example:
```bash
docker push yuvaraj2k3/auth-service
```

## 📁 Project Structure

```
/kubetask
 ├── auth-api/
 ├── users-api/
 ├── tasks-api/
 ├── frontend/
 ├── k8s/
 │    ├── auth-deployment.yaml
 │    ├── users-deployment.yaml
 │    ├── tasks-deployment.yaml
 │    ├── frontend-deployment.yaml
 │    └── services.yaml
 └── README.md
```

## 🚀 How to Deploy on Minikube

### 1️⃣ Start Minikube
```bash
minikube start
```

### 2️⃣ Apply All Kubernetes Manifests
```bash
kubectl apply -f k8s/
```

### 3️⃣ Verify Running Pods
```bash
kubectl get pods
```

### 4️⃣ Access Frontend
```bash
minikube service frontend-service
```

## 📸 Architecture Diagram

Place your generated diagram inside the repo as shown:

```
![Kubernetes Architecture](architecture.png)
```

## 🎯 What I Learned

- Kubernetes deployments, services & rollouts  
- Internal microservices communication  
- ClusterIP vs LoadBalancer  
- Docker image lifecycle (build → push → deploy)  
- Scalable microservice design  
- DNS-based service discovery in Kubernetes  

## 🔗 Repository Link

👉 **GitHub:** https://github.com/YUVARAJ-2K3/kubetask

## 🏷️ Tech Stack

- Kubernetes  
- Docker  
- Node.js  
- React  
- Minikube  
- YAML  
- JWT Authentication  

## 🌟 Contributing

Contributions, issues, and feature requests are welcome!

## 📄 License

MIT License © 2025 Yuvaraj S
