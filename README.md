# Chat MVP

A production-ready realtime chat application built with **Go**, **Gin**,
**WebSocket**, **PostgreSQL**, **Redis**, and **Redis Streams**,
following **Clean Architecture** and **Manual Dependency Injection**.

The project also includes a separate **Notification Service** built with
**Spring Boot 3 (Java 21)** to demonstrate a hybrid microservice
architecture.

------------------------------------------------------------------------

# Overview

Chat MVP focuses on building a production-ready backend for realtime
one-to-one messaging. The main application is implemented in Go, while
asynchronous notifications are handled by an independent Spring Boot
service.

This architecture keeps the MVP simple while introducing practical
microservice concepts.

------------------------------------------------------------------------

# Tech Stack

## Chat API

-   Go 1.26+
-   Gin
-   WebSocket
-   PostgreSQL
-   Redis
-   Redis Streams
-   Swagger
-   Docker

## Notification Service

-   Java 21
-   Spring Boot 3
-   Maven
-   Spring Data Redis
-   Spring Mail
-   Docker

------------------------------------------------------------------------

# Architecture

``` text
                  Client
             (Web / Mobile)
            REST + WebSocket
                    │
                    ▼
           +------------------+
           |    Go Chat API   |
           | REST + WebSocket |
           +--------+---------+
                    │
          Save Message + XADD
                    │
                    ▼
            Redis Streams
                    │
        +-----------+-----------+
        │                       │
        ▼                       ▼
 Message Delivery        Notification Service
   Worker (Go)          Spring Boot (Java 21)
                                │
                                ▼
                      Email / Push (Future)
```

------------------------------------------------------------------------

# Clean Architecture

``` text
Delivery Layer
      │
Use Case Layer
      │
Domain Layer
      │
Infrastructure Layer
```

Dependencies always point inward.

------------------------------------------------------------------------

# Features

## Authentication

-   Register
-   Login
-   JWT Authentication

## User

-   Profile
-   Online Status
-   Last Seen

## Conversation

-   Create Conversation
-   List Conversations

## Messaging

-   Send Text Message
-   Receive Realtime Message
-   Message History

## WebSocket

-   Persistent Connection
-   Ping / Pong
-   Automatic Reconnect

## Notification

-   Consume message events
-   Send email notification
-   Extensible for Push Notification and SMS

------------------------------------------------------------------------

# Redis Streams

Example stream:

``` text
stream:messages
```

Event flow:

``` text
User A
   │
Send Message
   │
Save PostgreSQL
   │
XADD stream:messages
   │
Consumer Group
   ├──────────────► WebSocket Delivery Worker
   └──────────────► Notification Service
```

------------------------------------------------------------------------

# Project Structure

``` text
chat-mvp/
├── cmd/
├── internal/
│   ├── bootstrap/
│   ├── config/
│   ├── delivery/
│   ├── domain/
│   ├── middleware/
│   ├── repository/
│   ├── service/
│   ├── redis/
│   └── stream/
├── pkg/
├── docs/
├── migrations/
├── docker/
├── Dockerfile
├── docker-compose.yml
├── Makefile
└── README.md
```

Notification service:

``` text
notification-service/
├── src/main/java/
│   ├── config/
│   ├── consumer/
│   ├── service/
│   ├── mail/
│   ├── dto/
│   └── util/
├── Dockerfile
├── pom.xml
└── README.md
```

------------------------------------------------------------------------

# Docker Services

Core:

-   chat-api
-   postgres
-   redis
-   notification-service

Optional:

-   redisinsight
-   pgadmin

------------------------------------------------------------------------

# Quick Start

``` bash
git clone https://github.com/<your-username>/chat-mvp.git
cd chat-mvp

cp .env.example .env

docker compose up -d
```

------------------------------------------------------------------------

# API Documentation

Swagger

``` text
http://localhost:8080/swagger/index.html
```

------------------------------------------------------------------------

# Design Principles

-   Clean Architecture
-   Manual Dependency Injection
-   Repository Pattern
-   Thin Handlers
-   Stateless API
-   PostgreSQL as the source of truth
-   Redis Streams as the event bus
-   Separate Spring Boot Notification Service

------------------------------------------------------------------------

# MVP Scope

-   Authentication
-   User Management
-   One-to-One Chat
-   Conversation
-   Message History
-   Realtime Messaging
-   Email Notification
-   Docker Deployment

------------------------------------------------------------------------

# Future Roadmap

-   Group Chat
-   Read Receipts
-   Typing Indicator
-   Attachments
-   Push Notifications
-   Search
-   Multi-device Support
-   Kubernetes

------------------------------------------------------------------------

