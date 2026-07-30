# Troubleshooting

## Overview

During the deployment process, several issues were encountered while setting up and running the NestJS application on an AWS Free Tier EC2 instance.

This document summarizes the problems, their root causes, the troubleshooting steps performed, and the outcomes.

---

# Issue 1 – Low Memory During Dependency Installation

## Problem

While installing the project dependencies using `npm install`, the EC2 instance ran out of available memory.

## Root Cause

The AWS Free Tier instance had limited RAM, causing the installation process to fail.

## Troubleshooting

A temporary swap file was created to provide additional virtual memory and allow the installation to complete.

## Outcome

The dependencies were installed successfully.

---

# Issue 2 – Docker Compose Command Not Found

## Problem

The initial Docker Compose command failed because the expected command was not available.

## Root Cause

The Docker Compose installation differed from the command used by the project documentation.

## Troubleshooting

Verified the installed Docker version and used the appropriate Docker Compose command supported by the environment.

## Outcome

Docker Compose commands were executed successfully.

---

# Issue 3 – Docker Image Pull Failure

## Problem

Docker was unable to download the required PostgreSQL and Redis images.

## Root Cause

The root filesystem ran out of available storage during the image download process.

## Troubleshooting

Disk usage was inspected using:

```bash
df -h
```

Docker storage usage and system resources were also reviewed to identify the storage bottleneck.

## Outcome

The issue was confirmed to be insufficient disk space.

---

# Issue 4 – No Space Left on Device

## Problem

Several commands failed with a **"No space left on device"** error.

## Root Cause

The default storage allocated to the EC2 Free Tier instance was insufficient for the application, dependencies, and Docker images.

## Troubleshooting

The following actions were performed:

- Checked disk usage
- Identified large files
- Removed the temporary swap file after it was no longer required
- Verified available storage before retrying the deployment

## Outcome

Some storage was recovered, but not enough to complete the backend deployment.

---

# Issue 5 – Backend Could Not Start

## Problem

The NestJS application could not connect to the required database services.

## Root Cause

PostgreSQL and Redis containers could not start because Docker images could not be fully downloaded due to storage limitations.

## Troubleshooting

- Verified Docker installation
- Checked running containers
- Reviewed application logs
- Confirmed environment variables
- Verified available system resources

## Outcome

The backend could not be started because the required services were unavailable.

---

# Linux Commands Used

| Purpose | Command |
|----------|---------|
| Check disk usage | `df -h` |
| Check memory | `free -h` |
| Monitor processes | `top` |
| View Docker containers | `docker ps -a` |
| View Docker images | `docker images` |
| Check Docker service | `systemctl status docker` |
| Check Nginx service | `systemctl status nginx` |

---

# Lessons Learned

- Always verify available disk space before deploying containerized applications.
- Free Tier instances have limited memory and storage that can affect deployment.
- Swap memory can help during dependency installation but is not a substitute for sufficient disk space.
- Checking system resources early can help identify deployment bottlenecks.
- A structured troubleshooting approach makes it easier to identify and resolve issues.

---

# Summary

Although the backend deployment could not be completed due to the storage limitations of the AWS Free Tier EC2 instance, the troubleshooting process provided valuable hands-on experience with Linux administration, Docker, resource monitoring, and deployment debugging.
