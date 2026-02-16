Project Overview
This repository contains Kubernetes manifests, a Helm chart, and a Jenkins pipeline for deploying the ShopNow MERN application (MongoDB, Express.js, React.js, Node.js).

Components
Frontend (React): Served via Nginx, exposed with a LoadBalancer.

Backend (Node.js/Express): Exposed internally via ClusterIP, connects to MongoDB.

MongoDB: Connection string managed via Kubernetes Secret.

Helm Chart: Provides configurable deployments for FE/BE.

Jenkins Pipeline: Automates build, push, and deploy steps.

Deployment Steps
Build Docker Images

bash
docker build -t <dockerhub-user>/shopnow-frontend ./frontend
docker build -t <dockerhub-user>/shopnow-backend ./backend
Push Images

bash
docker push <dockerhub-user>/shopnow-frontend
docker push <dockerhub-user>/shopnow-backend
Deploy with Helm

bash
helm upgrade --install shopnow ./helm/shopnow-chart -f ./helm/shopnow-chart/values.yaml
Access Application

Frontend: via LoadBalancer IP

Backend: via ClusterIP (used internally by frontend)

Challenges & Solutions
Secrets Management: Used secrets.yaml for MongoDB URI instead of hardcoding.

Ingress Routing: Configured / for frontend and /api for backend.

CI/CD: Jenkins pipeline ensures consistent builds and deployments.