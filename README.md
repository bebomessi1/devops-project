# DevOps Project

## Overview

This project demonstrates a basic DevOps workflow for deploying and monitoring a containerized web application.

The project uses:

- Docker for containerization
- Jenkins for CI/CD automation
- Terraform for infrastructure provisioning
- Ansible for environment configuration
- Uptime Kuma for application monitoring
- GitHub for source code management
- Nginx as the web server

---

## Project Structure

```text
devops-project/
├── app/
│   ├── Dockerfile
│   └── index.html
│
├── ansible/
│   ├── inventory
│   └── setup.yml
│
├── terraform/
│   ├── main.tf
│   ├── terraform.tfstate
│   ├── terraform.tfstate.backup
│   └── .terraform.lock.hcl
│
├── jenkins/
│   └── Dockerfile
│
├── Jenkinsfile
├── README.md
└── .gitignore
