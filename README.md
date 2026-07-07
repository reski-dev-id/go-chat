# Chat MVP

A production-ready realtime chat application built with **Go**, **Gin**,
**WebSocket**, **PostgreSQL**, and **Redis Streams**, following **Clean
Architecture** and **Manual Dependency Injection**.

------------------------------------------------------------------------

# Overview

Chat MVP is a backend service for realtime one-to-one messaging inspired
by messaging applications such as WhatsApp.

The project intentionally focuses on a small but production-ready
feature set while maintaining an architecture that can be extended in
the future.

------------------------------------------------------------------------

# Tech Stack

## Backend

-   Go 1.26+
-   Gin

## Realtime

-   WebSocket

## Database

-   PostgreSQL

## Redis

-   Redis Cache
-   Redis Streams
-   Consumer Groups
-   Presence
-   Session Storage

## Architecture

-   Clean Architecture
-   Manual Dependency Injection
-   Repository Pattern
-   Service (Use Case) Layer
-   Domain Driven Module Separation

## Infrastructure

-   Docker
-   Docker Compose

## Documentation

-   Swagger / OpenAPI

------------------------------------------------------------------------

# High Level Architecture

``` text
                 Client
          (Web / Mobile App)
            REST + WebSocket
                   │
                   ▼
          +-------------------+
          |   Gin API Server  |
          | REST + WebSocket  |
          +---------+---------+
                    │
             Dependency Injection
                    │
      +-------------+-------------+
      |             |             |
      ▼             ▼             ▼
   Auth         Conversation    Message
      │             │             │
      +-------------+-------------+
                    ▼
             Service / Use Case
                    │
          +---------+---------+
          |                   |
          ▼                   ▼
     PostgreSQL        Redis Streams
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

Dependency flow:

``` text
HTTP / WebSocket Handler
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

-   Send Text Message
-   Receive Realtime Message
-   Message History

## WebSocket

-   Persistent Connection
-   Heartbeat (Ping/Pong)
-   Automatic Reconnect

------------------------------------------------------------------------

# Redis Streams

Redis Streams is used as the internal event bus.

Example stream:

``` text
stream:messages
```

Flow:

``` text
Save Message
      │
      ▼
PostgreSQL
      │
      ▼
XADD stream:messages
      │
      ▼
Consumer Group
      │
      ▼
WebSocket Hub
      │
      ▼
Recipient
```

Redis is also responsible for:

-   Online presence
-   Session storage
-   Temporary cache

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
│   ├── redis/
│   └── stream/
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

# Docker Services

-   chat-api
-   postgres
-   redis

Optional

-   redisinsight
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

## Run

``` bash
docker compose up -d
```

## Stop

``` bash
docker compose down
```

------------------------------------------------------------------------

# API Documentation

Swagger:

``` text
http://localhost:8080/swagger/index.html
```

------------------------------------------------------------------------

# Design Principles

-   Clean Architecture
-   Manual Dependency Injection
-   Thin Handlers
-   Stateless API
-   PostgreSQL as the source of truth
-   Redis Streams for asynchronous event processing
-   Interface-based dependency inversion
-   Modular project structure

------------------------------------------------------------------------

# MVP Scope

-   User Authentication
-   JWT
-   One-to-One Chat
-   Conversation Management
-   Message History
-   Realtime Messaging
-   Docker Deployment


------------------------------------------------------------------------

