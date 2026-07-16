# Docker

## What is Docker?

Docker is a containerization platform that packages an application along with all its dependencies into a **container**.

A container runs consistently across different environments such as:

- Local machine
- Testing server
- Production server
- Cloud platforms

---

## Why Docker?
# Why Use Docker?

Docker solves many problems that developers face while building, testing, and deploying applications.

---

# 1. Consistent Environment

One of the biggest reasons to use Docker is **environment consistency**.

### Without Docker

Developer A

- Node.js 20
- PostgreSQL 16

Application works ✅

Developer B

- Node.js 18
- PostgreSQL 15

Application fails ❌

Production Server

- Different versions

Unexpected errors ❌

### With Docker

Everyone runs the **same Docker image**, so the application behaves identically everywhere.

**Benefit:** "It works on my machine" problem is eliminated.

---

# 2. Easy Project Setup

Without Docker, a new developer must install:

- Node.js
- PostgreSQL
- Redis
- MongoDB
- RabbitMQ
- Nginx
- Environment variables

This can take hours.

With Docker:

```bash
docker compose up
```

Everything starts automatically.

---

# 3. Isolated Applications

Containers are isolated from each other.

Example:

Project A

- Node.js 18
- PostgreSQL 14

Project B

- Node.js 22
- PostgreSQL 17

Both can run on the same machine without conflicts.

---

# 4. Version Management

Different projects often require different software versions.

Without Docker:

- Install multiple versions manually.
- Risk breaking other projects.

With Docker:

Each project uses its own version inside its container.

---

# 5. Easy Deployment

Instead of saying:

> Install Node.js, PostgreSQL, Redis, and configure everything...

You simply provide the Docker image.

The server only needs Docker installed.

---

# 6. Dependency Management

Applications depend on many libraries and services.

Docker packages:

- Application code
- Runtime
- Libraries
- Dependencies
- Configuration

Everything travels together.

---

# 7. Faster Onboarding

New team member joins.

Without Docker:

- Install software
- Configure database
- Fix errors
- Match versions

Time: Several hours

With Docker:

```bash
git clone
docker compose up
```

Application is ready within minutes.

---

# 8. Microservices Support

Modern applications often use multiple services.

Example:

- User Service
- Order Service
- Payment Service
- Notification Service
- PostgreSQL
- Redis

Docker runs each service in its own container while allowing them to communicate.

---

# 9. Lightweight Compared to Virtual Machines

Docker containers:

- Share the host operating system kernel
- Start in seconds
- Consume less RAM
- Require less disk space

This makes them much more efficient than traditional virtual machines.

---

# 10. Easy Scaling

Need more instances?

Docker makes it simple to run multiple containers of the same application.

Example:

```
App Container 1

App Container 2

App Container 3
```

Useful for handling increased traffic.

---

# 11. CI/CD Integration

Docker works well with CI/CD pipelines.

Typical workflow:

Code

↓

GitHub

↓

Build Docker Image

↓

Run Tests

↓

Deploy

This ensures the same image is tested and deployed.

---

# 12. Better Testing

Developers can create clean, temporary environments for testing.

Example:

```bash
docker compose up
```

Run tests.

```bash
docker compose down
```

Everything is removed, leaving no leftover configuration.

---

# 13. Portable Applications

Docker images can run on:

- Windows
- Linux
- macOS
- AWS
- Azure
- Google Cloud
- DigitalOcean

As long as Docker is installed, the application runs the same way.

---

# 14. Simplifies Database Management

Instead of installing PostgreSQL locally:

```bash
docker run postgres
```

You instantly have a PostgreSQL database running in a container.

The same applies to Redis, MongoDB, MySQL, Elasticsearch, and many other services.

---

# 15. Resource Isolation

Docker lets you limit CPU and memory usage for each container.

Example:

- Container A: 1 CPU, 1 GB RAM
- Container B: 2 CPUs, 2 GB RAM

This prevents one application from consuming all system resources.

---

# Real-World Example

Suppose you're building an IAM backend with:

- Node.js
- TypeScript
- PostgreSQL
- Redis
- Prisma

Without Docker:

- Install Node.js
- Install PostgreSQL
- Install Redis
- Configure environment variables
- Ensure correct versions
- Troubleshoot installation issues

With Docker:

```bash
docker compose up
```

Everything starts automatically with the correct versions and configuration.

---

# Summary

Docker is used because it:

- Eliminates "works on my machine" issues.
- Creates consistent development environments.
- Isolates applications and dependencies.
- Simplifies project setup.
- Makes deployments predictable.
- Supports microservices.
- Enables reproducible testing.
- Integrates well with CI/CD.
- Makes applications portable across platforms.
- Improves team collaboration.



-----

# Docker Architecture

## What is Docker Architecture?

Docker Architecture describes how different Docker components work together to build, manage, and run containers.

When you execute a Docker command, multiple components communicate behind the scenes.

---

# Docker Architecture Diagram

```
                +----------------------+
                |    Docker Client     |
                | (CLI / Docker Desktop)|
                +----------+-----------+
                           |
                           | Docker API
                           |
                           v
                +----------------------+
                |    Docker Daemon     |
                |      (dockerd)       |
                +----------+-----------+
                           |
          +----------------+----------------+
          |                                 |
          v                                 v
+----------------------+         +----------------------+
|      Docker Images   |         |   Docker Containers  |
+----------------------+         +----------------------+
                           |
                           v
                  +--------------------+
                  |   Docker Registry  |
                  | (Docker Hub/Private)|
                  +--------------------+
```

---

# Components of Docker Architecture

## 1. Docker Client

The Docker Client is the interface you use to interact with Docker.

Examples:

```bash
docker run nginx
docker build .
docker ps
docker images
```

The client **does not run containers itself**. It sends requests to the Docker Daemon.

---

## 2. Docker Daemon (dockerd)

The Docker Daemon is the background service that performs all Docker operations.

Responsibilities:

- Build images
- Run containers
- Stop containers
- Delete containers
- Manage networks
- Manage volumes
- Pull images
- Push images

Think of it as the "engine" behind Docker.

---

## 3. Docker Images

A Docker Image is a **read-only template** used to create containers.

An image contains:

- Application code
- Runtime (e.g., Node.js)
- Libraries
- Dependencies
- Configuration

Example:

```
Node.js Image

↓

Node.js + Express App Image
```

One image can create many containers.

---

## 4. Docker Containers

A Container is a running instance of an image.

Example:

```
Node Image

↓

Container 1

Container 2

Container 3
```

Each container has its own:

- File system
- Network
- Processes

Containers are isolated from one another.

---

## 5. Docker Registry

A Docker Registry stores Docker images.

Examples:

- Docker Hub
- GitHub Container Registry (GHCR)
- Amazon ECR
- Google Artifact Registry
- Azure Container Registry

When an image isn't available locally, Docker pulls it from a registry.

Example:

```bash
docker pull nginx
```

---

# How Docker Works

Suppose you run:

```bash
docker run nginx
```

### Step 1

The Docker Client sends the command to the Docker Daemon.

↓

### Step 2

The Docker Daemon checks if the `nginx` image exists locally.

↓

### Step 3

If the image is missing, Docker downloads it from Docker Hub.

↓

### Step 4

Docker creates a new container from the image.

↓

### Step 5

The container starts running.

↓

### Step 6

Your application becomes available.

---

# Request Flow

```
User

↓

docker run nginx

↓

Docker Client

↓

Docker Daemon

↓

Check Local Image

↓

Image Found?
      |
   Yes|No
      |
      |-------- Download from Docker Hub

↓

Create Container

↓

Run Container

↓

Application Running
```

---

# Docker Architecture in Real Projects

Example: IAM Backend

```
Developer

↓

docker compose up

↓

Docker Client

↓

Docker Daemon

↓

Starts:

- Backend Container
- PostgreSQL Container
- Redis Container

↓

Containers communicate through Docker Network

↓

Application Ready
```

---

# Why Docker Uses a Client-Server Architecture

- The Docker Client provides a simple interface for users.
- The Docker Daemon performs all heavy operations.
- Multiple clients can communicate with the same Docker Daemon.
- Docker Desktop, the CLI, and APIs all interact with the same daemon.

---

# Interview Questions

### What is Docker Architecture?

Docker Architecture is a client-server architecture where the Docker Client sends commands to the Docker Daemon, which manages images, containers, networks, and volumes.

---

### What is the Docker Client?

The Docker Client is the command-line interface (CLI) or Docker Desktop that users interact with to send commands to the Docker Daemon.

---

### What is the Docker Daemon?

The Docker Daemon (`dockerd`) is the background service responsible for building images, creating containers, managing networks, volumes, and communicating with registries.

---

### What is a Docker Registry?

A Docker Registry is a repository used to store and distribute Docker images, such as Docker Hub or a private registry.

---

### What happens when you run `docker run nginx`?

1. The Docker Client sends the command to the Docker Daemon.
2. The Daemon checks for the image locally.
3. If the image is not found, it downloads it from a registry.
4. A container is created from the image.
5. The container starts running.


# Docker Installation & Setup

## What is Docker Installation?

Installing Docker means installing the Docker Engine and tools required to:

- Create images
- Run containers
- Manage networks
- Manage volumes

---

# Docker Components Installed

When you install Docker Desktop/Engine, you get:

## 1. Docker Engine

The core runtime that runs containers.

Responsible for:

- Creating containers
- Starting/stopping containers
- Managing images
- Managing networks

---

## 2. Docker CLI

Command-line interface used to interact with Docker.

Example:

```bash
docker run nginx
```

---

## 3. Docker Compose

Tool used to run multiple containers together.

Example:

A backend project:

```
Backend API
+
PostgreSQL
+
Redis
```

can be started using:

```bash
docker compose up
```

---

# Installing Docker on Windows

## Requirements

Before installation:

- Windows 10/11 64-bit
- WSL 2 enabled
- Virtualization enabled in BIOS
- Minimum 4GB RAM recommended

---

## Step 1: Install WSL 2

Open PowerShell as Administrator:

```powershell
wsl --install
```

Restart your computer.

Check:

```powershell
wsl --version
```

---

## Step 2: Install Docker Desktop

Download and install Docker Desktop.

During installation:

Enable:

```
Use WSL 2 based engine
```

Restart after installation.

---

## Step 3: Verify Installation

Open terminal:

```bash
docker --version
```

Example:

```
Docker version 28.x.x
```

---

Check Docker information:

```bash
docker info
```

Output contains:

- Containers
- Images
- Server information
- Storage driver

---

# Test Docker Installation

Run:

```bash
docker run hello-world
```

What happens?

1. Docker searches for `hello-world` image.
2. If not available, downloads it.
3. Creates a container.
4. Runs the container.
5. Shows success message.

---

# Docker Desktop Dashboard

Docker Desktop provides a GUI to manage:

## Containers

View:

- Running containers
- Stopped containers
- Logs

---

## Images

View downloaded images.

Example:

```
nginx
postgres
redis
node
```

---

## Volumes

Manage persistent data.

Example:

```
PostgreSQL database files
```

---

## Networks

Manage communication between containers.

---

# Basic Docker Commands After Installation

## Check Docker Version

```bash
docker version
```

Shows:

Client version

+

Server version

---

## Docker System Information

```bash
docker info
```

---

## Docker Help

```bash
docker help
```

or

```bash
docker command --help
```

Example:

```bash
docker run --help
```

---

# Docker Service Check

Linux:

```bash
systemctl status docker
```

Start Docker:

```bash
sudo systemctl start docker
```

---

# Docker Login

To access private images:

```bash
docker login
```

You provide:

- Docker Hub username
- Password/token

---

# Docker Logout

```bash
docker logout
```

---

# Docker Installation Troubleshooting

## Problem: Docker command not found

Solution:

- Restart terminal
- Check Docker installation
- Add Docker to PATH

---

## Problem: Docker daemon not running

Error:

```
Cannot connect to Docker daemon
```

Solution:

Start Docker Desktop.

---

## Problem: WSL issue

Check:

```powershell
wsl --status
```

Update:

```powershell
wsl --update
```

---

# Real Backend Developer Setup

For Node.js + TypeScript Backend:

Install:

```
Docker Desktop

        |

        ↓

Docker Engine

        |

        ↓

Docker Compose

        |

        ↓

Run:

Node.js Container
PostgreSQL Container
Redis Container
```

---

# Interview Questions

## How do you verify Docker installation?

Using:

```bash
docker --version
```

and

```bash
docker run hello-world
```

---

## What is Docker Desktop?

Docker Desktop is an application that provides Docker Engine, CLI, Compose, and GUI tools for Windows and macOS.

---

## Why is WSL 2 required on Windows?

Because Docker containers use Linux kernel features, and WSL 2 provides a lightweight Linux environment.

---

## Difference between Docker Engine and Docker Desktop?

Docker Engine:
- Core runtime
- Runs containers

Docker Desktop:
- GUI application
- Includes Docker Engine, CLI, Compose, and Kubernetes support



# Docker Images

## What is a Docker Image?

A Docker Image is a **read-only template** used to create Docker containers.

It contains everything required to run an application:

- Application code
- Runtime environment
- System libraries
- Dependencies
- Configuration files

Think of an image as a **blueprint** and a container as the **running house**.

```
Docker Image
      |
      |
      v
Docker Container
```

---

# Real Example

Suppose you have a Node.js application.

Without Docker:

You need:

```
Install Node.js
Install npm packages
Copy project files
Configure environment
Run application
```

With Docker Image:

```
Node.js Runtime
+
Application Code
+
Dependencies
+
Configuration

        ↓

     Docker Image

        ↓

     Container
```

---

# Image vs Container

| Docker Image | Docker Container |
|---|---|
| Blueprint/template | Running instance |
| Read-only | Writable layer |
| Stored locally | Runs as a process |
| Created using Dockerfile | Created from an image |
| Cannot execute directly | Executes application |

Example:

```
nginx Image

       ↓

nginx Container 1

nginx Container 2

nginx Container 3
```

One image can create multiple containers.

---

# Docker Image Layers

Docker images are built using multiple layers.

Example:

```
Application Image

Layer 5:
Application Code

Layer 4:
npm dependencies

Layer 3:
Node.js

Layer 2:
Linux libraries

Layer 1:
Base Operating System
```

Each layer is cached.

---

# Why Layers Matter?

## Faster Builds

If only your code changes:

Docker does not rebuild everything.

It reuses existing layers.

---

## Less Storage

Common layers are shared between images.

Example:

```
Node Image

        +

React App Image

        +

Express App Image
```

All can share the same Node.js layer.

---

# Image Repository

Images are stored in repositories.

Examples:

- Docker Hub
- Private Registry
- Cloud Registry

Example:

```
docker.io/library/nginx
```

Structure:

```
Registry
    |
    |
 Repository
    |
    |
 Image
```

---

# Pulling Images

Download an image from Docker Hub:

```bash
docker pull nginx
```

Docker downloads:

```
nginx image

↓

Local Machine
```

---

# List Images

Show all downloaded images:

```bash
docker images
```

Example output:

```
REPOSITORY     TAG       IMAGE ID
nginx          latest    abc123
node           22        xyz456
postgres       16        pqr789
```

---

# Image Information

Inspect an image:

```bash
docker inspect nginx
```

Shows:

- Layers
- Configuration
- Environment variables
- Architecture

---

# Remove Images

Remove an image:

```bash
docker rmi nginx
```

Remove unused images:

```bash
docker image prune
```

---

# Image Tags

A tag identifies different versions of an image.

Example:

```
node:22

node:20

node:18
```

Format:

```
image_name:version
```

Example:

```bash
docker pull node:22
```

---

# Latest Tag

If you don't specify a tag:

```bash
docker pull nginx
```

Docker uses:

```
nginx:latest
```

Example:

```bash
docker pull nginx:latest
```

---

# Creating Your Own Image

Custom images are created using:

```
Dockerfile
```

Example:

Project:

```
my-api

 |
 |-- server.js
 |-- package.json
 |-- Dockerfile
```

Dockerfile:

```dockerfile
FROM node:22

WORKDIR /app

COPY package*.json .

RUN npm install

COPY . .

CMD ["npm","start"]
```

Build image:

```bash
docker build -t my-api .
```

Result:

```
my-api Image
```

---

# Running Custom Image

Create container:

```bash
docker run my-api
```

Flow:

```
Dockerfile

      ↓

Docker Build

      ↓

Docker Image

      ↓

Docker Run

      ↓

Container
```

---

# Common Image Commands

## Pull Image

```bash
docker pull image_name
```

Example:

```bash
docker pull redis
```

---

## List Images

```bash
docker images
```

---

## Remove Image

```bash
docker rmi image_name
```

---

## Image History

Shows image layers:

```bash
docker history nginx
```

---

## Inspect Image

```bash
docker inspect nginx
```

---

# Practical Backend Example

IAM Backend Project:

Technology:

```
Node.js
TypeScript
Express
PostgreSQL
Redis
Prisma
```

Images required:

```
node:22

postgres:16

redis:7
```

Architecture:

```
        Docker Compose

              |

   ----------------------

   Node Container

   PostgreSQL Container

   Redis Container

   ----------------------

              |

        Application
```

---

# Interview Questions

## What is a Docker Image?

A Docker Image is a read-only template containing application code, dependencies, libraries, and configuration required to create containers.

---

## How are Docker Images created?

Docker images are created using a Dockerfile and the `docker build` command.

Example:

```bash
docker build -t app-name .
```

---

## What are Docker Image Layers?

Layers are independent read-only filesystem changes that make up a Docker image. Layers improve caching and reduce storage usage.

---

## Difference between Image and Container?

An image is a blueprint, while a container is a running instance of that image.

---

## What happens when you run docker pull nginx?

Docker downloads the nginx image from a registry and stores it locally.


