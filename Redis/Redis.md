# Redis Notes

## Table of Contents
1. Introduction
2. Why Redis?
3. Installation
4. Redis Architecture
5. Data Types
6. Commands
7. Expiration
8. Persistence
9. Transactions
10. Pub/Sub
11. Streams
12. Caching
13. Rate Limiting
14. Distributed Lock
15. Interview Questions
16. Best Practices
17. Useful Resources


# Introduction to Redis

## What is Redis?

Redis (Remote Dictionary Server) is an open-source, in-memory NoSQL data store.
In the other words,
Redis is an open-source, in-memory data store that is commonly used as a cache, database, message broker, and streaming engine. Because it stores data primarily in RAM, Redis is extremely fast—typically handling operations in microseconds.

It can be used as:

- Database
- Cache
- Message Broker
- Queue
- Session Store
- Real-time Analytics Store

## Features

- Extremely Fast (microseconds)
- In-memory storage
- Supports multiple data structures
- Persistence support
- Replication
- Clustering
- Pub/Sub
- Lua scripting

## Why Redis?

Traditional databases read/write from disk.

Redis stores data in RAM.

RAM is much faster than disk.

Result:
- Low latency
- High throughput
- Excellent for caching

## Real-world Uses

- Authentication sessions
- OTP storage
- API caching
- Leaderboards
- Chat applications
- Rate limiting
- Shopping carts


[Src](https://www.youtube.com/watch?v=Vx2zPMPvmug&t=785s)