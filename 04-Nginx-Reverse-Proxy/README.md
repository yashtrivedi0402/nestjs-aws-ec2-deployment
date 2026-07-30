# Nginx Reverse Proxy

## Overview

Nginx is commonly used as a reverse proxy to forward incoming client requests to backend applications. In this project, the goal was to configure Nginx to forward HTTP requests to the NestJS application running on **port 9001**.

---

# Objective

- Configure Nginx as a reverse proxy
- Forward incoming HTTP requests to the NestJS backend
- Allow users to access the application through the EC2 public IP instead of the application port

---

# Why Use a Reverse Proxy?

A reverse proxy acts as an intermediary between the client and the backend application.

Using Nginx provides several benefits:

- Hides the backend application port from users.
- Handles incoming HTTP requests.
- Improves security.
- Supports SSL/TLS configuration.
- Can be used for load balancing and caching.

---

# Expected Request Flow

```
Client
   │
   ▼
Nginx (Port 80)
   │
   ▼
NestJS Application (Port 9001)
```

---

# Example Configuration

The following is an example Nginx server block that can be used to forward requests to a NestJS application running on port **9001**.

```nginx
server {
    listen 80;

    server_name <EC2_PUBLIC_IP>;

    location / {
        proxy_pass http://127.0.0.1:9001;
        proxy_http_version 1.1;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

---

# Verification Steps

Once the backend application is running successfully, the following steps can be performed:

- Test the Nginx configuration.

```bash
sudo nginx -t
```

- Restart Nginx.

```bash
sudo systemctl restart nginx
```

- Verify the Nginx service.

```bash
sudo systemctl status nginx
```

- Access the application through the EC2 public IP.

```
http://<EC2_PUBLIC_IP>
```

---

# Current Status

The reverse proxy configuration could not be completed because the NestJS backend was not running successfully due to storage limitations on the AWS Free Tier EC2 instance. Since the backend service was unavailable, the reverse proxy could not be tested.

---

# Key Learnings

- Understanding the role of a reverse proxy
- Configuring Nginx to forward requests
- Basic Nginx server block configuration
- Request flow between client, Nginx, and backend application
- Verification steps for Nginx configuration
