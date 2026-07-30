# Linux Server Setup

## Overview

After successfully launching the EC2 instance, the next step was to prepare the Ubuntu server for application deployment. This included updating the system, installing the required software, verifying the installations, and checking the overall health of the server.

---

# Objective

- Update the Ubuntu server
- Install Nginx
- Install Node.js and npm
- Install Docker
- Verify all installations
- Monitor server resources

---

# Step 1 – Update Ubuntu

Before installing any software, I updated the package repository and upgraded the existing packages to ensure the system was running the latest available versions.

### Commands

```bash
sudo apt update
sudo apt upgrade -y
```

### Verification

```bash
sudo apt list --upgradable
```

---

# Step 2 – Install Nginx

Nginx was installed to serve as the web server and reverse proxy for the backend application.

### Commands

```bash
sudo apt install nginx -y
```

### Verification

```bash
nginx -v

sudo systemctl status nginx
```

---

# Step 3 – Install Node.js and npm

Node.js provides the JavaScript runtime required to run the NestJS application, while npm is used to install project dependencies.

I installed Node.js using the official installation method and verified both Node.js and npm after installation.

### Verification

```bash
node -v

npm -v
```

---

# Step 4 – Install Docker

Docker was installed to run the PostgreSQL and Redis services required by the backend application.

### Commands

```bash
sudo apt install docker.io -y

sudo systemctl enable docker

sudo systemctl start docker

sudo usermod -aG docker ubuntu

newgrp docker
```

### Verification

```bash
docker --version

docker ps
```

---

# Step 5 – Linux Monitoring Commands

The following commands were used to monitor the health and status of the Ubuntu server.

| Purpose | Command |
|----------|---------|
| CPU Usage | `top` |
| RAM Usage | `free -h` |
| Disk Usage | `df -h` |
| Running Services | `systemctl list-units --type=service --state=running` |
| Open/Listening Ports | `ss -tulnp` |

---

# Verification Summary

The following components were successfully installed and verified.

| Component | Status |
|-----------|--------|
| Ubuntu Updated | ✅ |
| Nginx | ✅ |
| Node.js | ✅ |
| npm | ✅ |
| Docker | ✅ |

---

# Key Learnings

- Updating an Ubuntu server
- Installing software using APT
- Managing Linux services with systemctl
- Installing and configuring Docker
- Adding users to the Docker group
- Monitoring CPU, memory, disk usage, and running services
- Checking listening network ports
