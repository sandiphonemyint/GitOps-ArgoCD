# 🎮 GitOps Implementation with Argo CD and GKE

### 📘 Project Overview

This project showcases how to deploy a containerized **Tetris game** to **Google Kubernetes Engine (GKE)** using **Argo CD** with the **GitOps** approach.

GitOps is a modern deployment strategy where Git is the single source of truth, and changes to infrastructure or applications are automatically synced to Kubernetes clusters. With Argo CD, every update to the Git repository is continuously monitored and applied to the cluster, ensuring consistent, reliable, and auditable deployments.

By completing this project, I’ve built a real-world GitOps workflow, demonstrating how modern DevOps teams manage cloud-native applications with automation, version control, and confidence.

---

### 🚀 Tech Stack

- GKE (Google Kubernetes Engine)
- Argo CD
- GitHub (for GitOps)
- Docker
- Kubernetes YAML

---

### ⚙️ Setup Instructions

#### 1️⃣ Create a GKE Cluster (Standard mode)
> Make sure the GKE cluster is running and ready.

---

#### 2️⃣ Connect to GKE and Install Argo CD

```bash
✅ Set project variables
export PROJECT_ID=$PROJECT_ID
export CLUSTER_NAME=$CLUSTER_NAME
export ZONE=$ZONE 

✅ Set GCP project
>> gcloud config set project $PROJECT_ID

✅ Connect kubectl to the cluster
>> gcloud container clusters get-credentials $CLUSTER_NAME --zone=$ZONE --project=$PROJECT_ID

✅ Create argocd namespace
>> kubectl create namespace argocd

✅ Install Argo CD
>> kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

✅ Expose Argo CD via LoadBalancer
>> kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'

✅ Get Argo CD external IP (wait until assigned)
>> kubectl get svc argocd-server -n argocd

✅ Get Argo CD admin password
>> kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo

✅ Access Argo CD
URL: https://<EXTERNAL-IP> External IP from LoadBalancer 
Username: admin
Password: (from the command above)

---

## 🚀 Next Steps

- 🔗 Connect your GitHub repo to Argo CD  
- 🚀 Create your Argo CD app using CLI or UI  
- 🔄 Push updates to GitHub and watch Argo CD auto-sync to GKE  
- 🧠 Explore GitOps workflow via Argo CD dashboard
