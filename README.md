# Argo CD Helm Deployment

This repository provides a Helm-based deployment of [Argo CD](https://argo-cd.readthedocs.io/), an open-source tool for Kubernetes GitOps continuous deployment.

## Table of Contents
1. [Prerequisites](#prerequisites)
2. [Repository Structure](#repository-structure)
3. [Configuration Overview](#configuration-overview)
4. [Installation Instructions](#installation-instructions)
5. [Managing Argo CD](#managing-argo-cd)
6. [Uninstallation](#uninstallation)
7. [References](#references)

## Prerequisites

Before deploying Argo CD, ensure you have the following tools installed:

- **Kubernetes Cluster** (EKS, AKS, GKE, etc.)
- **Helm 3.x**: [Installation Guide](https://helm.sh/docs/intro/install/)
- **kubectl**: [Installation Guide](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- **Ingress Controller**: ALB Ingress Controller is required for this deployment

## Repository Structure

```bash
.
├── charts/                # Directory for Helm charts
├── values.yaml            # Custom values for Argo CD installation
└── README.md              # Instructions for setting up Argo CD
```

## Configuration Overview

This deployment leverages a customized values.yaml to define the Argo CD setup:

- **Global Settings: Node selectors, tolerations, and domain configuration.
Custom Resource Definitions (CRDs): Ensures CRDs are installed and retained on uninstall.
- **Ingress: Configured for internal ALB with SSL.
- **Autoscaling: Horizontal Pod Autoscaling (HPA) is enabled for the Argo CD server and repo-server components.
## Key configuration parameters include:

Parameter	Description	Default
global.domain	Base domain for ingress URLs	""
server.autoscaling.enabled	Enable Horizontal Pod Autoscaling for the Argo CD server	true
controller.replicas	Number of replicas for the application controller	2
ingress.annotations	Annotations for ALB ingress (SSL, CIDRs, etc.)	Customizable
redis-ha.enabled	Enable highly available Redis setup	true
For a full list of configurable options, see the Argo CD Helm chart documentation.

## Installation Instructions
1. Add the Argo Helm Repository
First, add the Argo CD Helm chart repository:
```bash
helm repo add argo https://argoproj.github.io/argo-helm
helm repo update
```

2. Install Argo CD
Install Argo CD into your Kubernetes cluster using the customized values.yaml file:

```bash
helm install argocd argo/argo-cd --namespace argocd --create-namespace -f values.yaml
```

This will deploy Argo CD in the argocd namespace using your configurations.

3. Access Argo CD
After installation, access the Argo CD dashboard via the configured domain:

```bash
kubectl get svc -n argocd argocd-server
```
If ingress is configured correctly, the dashboard will be available at https://argocd.<your-domain>.com.

## Managing Argo CD
Access Argo CD UI
To log in to the Argo CD UI, you'll need the initial admin password, which can be retrieved with:

```bash
kubectl get secret -n argocd argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

Use this password with the username admin to access the dashboard.

Sync and Manage Applications
Argo CD allows you to sync and manage Kubernetes applications declaratively through GitOps. Refer to Argo CD Documentation for more details.

## Uninstallation
To uninstall Argo CD from your cluster:

```bash
helm uninstall argocd --namespace argocd
```
Optionally, delete the namespace and any remaining resources:

```bash
kubectl delete namespace argocd
```