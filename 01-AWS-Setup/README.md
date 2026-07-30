# AWS EC2 Setup

## Overview

The first step of this project was to prepare the cloud infrastructure required for deploying the backend application. For this assignment, I used an existing AWS Free Tier account and launched a new Ubuntu EC2 instance.

---

# Objective

- Create a Linux server on AWS.
- Configure secure remote access.
- Prepare the server for application deployment.

---

# AWS Resources Used

| Resource | Value |
|----------|-------|
| Cloud Provider | AWS |
| Service | Amazon EC2 |
| Operating System | Ubuntu 24.04 LTS |
| Instance Type | Free Tier Eligible |
| Instance Name | devops-task-server |

---

# Step 1 – Launch EC2 Instance

I launched a new Ubuntu 24.04 EC2 instance from the AWS Management Console and named it:

```
devops-task-server
```

During the instance creation process, I selected a Free Tier eligible instance type and configured the default storage provided by AWS.

---

# Step 2 – Create SSH Key Pair

To securely access the server, I used an SSH key pair.

The private key (`.pem` file) was downloaded during instance creation and stored securely on my local machine.

---

# Step 3 – Configure Security Group

The following inbound rules were configured.

| Port | Protocol | Purpose |
|------|----------|---------|
| 22 | TCP | SSH Remote Access |
| 80 | TCP | HTTP Traffic |
| 443 | TCP | HTTPS Traffic |

---

# Step 4 – Connect to the EC2 Instance

The server was accessed from my local terminal using SSH.

Example:

```bash
ssh -i <key-name>.pem ubuntu@<EC2-Public-IP>
```

After successful authentication, I was able to manage the Ubuntu server remotely.

---

# Verification

The connection was verified by successfully logging into the Ubuntu server through SSH.

---

# Key Learnings

- Creating an EC2 instance
- Understanding Free Tier resources
- Configuring Security Groups
- Using SSH key pairs
- Connecting to a remote Linux server securely
