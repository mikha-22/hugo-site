---
title: "Welcome to Milenika's Homelab"
date: 2025-07-30
draft: false
description: "A technical blog documenting the creation and automation of a modern homelab using Kubernetes, GitOps, and Infrastructure as Code."
---

# A Journey in Automation

This site serves as the digital logbook for my personal cloud infrastructure. Here, I document the process of building a fully automated, production-grade homelab from the ground up. The core philosophy is to manage everything as code, from the virtualized infrastructure to the applications and this very website.

This project is a continuous exploration of DevOps principles and cloud-native technologies in a self-hosted environment.

## The Core Technology Stack

The entire homelab is built upon a layered architecture, with each component managed declaratively through Git.

### Infrastructure Layer
The foundation is provisioned using Infrastructure as Code to ensure reproducibility and consistency.
- **Virtualization**: Proxmox VE Cluster
- **Orchestration**: K3s (A lightweight, certified Kubernetes distribution)
- **Provisioning**: Terraform
- **Secrets Management**: Google Secret Manager & External Secrets Operator

### Application & GitOps Layer
Services are deployed and managed using a GitOps workflow, ensuring the cluster's state always matches the configuration in the repository.
- **Continuous Delivery**: ArgoCD (App of Apps pattern)
- **Package Management**: Helm
- **Ingress & Networking**: Traefik & Cloudflare Tunnel
- **Object Storage**: MinIO
- **Web Server**: NGINX

### Content & Delivery Pipeline
This website is built and deployed automatically whenever new content is pushed to the main branch.
- **Static Site Generator**: Hugo
- **CI/CD Automation**: GitHub Actions

## What You'll Find Here

This blog is a place to share knowledge gained throughout this project. You can expect to find:

- Step-by-step tutorials on setting up infrastructure with Terraform and Proxmox.
- Detailed guides for deploying applications on Kubernetes with ArgoCD.
- Insights into building a robust observability stack for a homelab environment.
- Discussions on CI/CD pipelines and practical GitOps workflows.

This project is constantly evolving. Explore the [latest posts](/posts/) to follow the journey, or learn more [about the project](/about/).
