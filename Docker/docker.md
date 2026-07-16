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