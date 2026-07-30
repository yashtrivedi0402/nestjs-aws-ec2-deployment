# Troubleshooting

## Overview

This document summarizes the issues encountered while deploying a **NestJS backend application** on an **AWS Free Tier Ubuntu EC2** instance.

The deployment involved configuring the server, installing dependencies, running Docker services, and starting the backend application. During this process, several infrastructure-related issues were identified and investigated.

Each issue below includes the problem, root cause, troubleshooting steps, and outcome.

---

# Deployment Incident Summary

| Issue | Status |
|--------|--------|
| Low Memory During Dependency Installation | ✅ Resolved |
| Docker Compose Command Issue | ✅ Resolved |
| Docker Image Pull Failure | ❌ Blocked by Storage |
| No Space Left on Device | ⚠️ Partially Resolved |
| Backend Startup Failure | ❌ Not Resolved |

---

# Issue 1 – Low Memory During Dependency Installation

## Problem

The `npm install` process failed because the EC2 instance ran out of available memory.

## Root Cause

The AWS Free Tier instance has limited RAM, which was insufficient for installing all project dependencies.

## Troubleshooting

To provide additional virtual memory, a temporary swap file was created.

This allowed the dependency installation to complete successfully.

## Outcome

✅ Project dependencies were installed successfully.

---

# Issue 2 – Docker Compose Command

## Problem

The Docker Compose command initially failed because the expected command was unavailable.

## Root Cause

The installed Docker version used a different Docker Compose implementation than the one referenced in the project documentation.

## Troubleshooting

Verified the installed Docker version.

```bash
docker --version

docker compose version
```

Used the Docker Compose command supported by the installed version.

## Outcome

✅ Docker Compose was working correctly after using the appropriate command.

---

# Issue 3 – Docker Image Pull Failure

## Problem

Docker failed to download the PostgreSQL and Redis images.

## Root Cause

The EC2 root filesystem ran out of available storage while downloading Docker images.

## Troubleshooting

Verified available disk space.

```bash
df -h
```

Reviewed Docker storage usage.

```bash
docker images

docker system df
```

Confirmed that the storage limitation was preventing the image download.

## Outcome

❌ Docker images could not be downloaded because of insufficient disk space.

---

# Issue 4 – No Space Left on Device

## Problem

Several commands failed with the following error:

```text
No space left on device
```

## Root Cause

The default storage allocated to the AWS Free Tier EC2 instance was not sufficient for:

- Project dependencies
- Docker images
- Temporary files
- Swap file

## Troubleshooting

Performed the following steps:

- Checked filesystem usage

```bash
df -h
```

- Checked memory usage

```bash
free -h
```

- Removed the temporary swap file after installation.

- Rechecked available storage before retrying the deployment.

## Outcome

⚠️ Some storage was recovered, but not enough to complete the deployment.

---

# Issue 5 – Backend Could Not Start

## Problem

The NestJS application failed to start because it could not connect to the required database services.

## Root Cause

The PostgreSQL and Redis Docker containers were unavailable because their images could not be downloaded successfully.

As a result:

- PostgreSQL was unavailable
- Redis was unavailable
- Prisma could not establish a database connection
- Backend startup failed

## Troubleshooting

Verified Docker installation.

```bash
docker ps -a

docker images

systemctl status docker
```

Verified application configuration and available system resources.

## Outcome

❌ The backend application could not be started.

---

# Useful Linux Commands

| Purpose | Command |
|----------|---------|
| Check disk usage | `df -h` |
| Check memory usage | `free -h` |
| Monitor running processes | `top` |
| View Docker containers | `docker ps -a` |
| View Docker images | `docker images` |
| View Docker storage usage | `docker system df` |
| Check Docker service | `systemctl status docker` |
| Check Nginx service | `systemctl status nginx` |

---

# Lessons Learned

- Always verify available storage before deploying containerized applications.
- AWS Free Tier instances have limited compute and storage resources.
- Temporary swap memory can help complete memory-intensive tasks such as dependency installation.
- Docker images require sufficient free disk space before containers can be created.
- Monitoring system resources early helps identify infrastructure bottlenecks faster.
- A structured troubleshooting approach makes deployment issues easier to diagnose and document.

---

# Conclusion

Although the backend deployment could not be completed because of the storage limitations of the AWS Free Tier EC2 instance, the troubleshooting process provided valuable hands-on experience with:

- Linux system administration
- Docker troubleshooting
- Resource monitoring
- Memory management
- Storage analysis
- Deployment debugging

The experience reinforced the importance of systematically identifying root causes before attempting corrective actions.
