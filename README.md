Deployment Steps
1. Build Docker Images
bash
docker build -t kumarDevOps/shopnow-frontend ./frontend
docker build -t kumarDevOps/shopnow-backend ./backend
2. Push Images to DockerHub
bash
docker push kumarDevOps/shopnow-frontend
docker push kumarDevOps/shopnow-backend
3. Deploy with Helm
bash
helm upgrade --install shopnow ./shopnow-chart -f ./shopnow-chart/values.yaml
4. Access Application
Frontend: via LoadBalancer IP (e.g., http://<LB-IP>).

Backend: via ClusterIP (used internally by frontend).

Ingress: routes / to frontend and /api to backend.

🔑 Helm Usage
Install:

bash
helm install shopnow ./shopnow-chart
Upgrade:

bash
helm upgrade shopnow ./shopnow-chart
Uninstall:

bash
helm uninstall shopnow
🛠️ Jenkins Pipeline
The Jenkinsfile automates:

Build frontend and backend Docker images.

Push images to DockerHub.

Deploy using Helm into Kubernetes.

⚠️ Challenges & Solutions
Secrets Management:
Used secrets.yaml to store MongoDB credentials securely instead of hardcoding.

Ingress Routing:
Configured ingress to route / → frontend and /api → backend.

CI/CD Automation:
Jenkins pipeline ensures consistent builds and deployments across environments.
