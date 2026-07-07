# Chat MVP

A production-ready realtime chat application built with **Go**, **Gin**,
**WebSocket**, **PostgreSQL**, **Redis**, and **Kafka**, following
**Clean Architecture** and **Dependency Injection** principles.

------------------------------------------------------------------------

## Overview

Chat MVP is a lightweight, scalable, and maintainable backend service
for realtime one-to-one messaging. The project focuses on building a
solid foundation that can later evolve into a production-scale messaging
platform.

This repository is intentionally scoped as an MVP while keeping the
architecture extensible for future features such as group chat, read
receipts, typing indicators, attachments, notifications, and search.

------------------------------------------------------------------------

## Tech Stack

### Backend

-   Go 1.26+
-   Gin

### Realtime

-   WebSocket

### Database

-   PostgreSQL

### Cache

-   Redis

### Event Streaming

-   Kafka

### Architecture

-   Clean Architecture
-   Repository Pattern
-   Manual Dependency Injection
-   Service (Use Case) Layer
-   Domain Driven Module Separation

### Infrastructure

-   Docker
-   Docker Compose

### Documentation

-   Swagger / OpenAPI

------------------------------------------------------------------------

# Architecture

``` text
                    Client
             (Web / Mobile App)
                REST + WebSocket
                       │
                       ▼
              +-------------------+
              |   Gin API Server  |
              |  REST + WebSocket |
              +---------+---------+
                        │
                  Dependency Injection
                        │
      +-----------------+------------------+
      |                 |                  |
      ▼                 ▼                  ▼
   Auth Module      User Module      Chat Module
      │                 │                  │
      +-----------------+------------------+
                        ▼
                 Service / Use Case
                        │
          +-------------+-------------+
          |             |             |
          ▼             ▼             ▼
     PostgreSQL      Redis         Kafka
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

Dependency direction:

``` text
Handler
   │
Service
   │
Repository Interface
   │
Repository Implementation
```

------------------------------------------------------------------------

# Features

## Authentication

-   Register
-   Login
-   JWT Authentication

## User

-   User Profile
-   Online Status
-   Last Seen

## Conversation

-   Create Conversation
-   List Conversations

## Messaging

-   Send Message
-   Receive Message (Realtime)
-   Message History

## WebSocket

-   Persistent Connection
-   Heartbeat (Ping / Pong)
-   Automatic Reconnect Support

------------------------------------------------------------------------

# Project Structure

``` text
chat-mvp/
├── cmd/
│   └── server/
├── internal/
│   ├── bootstrap/
│   ├── config/
│   ├── delivery/
│   │   ├── http/
│   │   └── websocket/
│   ├── domain/
│   ├── middleware/
│   ├── repository/
│   │   └── postgres/
│   ├── service/
│   ├── kafka/
│   └── redis/
├── pkg/
│   ├── logger/
│   ├── response/
│   └── validator/
├── docs/
├── migrations/
├── docker/
├── Dockerfile
├── docker-compose.yml
├── Makefile
├── README.md
└── .env.example
```

------------------------------------------------------------------------

# High Level Flow

``` text
Client
   │
REST Login
   │
JWT
   │
WebSocket Connect
   │
Send Message
   │
Save Message
   │
PostgreSQL
   │
Publish Event
   │
Kafka
   │
Deliver Message
   │
Recipient
```

------------------------------------------------------------------------

# Docker Services

-   chat-api
-   postgres
-   redis
-   kafka

Optional:

-   kafka-ui
-   pgadmin

------------------------------------------------------------------------

# Quick Start

## Clone

``` bash
git clone https://github.com/<your-username>/chat-mvp.git

cd chat-mvp
```

## Configure

``` bash
cp .env.example .env
```

## Start

``` bash
docker compose up -d
```

## Stop

``` bash
docker compose down
```

------------------------------------------------------------------------

# API Documentation

Swagger will be available after the API starts.

``` text
http://localhost:8080/swagger/index.html
```

------------------------------------------------------------------------

# Design Principles

-   Single deployable backend service
-   Stateless API
-   PostgreSQL as the source of truth
-   Redis for transient state and caching
-   Kafka for asynchronous event processing
-   Thin handlers
-   Business logic isolated in services
-   Interface-based dependency inversion
-   Manual dependency injection
-   Production-oriented project structure

------------------------------------------------------------------------

# Roadmap

-   Authentication
-   One-to-One Chat
-   Conversation
-   Message History
-   WebSocket
-   Docker Deployment


-------------------------------

