# 🚆 Railway Ticket Booking Application Helm Chart

- This Helm chart deploys a simple **Railway Ticket Booking Application** on a Kubernetes cluster. It includes both **frontend** and **backend** services and connects to an external **AWS RDS** database using credentials securely managed via Kubernetes **Secrets**.

## 📁 Helm Chart Directory Structure

```
helm-chart/
├── Chart.yaml                      # Helm chart metadata (name, version, dependencies)
├── values.yaml                     # Configuration values for the chart (images, secrets, replicas, etc.)
└── templates/                      # Kubernetes manifest templates
    ├── frontend-deployment.yaml    # Deployment for the frontend application
    ├── frontend-service.yaml       # Service to expose the frontend
    ├── backend-deployment.yaml     # Deployment for the backend application
    ├── backend-service.yaml        # Service to expose the backend
    └── db-secret.yaml              # Kubernetes Secret storing AWS RDS credentials
```

## 🔐 AWS RDS Credentials via Kubernetes Secrets

- The database `username` and `password` for `AWS RDS` are stored securely in `Kubernetes Secrets`.

- The `secrets` are referenced in the `backend deployment` and passed as environment variables.

- These values are defined and managed via `values.yaml`.

   - Customize values.yaml:
 
   - Edit the `values.yaml` file to include your specific configuration:
 
```
frontend:
  deploymentname: frontend-deployment
  replicas: 1
  image: 657001761946.dkr.ecr.us-east-1.amazonaws.com/repo-front:1.0.9
  servicename: frontend-service
  type: LoadBalancer

backend:
  deploymentname: backend-deployment
  replicas: 1
  image: 657001761946.dkr.ecr.us-east-1.amazonaws.com/repo-back:1.0.9
  servicename: backend-service

db:
  secrets:
    name: db-secrets
    username: dmlqYXk=
    password: UGFzc3dvcmQxMjM=
```

## Clone the repository (if using locally):

```
git clone https://github.com/vijaygiduthuri/aws-2-tier-helm-chart.git
cd helm-chart
```

- Install the Helm chart:

```
helm install railway-app ./helm-chart
helm status railway-app
(or)
helm ls
```

- Upgrade the release (on changes):

```
helm upgrade railway-app ./helm-chart
```

- Uninstall the chart:

```
helm uninstall railway-app
```

**Note:** Ensure your Kubernetes cluster has access to the AWS RDS endpoint (VPC, subnet, security group, etc.).
