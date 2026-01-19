# GitOps Repository – Kubernetes Deployment for AWS EKS

This repository follows the **GitOps approach** to manage and deploy Kubernetes resources on an **AWS EKS cluster** using **ArgoCD**.  
All deployment changes are automated and driven by Git commits made by the Jenkins CD pipeline.

---

## Purpose of This Repository

This repository is responsible for:

- Storing **Kubernetes manifests** (Deployment, Service, etc.)
- Acting as the **single source of truth** for application state
- Enabling **automatic deployment** via ArgoCD
- Supporting **fully automated CD** triggered by Jenkins

> ⚠️ No application source code exists in this repository  
> Only Kubernetes configuration and deployment manifests are stored here.

---

## GitOps Workflow (High Level)

1. Jenkins **CI pipeline** builds and pushes a Docker image
2. Jenkins **CD pipeline**:
   - Updates the image tag in `deployment.yaml`
   - Commits and pushes changes to this GitOps repository
3. **ArgoCD** continuously watches this repository
4. ArgoCD detects changes and automatically:
   - Syncs manifests
   - Deploys updated application to **EKS**
   - Self-heals and prunes resources if needed

---

## Repository Structure

```text
.
├── deployment.yaml        # Kubernetes Deployment manifest
├── service.yaml           # Kubernetes Service (LoadBalancer)
├── Jenkinsfile            # CD pipeline (update image tag & push)
└── README.md              # Documentation (this file)
