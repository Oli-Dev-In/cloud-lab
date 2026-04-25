# Ansible Basics

## Why Ansible

Terraform creates infrastructure — Ansible configures it. Once Terraform has deployed a server on AWS, Ansible connects to it and installs packages, creates users, configures firewalls, sets up monitoring agents, and anything else needed to make it production-ready.

Ansible appears in 60% of junior cloud/DevOps job postings. It is agentless — it connects via SSH and requires nothing installed on the target server. Configurations are written in YAML files called playbooks.

## What This Lab Covers

- Ansible installation and configuration
- Inventory files — telling Ansible which servers to manage
- Playbooks — sequences of tasks to execute on servers
- Roles — reusable Ansible components
- Configuring a Linux server from scratch via Ansible

## Prerequisites

- linux-basics/ lab completed
- terraform-basics/ lab completed (servers to configure)

## Progress

- [ ] Ansible installed
- [ ] First inventory file written
- [ ] First playbook written and executed
- [ ] Full server configuration playbook (packages, users, firewall, monitoring agent)
- [ ] Ansible integrated with Terraform-deployed infrastructure

## Files

Playbooks will be added here as they are written and tested.