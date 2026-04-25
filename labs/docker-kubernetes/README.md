# Docker and Kubernetes

## Why Docker

Docker packages applications and their dependencies into containers — isolated, lightweight, and portable units that run identically everywhere. A containerized application runs the same way on your laptop, on a test server, and in production on AWS. Docker is present in 90% of junior cloud/DevOps job postings.

## Why Kubernetes

Kubernetes orchestrates containers at scale. When you have dozens or hundreds of containers to deploy, scale, update, and monitor, Kubernetes manages all of that automatically. It is the standard for running containerized workloads in production. AWS offers it as EKS (Elastic Kubernetes Service).

## What This Lab Covers

- Docker: building images, running containers, Docker Compose
- Pushing images to AWS ECR (Elastic Container Registry)
- Running containers on AWS ECS Fargate
- Kubernetes: deploying applications, scaling, services, ingress
- AWS EKS cluster setup and management
- Helm charts for Kubernetes package management

## Prerequisites

- terraform-basics/ lab completed
- AWS account configured

## Progress

- [ ] Docker installed and first container running
- [ ] First Docker image built from scratch
- [ ] Image pushed to AWS ECR
- [ ] Application running on ECS Fargate
- [ ] Minikube local Kubernetes cluster running
- [ ] First application deployed on Kubernetes
- [ ] AWS EKS cluster deployed via Terraform
- [ ] Helm chart used for deployment

## Files

Dockerfiles, Kubernetes manifests, and Helm charts will be added here.