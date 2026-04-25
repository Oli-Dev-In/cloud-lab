# Terraform Basics

## Why Terraform

Terraform is the industry-standard Infrastructure as Code tool. Instead of creating AWS resources manually through the console, you write code that describes exactly what infrastructure you want — and Terraform builds it, modifies it, or destroys it automatically.

This matters for three reasons. First, reproducibility — anyone can take this code and recreate the exact same infrastructure from scratch. Second, version control — infrastructure changes are tracked in Git like any other code. Third, professionalism — clicking around in the AWS console is not how production infrastructure is managed. Every deployment in this lab uses Terraform.

## What This Lab Covers

- Terraform core workflow: init, plan, apply, destroy
- Providers and resources
- Variables and outputs
- State management
- First AWS deployments: EC2, S3, VPC, IAM

## Prerequisites

- AWS account with Free Tier
- AWS CLI installed and configured
- Terraform installed

## Progress

- [ ] Terraform installed
- [ ] First configuration written (provider block)
- [ ] First resource deployed (S3 bucket)
- [ ] EC2 instance deployed via Terraform
- [ ] VPC and networking configured via Terraform
- [ ] Variables and outputs implemented
- [ ] Remote state on S3 configured

## Files

Terraform configurations will be added here as they are built.