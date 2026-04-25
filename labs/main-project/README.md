# Main Project

## What This Is

The main project is the capstone of this learning lab. It assembles every technology learned in the individual labs into a single, coherent, production-grade infrastructure deployment.

This is the project that replaces professional experience in job applications. A recruiter or engineer who reads this README and explores this folder should understand exactly what was built, why each decision was made, and how to reproduce everything from scratch.

## Architecture

A complete AWS infrastructure including:

- VPC with public and private subnets
- EC2 instances or ECS Fargate for compute
- S3 for storage
- RDS or DynamoDB for data
- All deployed via Terraform
- All servers configured via Ansible
- Applications containerized with Docker
- Orchestrated with Kubernetes on AWS EKS
- Monitored with Prometheus and Grafana
- Deployed automatically via GitHub Actions CI/CD pipeline
- Automated with Python boto3 scripts

## Prerequisites

All individual labs completed:
- linux-basics/
- python-scripts/
- terraform-basics/
- terraform-advanced/
- ansible-basics/
- docker-kubernetes/
- monitoring-prometheus-grafana/
- cicd-github-actions/

## Status

Not started — will be built after individual labs are completed.

## Documentation

Full architecture diagrams, decision records, and reproduction instructions will be added here as the project is built.