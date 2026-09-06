# kubernetes-argo-eks

A minimal GitOps demo that packages a static web app in Docker and deploys it to Amazon EKS using ArgoCD.

## Overview

This repository contains:

- a simple NGINX-based web application in `src/`
- a Docker image definition in `Dockerfile`
- Kubernetes manifests in `k8s/` for deployment and service exposure
- a GitOps workflow where ArgoCD watches the `k8s/` directory and syncs changes to the cluster

## Repository structure

```text
.
├── Dockerfile
├── README.md
├── k8s/
│   ├── deployment.yaml
│   └── service.yaml
└── src/
    └── index.html
```

## Prerequisites

- Docker installed locally
- Access to a container registry (for example Docker Hub)
- An Amazon EKS cluster
- ArgoCD installed and configured to manage this repository

## Build the container image

```bash
docker build -t <your-dockerhub-user>/kubernetes-argo-eks:v1 .
docker push <your-dockerhub-user>/kubernetes-argo-eks:v1
```

Update the image value in `k8s/deployment.yaml` to match the registry and tag you pushed.

## Deploy to Kubernetes

Apply the manifests directly if you want a quick test:

```bash
kubectl apply -f k8s/
```

This creates a Deployment with 2 replicas and a LoadBalancer Service exposing the app on port 80.

## Deploy via ArgoCD

Create an ArgoCD Application with the following settings:

- Repository: this Git repository
- Path: `k8s`
- Destination: your EKS cluster
- Namespace: `default`

ArgoCD will automatically reconcile the resources defined in `k8s/` and keep the cluster state aligned with the Git repo.

## Verify the app

After the Service is ready, retrieve the external address:

```bash
kubectl get svc
```

Then open the LoadBalancer hostname or IP in a browser to confirm the app is running.

## Notes

The app is intentionally simple and is designed as a starting point for a Kubernetes + GitOps demo. You can replace the static page content in `src/index.html` and commit the change to trigger an ArgoCD sync.
