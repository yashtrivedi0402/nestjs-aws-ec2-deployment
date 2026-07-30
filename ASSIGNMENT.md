# DevOps Practical Assignment

This repository contains my implementation and documentation for the DevOps practical assignment. The objective of this assignment was to deploy a NestJS backend application on an AWS EC2 Ubuntu server while performing Linux server setup, backend deployment, and web server configuration.

---

## AWS Setup

1. Create an AWS Free Tier account.
2. Launch an Ubuntu EC2 instance using a Free Tier eligible instance type.
3. Set the EC2 instance name as **devops-task-server**.
4. Configure an SSH key pair and connect to the server using SSH.

---

## Task 1 – Linux Server Setup

5. Set up and configure the Ubuntu Linux server.
6. Install and verify Nginx.
7. Install and verify Node.js and npm.
8. Install and verify Docker.
9. Share the Ubuntu commands used to check:
   - CPU usage/details
   - RAM usage
   - Disk usage
   - Running services
   - Open/listening ports
10. Configure the required AWS Security Group/firewall ports and mention the port number, protocol, and purpose of each port.

---

## Task 2 – Backend Deployment

11. Clone the provided backend repository.  [https://drive.google.com/file/d/1x1bpkQ1UxxHn9IkDqBwrXH5MD4Z0cTTM/view?usp=sharing]
12. Install all required dependencies.
13. Configure the required environment variables.
14. Run the NestJS backend on port **9001**.
15. Make sure the application keeps running after the SSH session is closed.
16. Configure Nginx as a reverse proxy for the backend.
17. Verify the API documentation endpoint:

```
http://127.0.0.1:9001/api-spec
```

18. Make the API accessible through the EC2 server's public IP or domain.

---

## Repository Structure

- **01-AWS-Setup** – AWS EC2 instance creation and SSH configuration.
- **02-Linux-Server-Setup** – Linux configuration, package installation, Docker, Node.js, and Nginx setup.
- **03-Backend-Deployment** – Backend deployment process and environment configuration.
- **04-Nginx-Reverse-Proxy** – Reverse proxy configuration and request flow.
- **05-Troubleshooting** – Issues encountered, debugging steps, and lessons learned.

---

> **Note:** This repository documents my implementation, learning process, troubleshooting, and observations while working on the assignment.
