# Backend Deployment

## Overview

The objective of this phase was to deploy the provided NestJS backend application on the Ubuntu EC2 instance. This involved preparing the application, installing the required dependencies, configuring environment variables, and running the backend on port **9001**.

---

# Objective

- Download the backend project
- Install project dependencies
- Configure environment variables
- Run the NestJS application
- Start the required database services
- Verify the application

---

# Step 1 – Download the Backend Project

The backend project was downloaded from the Google Drive link provided in the assignment and extracted on the Ubuntu EC2 instance.

---

# Step 2 – Install Dependencies

After navigating to the project directory, all required Node.js dependencies were installed.

### Command

```bash
npm install
```

During the installation, the EC2 instance ran out of memory. To continue the installation successfully, a temporary swap file was created.

---

# Step 3 – Configure Environment Variables

The required environment variables were configured using the project's `.env` file.

The application was configured to run on:

```env
PORT=9001
```

---

# Step 4 – Database Services

The project required PostgreSQL and Redis containers to be started using Docker Compose.

Example command:

```bash
docker-compose -f docker-compose.dev.yaml up -d postgres redis
```

These services were required before starting the backend application.

---

# Step 5 – Application Startup

After configuring the environment, I attempted to start the NestJS application.

Example commands:

```bash
npm run start:dev
```

or

```bash
npm run start:prod
```

---

# Deployment Challenge

During the deployment process, the AWS Free Tier EC2 instance ran out of available storage while Docker was pulling the required PostgreSQL and Redis images.

This prevented the database containers from starting successfully, which also prevented the NestJS backend from connecting to the database and completing the application startup.

To troubleshoot the issue, I:

- Checked available disk space using `df -h`
- Checked Docker storage usage
- Created a temporary swap file to complete dependency installation
- Investigated Linux storage usage
- Removed the temporary swap file after troubleshooting
- Verified system resources before retrying the deployment

Despite multiple troubleshooting attempts, the deployment could not be completed because of the storage limitation on the EC2 Free Tier instance.

---

# Current Status

| Task | Status |
|------|--------|
| Backend Downloaded | ✅ |
| Dependencies Installed | ✅ |
| Environment Variables Configured | ✅ |
| Docker Installed | ✅ |
| Backend Started | ❌ |
| API Verified | ❌ |

---

# Key Learnings

- Deploying a Node.js/NestJS application on Ubuntu
- Managing project dependencies
- Configuring environment variables
- Understanding Docker Compose services
- Troubleshooting deployment issues
- Diagnosing Linux storage limitations
- Investigating Docker-related deployment failures
