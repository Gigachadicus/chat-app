# Java Backend Engineering Learning Project

**Version:** 1.0

---

# Table of Contents

1. Project Vision
2. Learning Objectives
3. Project Scope
4. Product Requirements (PRD)
5. Technical Requirements (TRD)
6. Feature Catalogue
7. Milestones
8. Success Criteria
9. Learning Outcomes

---

# 1. Project Vision

## Purpose

Develop a minimal real-time chat application whose primary goal is learning modern Java backend engineering.

The application itself is intentionally simple. Every implemented feature exists because it teaches one or more backend engineering concepts.

---

## Core Philosophy

**Priority**

> Learning > Code Quality > Features

The project is successful if the developer understands **why** each technology exists rather than simply making the application work.

---

## Constraints

| Item | Value |
|------|------|
| Experience | Beginner |
| Time Budget | 3 Days |
| Daily Time | 5 Hours |
| Total Time | ~15 Hours |

---

# 2. Learning Objectives

## Primary Technologies

- Java Socket Programming
- Spring Boot
- Dependency Injection
- PostgreSQL
- Spring Data JPA
- Flyway
- Redis
- Elasticsearch
- BCrypt
- Concurrent Programming
- SLF4J Logging

## Secondary Goals

Understand:

- Layered backend architecture
- Persistence strategies
- Caching
- Search engines
- Authentication flow
- Concurrent client communication

---

# 3. Project Scope

## In Scope

- User Registration
- User Login
- Global Chat Room
- Multiple Concurrent Users
- Message Broadcasting
- Recent Chat History
- Full-text Message Search
- Graceful Disconnect
- Logging

## Out of Scope

- REST API
- GUI
- Spring Security
- JWT
- Docker
- Tests
- Multiple Chat Rooms
- Private Messaging
- File Uploads
- Notifications
- Read Receipts
- Typing Indicators
- Message Editing
- User Profiles
- Administration
- Cloud Deployment

---

# 4. Product Requirements (PRD)

## Product Summary

Develop a minimal console-based chat application supporting authenticated users communicating in a single global chat room.

The application focuses on backend concepts rather than application complexity.

---

## Target User

A developer learning backend engineering.

---

## Functional Requirements

### Authentication

Users shall be able to:

- Register
- Login

Requirements:

- Username must be unique.
- Passwords shall be securely hashed.
- Invalid credentials shall be rejected.
- Only authenticated users may enter the chat.

---

### Global Chat

Authenticated users shall be able to:

- Join the chat
- Send messages
- Receive broadcasts

---

### Recent History

Command

```text
/history
```

Returns the latest 100 chat messages.

---

### Message Search

Command

```text
/search <keyword>
```

Returns matching historical messages.

---

### Disconnect

Command

```text
/quit
```

Gracefully disconnects the client from the server.

---

## User Flow

```text
Start Client
      │
      ▼
Register / Login
      │
      ▼
Join Chat
      │
      ▼
Send Messages
      │
 ┌────┴─────┐
 ▼          ▼
History   Search
      │
      ▼
Quit
```

---

# 5. Technical Requirements (TRD)

## Technology Stack

| Layer | Technology |
|------|------------|
| Language | Java 21 |
| Framework | Spring Boot |
| Build Tool | Gradle |
| Database | PostgreSQL |
| ORM | Spring Data JPA |
| Migration | Flyway |
| Cache | Redis |
| Search | Elasticsearch |
| Networking | TCP Sockets |
| Logging | SLF4J |
| Security | BCrypt |

---

## System Responsibilities

### Spring Boot

Responsible for:

- Application lifecycle
- Dependency Injection
- Configuration
- Layered architecture

---

### TCP Socket Server

Responsible for:

- Accepting clients
- Maintaining socket connections
- Broadcasting messages
- Concurrent communication

---

### PostgreSQL

Stores:

- Persistent user information

---

### Redis

Stores:

- Recent chat history

---

### Elasticsearch

Stores:

- Searchable message documents

---

### BCrypt

Responsible for:

- Password hashing
- Password verification

---

### Logging

Responsible for:

- Application logs
- Connection logs
- Error logs

---

## System Architecture

```text
                 Console Client
                       │
                 TCP Socket
                       │
                       ▼

          +----------------------------+
          |      Spring Boot Server    |
          |----------------------------|
          | Socket Server              |
          | Authentication Service     |
          | Chat Service               |
          | Redis Service              |
          | Search Service             |
          +----------------------------+
              │          │          │
              ▼          ▼          ▼
        PostgreSQL    Redis   Elasticsearch
```

---

## Storage Responsibilities

### PostgreSQL

Persistent data

```text
users

id
username
password_hash
created_at
```

---

### Redis

Temporary data

```text
chat_history

Latest 100 messages
```

---

### Elasticsearch

Search index

```text
messages

username
message
timestamp
```

---

## Suggested Package Structure

```text
config/
socket/
entity/
repository/
service/
dto/
util/
```

---

# 6. Feature Catalogue

Every feature exists to teach at least one backend engineering concept.

| Feature | Why it Exists | Technology Learned |
|---------|---------------|--------------------|
| User Registration | Learn persistence | PostgreSQL + JPA + Flyway |
| Login | Learn authentication | BCrypt + JPA |
| Real-time Chat | Learn networking | TCP Sockets |
| Multiple Clients | Learn concurrency | ExecutorService |
| Broadcast Messages | Learn shared state | ConcurrentHashMap |
| Chat History | Learn caching | Redis Lists |
| Message Search | Learn search engines | Elasticsearch |
| Graceful Disconnect | Learn resource cleanup | Sockets |
| Logging | Learn production practices | SLF4J |

---

## Feature 1 — Register

Flow

```text
Username
    │
    ▼
Password
    │
    ▼
Hash Password
    │
    ▼
Save User
```

### Concepts

- Entity
- Repository
- Service
- Flyway
- BCrypt

---

## Feature 2 — Login

Flow

```text
Username
    │
    ▼
Password
    │
    ▼
Verify Hash
    │
    ▼
Allow Socket Session
```

### Concepts

- Authentication
- Repository lookup
- Password verification

---

## Feature 3 — Global Chat

Flow

```text
Alice
   │
Hello
   │
   ▼
 Server
   │
Broadcast
   │
   ▼
Everyone
```

### Concepts

- TCP
- Threads
- Shared collections

---

## Feature 4 — Chat History

Command

```text
/history
```

Flow

```text
Redis
   │
Latest 100
   │
Return
```

### Concepts

- Redis Lists
- Serialization

---

## Feature 5 — Search

Command

```text
/search spring
```

Flow

```text
Server
   │
   ▼
Elasticsearch
   │
Match Query
   │
Results
```

### Concepts

- Indexing
- Full-text Search
- JSON documents

---

## Feature 6 — Quit

Command

```text
/quit
```

Flow

```text
Disconnect
     │
     ▼
Remove Client
     │
Close Socket
     │
Log Disconnect
```

### Concepts

- Resource cleanup
- Exception handling

---

## Features Explicitly Rejected

| Feature | Reason |
|----------|--------|
| Multiple Chat Rooms | More routing logic, no new technology |
| Private Messaging | More socket logic only |
| Read Receipts | UI concern |
| Typing Indicators | Networking noise |
| Message Editing | CRUD repetition |
| Delete Messages | CRUD repetition |
| Emojis | No backend learning |
| User Profiles | CRUD repetition |
| Friend System | Database complexity without new concepts |
| Roles/Admin | Security rabbit hole |

---

## Stretch Goal

### `/stats`

Returns

```text
Online Users : 5

Messages Sent : 324

Redis Messages : 100

Indexed Messages : 324
```

Purpose

Learn operational metrics and maintaining shared server state.

---

# 7. Milestones

## Milestone 1 — Foundation

### Goal

Build the application skeleton and authentication system.

### Deliverables

- Spring Boot setup
- PostgreSQL configuration
- Flyway migrations
- User entity
- Repository layer
- BCrypt integration
- User registration
- User login

### Technologies Learned

- Spring Boot
- Dependency Injection
- PostgreSQL
- JPA
- Flyway
- BCrypt

---

## Milestone 2 — Real-time Messaging

### Goal

Build the core chat server.

### Deliverables

- TCP socket server
- Multiple client connections
- ExecutorService
- Broadcast messaging
- Graceful disconnect

### Technologies Learned

- Java Networking
- TCP
- Threads
- ExecutorService
- ConcurrentHashMap

---

## Milestone 3 — Data Services

### Goal

Add supporting backend infrastructure.

### Deliverables

- Redis integration
- `/history`
- Elasticsearch integration
- `/search`
- Logging

### Technologies Learned

- Redis
- Elasticsearch
- SLF4J
- Serialization
- Search indexing

---

## Stretch Milestone

### Deliverables

- `/stats`

### Technologies Learned

- Operational metrics
- Shared server state

---

# 8. Success Criteria

The project is successful if the developer can confidently explain:

- Why Spring Boot is being used.
- How Dependency Injection works.
- How TCP sockets communicate.
- How multiple clients communicate simultaneously.
- Why PostgreSQL stores users.
- Why Redis stores recent chat history.
- Why Elasticsearch stores searchable messages.
- How Flyway manages schema evolution.
- Why passwords are hashed.
- Why logging matters in production applications.

The codebase is secondary.

Understanding is primary.

---

# 9. Learning Outcomes

After completing the project, the developer should be comfortable:

- Reading Spring Boot codebases
- Building small backend services
- Implementing socket-based communication
- Designing layered backend architecture
- Working with relational databases
- Managing database migrations
- Using Redis appropriately
- Implementing Elasticsearch indexing and searching
- Writing concurrent Java programs
- Explaining why each technology was chosen