# 🎮 Tetris Game Deployment with Argo CD on GKE (GitOps)

Deploying a containerized **Tetris game** to **Google Kubernetes Engine (GKE)** using **Argo CD** and the **GitOps** approach.

---

## 🚀 Tech Stack

- GKE (Google Kubernetes Engine)
- Argo CD
- GitHub (for GitOps)
- Docker
- Kubernetes YAML

---

## ⚙️ Setup Instructions

### 1️⃣ Create a GKE Cluster (Standard mode)
> Make sure the GKE cluster is running and ready.

---

### 2️⃣ Connect to GKE and Install Argo CD

```bash
✅ Set project variables
export PROJECT_ID=$PROJECT_ID
export CLUSTER_NAME=$CLUSTER_NAME
export ZONE=$ZONE 

✅ Set GCP project
gcloud config set project $PROJECT_ID

✅  Connect kubectl to the cluster
gcloud container clusters get-credentials $CLUSTER_NAME \
  --zone=$ZONE --project=$PROJECT_ID

✅ Create argocd namespace
kubectl create namespace argocd

✅ Install Argo CD
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

✅ Expose Argo CD via LoadBalancer
kubectl patch svc argocd-server -n argocd \
  -p '{"spec": {"type": "LoadBalancer"}}'

✅ Get Argo CD external IP (wait until assigned)
kubectl get svc argocd-server -n argocd

✅ Get Argo CD admin password
kubectl -n argocd get secret argocd-initial-admin-secret \
  -o jsonpath="{.data.password}" | base64 -d; echo

✅ Access Argo CD
URL: https://<EXTERNAL-IP> External IP from LoadBalancer 
Username: admin
Password: (from the command above)
