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

##  configuration overview