Backend Engineering Learning Project
Engineering Specification v1.0
1. Purpose

Develop a minimal real-time chat application that serves as a vehicle for learning modern Java backend development.

The application itself is not the objective. Instead, each feature exists to demonstrate and provide hands-on experience with one or more backend technologies.

2. Objectives
   Primary

Gain practical experience with:

Java Socket Programming
Spring Boot
Dependency Injection
PostgreSQL
Spring Data JPA
Flyway
Redis
Elasticsearch
BCrypt
Concurrent programming
Secondary

Understand how different persistence technologies complement each other.

3. Constraints

Time Budget

3 Days

5 Hours / Day

≈15 Hours

Developer Experience

Beginner

Priority

Learning > Completeness
4. Success Criteria

The project is successful if the developer can explain:

Why Spring Boot is being used
How TCP sockets work
How multiple clients communicate simultaneously
Why PostgreSQL stores users
Why Redis stores chat history
Why Elasticsearch stores searchable messages
How Flyway manages database schema
Why passwords are hashed

The codebase is secondary.

Understanding is primary.

5. Scope

The application supports

User registration
User login
One global chat room
Multiple concurrent users
Recent message history
Full-text message search
Graceful disconnect
6. Out of Scope

No REST API

No GUI

No Spring Security

No JWT

No Docker

No Tests

No Multiple Rooms

No Private Messaging

No File Uploads

No Notifications

No Read Receipts

No Typing Indicators

No Message Editing

No Cloud Deployment

7. Technology Stack
   Layer	Technology
   Language	Java 21
   Framework	Spring Boot
   Build	Gradle
   Database	PostgreSQL
   ORM	Spring Data JPA
   Migration	Flyway
   Cache	Redis
   Search	Elasticsearch
   Networking	TCP Sockets
   Logging	SLF4J
   Password Hashing	BCrypt
8. System Responsibilities
   Spring Boot

Application lifecycle

Dependency injection

Configuration

PostgreSQL

Persistent user information

Redis

Recent chat history

Elasticsearch

Search engine

Socket Server

Real-time communication

9. Functional Requirements
   Authentication

Users shall be able to:

Register
Login

Passwords shall be hashed.

Chat

Authenticated users shall:

Connect
Send messages
Receive broadcasts
History

Users shall retrieve recent messages using

/history
Search

Users shall search previous messages using

/search <keyword>
Exit

Users shall disconnect using

/quit
10. Data Model
    PostgreSQL
    users

id
username
password_hash
created_at
Redis
chat_history

List<Message>

Latest 100
Elasticsearch
messages

username
message
timestamp
11. Milestones
    M1

Authentication works.

M2

Multiple clients can chat.

M3

Redis stores history.

M4

Elasticsearch searches messages.

12. Learning Outcomes

After completing the project, the developer should be comfortable:

Reading Spring Boot codebases
Building small backend services
Working with relational databases
Managing database migrations
Using Redis
Using Elasticsearch
Writing concurrent Java programs
Understanding layered backend architecture

Let's be ruthless about the features. Every feature should justify at least one technology you're trying to learn.

Feature	Why it exists	Technology learned	Keep?
User Registration	Learn persistence	PostgreSQL + JPA + Flyway	✅
Login	Learn authentication flow	BCrypt + JPA	✅
Real-time Chat	Learn sockets	Java Sockets + Threads	✅
Multiple Clients	Learn concurrency	ExecutorService	✅
Broadcast Messages	Learn shared state	ConcurrentHashMap	✅
Chat History	Learn Redis	Redis Lists	✅
Message Search	Learn Elasticsearch	Indexing + Search	✅
Graceful Disconnect	Learn resource management	Sockets	✅
Logging	Learn production practices	SLF4J	✅

That's essentially the entire MVP.

Feature 1 — Register
register

Flow

Username

↓

Password

↓

Hash password

↓

Save in PostgreSQL

Concepts:

Entity
Repository
Service
Flyway
BCrypt
Feature 2 — Login
login

Flow

Username

↓

Password

↓

Verify hash

↓

Allow socket session

Concepts:

Authentication
Repository lookup
Password verification
Feature 3 — Global Chat

Everyone joins

General Room

No rooms.

No DMs.

Flow

Alice

↓

Hello

↓

Server

↓

Broadcast

↓

Everyone receives

Concepts:

TCP
Threads
Shared collections
Feature 4 — Chat History
/history

Server

Redis

↓

Latest 100

↓

Return to client

Concepts:

Redis Lists
Serialization
Feature 5 — Search
/search spring

Server

Elasticsearch

↓

match query

↓

Results

Concepts:

Indexing
Search
JSON documents
Feature 6 — Quit
/quit

Server

Remove client

↓

Close socket

↓

Log disconnect

Concepts:

Resource cleanup
Exception handling
Features I'd Reject

These are tempting, but they don't give you enough learning for the added complexity.

❌ Multiple Chat Rooms

Adds routing logic and state management, but doesn't teach a new technology.

❌ Private Messages

Just more socket logic.

No new backend concept.

❌ Read Receipts

UI feature.

❌ Typing Indicators

Networking noise.

❌ Message Editing

Needs persistent message storage.

❌ Delete Messages

Same.

❌ Emojis

No backend value.

❌ User Profiles

CRUD repetition.

❌ Friend System

Lots of database work, little new learning.

❌ Roles/Admin

Security rabbit hole.

One Feature I'd Consider Adding

If you have 30–60 minutes left on Day 3:

/stats
/stats

Returns something like:

Online Users : 5

Messages Sent : 324

Redis Messages : 100

Search Index : 324

Why?

It forces you to think about maintaining server state and gives you a useful operational view without introducing another technology.

Final Feature List
Authentication
Register
Login
Messaging
Global chat
Broadcast messages
Multiple concurrent users
Data
Recent history (/history)
Full-text search (/search)
System
Graceful disconnect (/quit)
Logging

That's 8 focused features, each directly tied to one or more backend concepts you want to learn. There's very little "application logic" for its own sake—the chat domain is just enough to exercise the technologies without becoming the project itself.

Product Requirements Document (PRD)
Project

Java Backend Learning Chat

1. Purpose

Develop a minimal console-based chat application that allows multiple users to communicate in real time.

The application focuses on a single global chat room with user authentication, recent chat history, and message search.

2. Target User
   Developer learning backend engineering.
   Single-user development project.
3. Goals

The application shall allow users to:

Register
Login
Join a global chat
Send and receive messages
View recent chat history
Search previous messages
Disconnect safely
4. Features
   User Registration

Users can create an account.

Requirements

Username must be unique
Password must be securely stored
Registration should fail if username already exists
Login

Registered users can authenticate.

Requirements

Validate credentials
Reject invalid login attempts
Allow only authenticated users into chat
Global Chat

Authenticated users can

Send messages
Receive broadcasts
Participate in a single shared chat room
Recent History

Users can execute

/history

to retrieve recent messages.

Search

Users can execute

/search <keyword>

to search previous messages.

Disconnect

Users can leave using

/quit
5. User Flow
   Start Client

↓

Register / Login

↓

Join Chat

↓

Chat

↓

History/Search

↓

Quit
6. Out of Scope
   GUI
   Multiple chat rooms
   Direct messaging
   File sharing
   Message editing
   Read receipts
   Typing indicators
   Notifications
   User profiles
   Administration
7. Success Criteria

The application supports

Multiple concurrent users
Authentication
Real-time messaging
Recent history retrieval
Message search
Technical Requirements Document (TRD)
1. Objective

Build the application using technologies commonly found in modern Java backend systems while understanding each technology's role.

2. Technology Stack
   Layer	Technology
   Language	Java 21
   Framework	Spring Boot
   Build	Gradle
   Database	PostgreSQL
   ORM	Spring Data JPA
   Migration	Flyway
   Cache	Redis
   Search	Elasticsearch
   Networking	TCP Sockets
   Logging	SLF4J
   Security	BCrypt
3. Technology Objectives
   Spring Boot

Learn

Dependency Injection
Bean lifecycle
Configuration
Layered architecture
Java Networking

Learn

TCP sockets
Client-server communication
Thread-per-client model
ExecutorService
PostgreSQL

Store

Users

Learn

JPA
CRUD
Relationships (basic)
Flyway

Learn

Versioned database migrations
Schema evolution
Redis

Store

Latest 100 messages

Learn

Lists
Fast retrieval
Elasticsearch

Store

Searchable message documents

Learn

Indexing
Match queries
Full-text search
BCrypt

Learn

Password hashing
Password verification
Logging

Learn

SLF4J
Log levels
Structured application logs
4. System Architecture
   Console Client
   │
   TCP Socket
   │
   +-----------------------+
   | Spring Boot Server    |
   |-----------------------|
   | Socket Server         |
   | Authentication        |
   | Chat Service          |
   | Redis Service         |
   | Search Service        |
   +-----------------------+
   │      │       │
   ▼      ▼       ▼
   PostgreSQL Redis Elasticsearch
5. Storage Responsibilities
   PostgreSQL

Persistent data

Users
Redis

Temporary data

Recent messages
Elasticsearch

Search index

Messages
6. Package Structure
   config/
   socket/
   entity/
   repository/
   service/
   dto/
   util/
7. Milestones
   Milestone 1
   Spring Boot setup
   PostgreSQL
   Flyway
   User registration
   Login
   Socket server
   Milestone 2
   Multiple clients
   Broadcast
   Redis integration
   History
   Milestone 3
   Elasticsearch integration
   Search
   Logging
   Cleanup
8. Learning Outcomes

By project completion, the developer should be able to:

Build a Spring Boot backend
Implement socket-based communication
Design a layered application
Persist data with JPA
Manage schemas with Flyway
Use Redis appropriately
Implement basic Elasticsearch indexing and searching
Explain why each technology was chosen