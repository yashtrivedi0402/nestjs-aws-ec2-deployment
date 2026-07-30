# 🚀 NestJS Backend Deployment on AWS EC2

This repository documents my attempt to deploy a **NestJS backend application** on an **AWS EC2 Ubuntu 24.04** server as part of a DevOps practical assignment.

The project covers Linux server configuration, Docker installation, Node.js setup, Nginx installation, AWS Security Group configuration, backend deployment, and the troubleshooting performed during the deployment process.

> **Note:** This repository focuses on documenting the complete deployment workflow, the commands used, challenges encountered, and the lessons learned throughout the assignment.

---

# 🎯 Objectives

- Launch an AWS EC2 Ubuntu server
- Configure the Linux server
- Install and verify Nginx
- Install Node.js and npm
- Install Docker
- Deploy a NestJS backend application
- Configure environment variables
- Run the application on port **9001**
- Configure Nginx as a reverse proxy
- Document the troubleshooting process

---

# 🛠️ Tech Stack

- AWS EC2
- Ubuntu 24.04 LTS
- Linux
- Nginx
- Node.js
- npm
- Docker
- Docker Compose
- NestJS
- PostgreSQL
- Redis

---

# 📂 Repository Structure

```text
.
├── ASSIGNMENT.md
├── README.md
├── 01-AWS-Setup
├── 02-Linux-Server-Setup
├── 03-Backend-Deployment
├── 04-Nginx-Reverse-Proxy
└── 05-Troubleshooting
```

---
---

# 🏗️ Deployment Architecture

```text
                    Internet
                        │
                        ▼
                 AWS Security Group
              (22, 80, 443 Allowed)
                        │
                        ▼
                 AWS EC2 Instance
                 Ubuntu 24.04 LTS
                        │
                        ▼
                     Nginx
               (Reverse Proxy)
                        │
                        ▼
             NestJS Backend (9001)
                  │            │
                  ▼            ▼
            PostgreSQL      Redis
              (Docker)      (Docker)
```

> **Note:** Due to storage limitations on the AWS Free Tier EC2 instance, the PostgreSQL and Redis containers could not be started successfully, preventing the backend deployment from completing.

---

# 🔄 Deployment Workflow

```text
Start
  │
  ▼
Launch EC2 Instance
  │
  ▼
Configure Security Group
  │
  ▼
Connect via SSH
  │
  ▼
Update Ubuntu
  │
  ▼
Install Nginx
  │
  ▼
Install Node.js
  │
  ▼
Install Docker
  │
  ▼
Download Backend Project
  │
  ▼
Configure Environment Variables
  │
  ▼
Install Dependencies
  │
  ▼
Start PostgreSQL & Redis
  │
  ▼
Run NestJS Application
  │
  ▼
Troubleshoot Deployment Issues
  │
  ▼
Document Findings & Learnings
```

---

# 📖 Documentation

| Section | Description |
|----------|-------------|
| 01-AWS-Setup | EC2 instance creation, SSH configuration, and Security Groups |
| 02-Linux-Server-Setup | Ubuntu configuration, Nginx, Node.js, Docker, and Linux monitoring commands |
| 03-Backend-Deployment | Backend deployment steps, dependency installation, environment configuration, and application setup |
| 04-Nginx-Reverse-Proxy | Reverse proxy configuration and request flow |
| 05-Troubleshooting | Deployment issues, debugging process, root cause analysis, and lessons learned |

---

# ⚠️ Challenges Faced

While deploying the backend, I encountered storage limitations on the AWS Free Tier EC2 instance. The required Docker containers for PostgreSQL and Redis could not start because the root volume became full during the deployment.

To troubleshoot the issue, I:

- Investigated disk usage using Linux commands.
- Created a temporary swap file to complete dependency installation.
- Checked Docker storage usage.
- Cleaned unnecessary files.
- Verified system resources and service status.

Although the backend deployment could not be completed due to the EC2 storage limitation, the troubleshooting process helped me better understand Linux resource management, Docker storage, and deployment debugging.

---

# 📚 Key Learnings

- AWS EC2 provisioning
- Ubuntu server administration
- Nginx installation and verification
- Node.js environment setup
- Docker installation and configuration
- Linux monitoring commands
- AWS Security Group configuration
- Backend deployment workflow
- Troubleshooting memory and storage issues
- Working with Docker containers in resource-constrained environments

---

# 📌 Assignment

The original assignment is available in **ASSIGNMENT.md**.

---

## 👨‍💻 Author

**Yash Trivedi**

Aspiring DevOps & Cloud Engineer
