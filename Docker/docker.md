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