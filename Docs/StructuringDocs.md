# Repository Structure

The project follows a layered architecture where each package has a single responsibility. Features are implemented by adding functionality to existing layers rather than creating new architectural patterns.

---

# Project Structure

```text
chat-app/
│
├── build.gradle
├── settings.gradle
├── gradlew
├── gradlew.bat
├── README.md
├── .gitignore
│
├── src/
│   ├── main/
│   │
│   │   ├── java/
│   │   │
│   │   │   └── com/
│   │   │       └── chatapp/
│   │   │
│   │   │           ├── ChatApplication.java
│   │   │           │
│   │   │           ├── config/
│   │   │           │
│   │   │           ├── socket/
│   │   │           │
│   │   │           ├── controller/
│   │   │           │
│   │   │           ├── service/
│   │   │           │
│   │   │           ├── repository/
│   │   │           │
│   │   │           ├── entity/
│   │   │           │
│   │   │           ├── dto/
│   │   │           │
│   │   │           ├── redis/
│   │   │           │
│   │   │           ├── elasticsearch/
│   │   │           │
│   │   │           ├── security/
│   │   │           │
│   │   │           ├── exception/
│   │   │           │
│   │   │           └── util/
│   │
│   │   └── resources/
│   │       │
│   │       ├── application.yml
│   │       │
│   │       └── db/
│   │           └── migration/
│   │
│   └── test/
│
└── docs/
    ├── PRD.md
    ├── TRD.md
    └── architecture.md
```

---

# Package Responsibilities

## ChatApplication

Application entry point.

Responsibilities

- Starts Spring Boot
- Initializes dependency injection
- Starts the application context

---

## config/

Contains Spring configuration.

Examples

- Bean definitions
- Application configuration
- Socket configuration
- Redis configuration
- Elasticsearch configuration

---

## socket/

Contains everything related to TCP networking.

Possible Classes

```text
ChatServer.java
ClientHandler.java
SocketSession.java
SocketConfig.java
```

Responsibilities

- Accept client connections
- Manage socket lifecycle
- Read incoming messages
- Broadcast messages
- Handle disconnects

---

## controller/

Reserved for future REST APIs.

Current Project

Not used.

Purpose

Keeps the project ready if HTTP endpoints are added later.

---

## service/

Contains business logic.

Possible Classes

```text
AuthService.java
ChatService.java
HistoryService.java
SearchService.java
UserService.java
```

Responsibilities

- Authenticate users
- Coordinate repositories
- Save chat history
- Search messages
- Broadcast business events

The service layer is the heart of the application.

---

## repository/

Contains PostgreSQL repositories.

Example

```text
UserRepository.java
```

Responsibilities

- Database CRUD
- JPA queries
- User persistence

No business logic belongs here.

---

## entity/

Contains database entities.

Example

```text
User.java
```

Responsibilities

- Represent PostgreSQL tables
- JPA annotations
- Database mapping

---

## dto/

Contains Data Transfer Objects.

Possible Classes

```text
LoginRequest.java
RegisterRequest.java
ChatMessage.java
```

Responsibilities

- Pass data between layers
- Prevent exposing database entities
- Simplify serialization

---

## redis/

Contains Redis-specific classes.

Possible Classes

```text
RedisConfig.java
RedisHistoryRepository.java
```

Responsibilities

- Store recent messages
- Retrieve chat history
- Configure Redis connection

---

## elasticsearch/

Contains Elasticsearch integration.

Possible Classes

```text
ElasticsearchConfig.java
MessageDocument.java
SearchRepository.java
```

Responsibilities

- Index messages
- Execute search queries
- Configure Elasticsearch

---

## security/

Contains password security.

Example

```text
PasswordEncoder.java
```

Responsibilities

- Hash passwords
- Verify passwords

Only BCrypt logic belongs here.

---

## exception/

Contains custom exceptions.

Examples

```text
AuthenticationException.java
UserAlreadyExistsException.java
```

Responsibilities

- Domain-specific exceptions
- Error handling

---

## util/

Contains helper classes.

Examples

```text
Constants.java
DateUtil.java
JsonUtil.java
```

Responsibilities

- Shared helper methods
- Utility functions
- Constants

Avoid putting business logic here.

---

# Resources

## application.yml

Contains

- Database configuration
- Redis configuration
- Elasticsearch configuration
- Logging configuration
- Spring Boot properties

---

## db/migration/

Contains Flyway migration scripts.

Example

```text
V1__create_users.sql
V2__...
```

Responsibilities

- Create schema
- Modify schema
- Version database changes

---

# Layered Architecture

```text
                Socket Layer
                     │
                     ▼
               Service Layer
                     │
     ┌───────────────┼───────────────┐
     ▼               ▼               ▼
Repository        Redis        Elasticsearch
     │
     ▼
 PostgreSQL
```

Dependency Rule

```text
Socket
   ↓
Service
   ↓
Persistence
```

Only the **Service** layer should communicate with multiple persistence technologies.

---

# Repository Evolution

## Milestone 1 — Authentication

```text
entity/
repository/
service/
security/
resources/db/migration/
```

Technologies

- Spring Boot
- PostgreSQL
- JPA
- Flyway
- BCrypt

---

## Milestone 2 — Real-Time Chat

```text
socket/
service/
util/
```

Technologies

- TCP Sockets
- ExecutorService
- ConcurrentHashMap

---

## Milestone 3 — Data Services

```text
redis/
elasticsearch/
config/
```

Technologies

- Redis
- Elasticsearch
- SLF4J

---

# Design Principles

- One package should have one primary responsibility.
- Business logic belongs in the service layer.
- Repositories should only access databases.
- Socket classes should never directly access databases.
- Services coordinate PostgreSQL, Redis, and Elasticsearch.
- Utilities should remain generic and free of business logic.
- Keep the architecture simple and layered until the project is complete.