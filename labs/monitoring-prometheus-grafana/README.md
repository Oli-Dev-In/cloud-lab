# Monitoring — Prometheus and Grafana

## Why Monitoring

Deploying infrastructure is only half the job. A Cloud/DevOps engineer must know what is happening inside that infrastructure at all times — CPU usage, memory, request latency, error rates, disk space. Without monitoring, problems are discovered by users, not engineers.

Prometheus collects metrics from infrastructure and applications. Grafana visualizes those metrics in dashboards and triggers alerts when thresholds are exceeded. This stack appears in the majority of junior cloud/DevOps job postings.

## What This Lab Covers

- Prometheus installation and configuration
- Scraping metrics from AWS infrastructure
- Grafana installation and dashboard creation
- Alerting — defining thresholds and notification rules
- Integrating monitoring into the main project infrastructure

## Prerequisites

- terraform-basics/ lab completed
- Linux server running on AWS

## Progress

- [ ] Prometheus deployed on AWS infrastructure
- [ ] Metrics being scraped from EC2 instances
- [ ] Grafana deployed and connected to Prometheus
- [ ] First dashboard created (CPU, memory, disk, network)
- [ ] Alerts configured for critical thresholds
- [ ] Monitoring integrated into main-project/

## Files

Prometheus configurations and Grafana dashboard definitions will be added here.