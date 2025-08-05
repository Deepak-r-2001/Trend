# Trend App Deployment - DevOps Project

## ✅ Project Summary
A complete CI/CD pipeline to deploy a React application on AWS EKS using Jenkins, Docker, Terraform, Prometheus, and Grafana.

## 🐳 Docker
- Dockerfile created to containerize the React app.
- Image pushed to DockerHub.

## ☁️ Terraform
- Infrastructure provisioned: VPC, IAM roles, EC2 (Jenkins), and EKS Cluster.

## 🚀 Kubernetes (EKS)
- Application deployed using `deployment.yaml` and exposed via LoadBalancer.
- Verified with `kubectl get pods/services`.

## 🔧 CI/CD - Jenkins
- Jenkins pipeline automates the build, Docker image push, and Kubernetes deployment.
- GitHub integrated using Webhooks.

## 📊 Monitoring
- Prometheus and Grafana installed on EKS.
- Grafana dashboards created for cluster and app monitoring.

## 📎 Application LoadBalancer URL
[http://aa382ab88486b40ea8db56fd257aa0f0-1581967591.ap-south-1.elb.amazonaws.com/](http://aa382ab88486b40ea8db56fd257aa0f0-1581967591.ap-south-1.elb.amazonaws.com/)

## 📷 Screenshots
> Add the following screenshots to this repo (in a `/screenshots` folder or below):
- Jenkins pipeline (success state)
- Kubernetes pods/services (`kubectl get pods -A`)
- React app running from LoadBalancer URL
- Grafana dashboards

## 📂 Folder Structure
```
trend-project/
├── Dockerfile
├── Jenkinsfile
├── terraform/
│   ├── main.tf
│   ├── variables.tf
├── k8s/
│   ├── deployment.yaml
│   ├── service.yaml
├── monitoring/
│   ├── prometheus.yaml
│   ├── grafana-dashboards/
├── screenshots/
│   ├── jenkins.png
│   ├── grafana.png
│   └── ...
├── README.md
```

---
🕓 *Generated on 2025-08-05 16:36:52*
