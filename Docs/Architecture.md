# Architecture

> **Project:** Football Hub (Working Title)
> **Version:** 1.0.0
> **Status:** Active

---

# Overview

Football Hub is designed as a modular, scalable and maintainable Full Stack application following the principles of **Clean Architecture** and **Domain-Oriented Design**.

The architecture prioritizes long-term maintainability over implementation speed.

Every layer has a single responsibility.

Every module owns its own business logic.

Infrastructure details never leak into the domain.

The application must be capable of evolving for years without requiring major architectural rewrites.

---

# High-Level Architecture

```text
                           Users
                             │
                             ▼
                    React + TypeScript
                             │
                             ▼
                      REST API (HTTPS)
                             │
                             ▼
                  NestJS Application Layer
                             │
        ┌────────────────────┼────────────────────┐
        ▼                    ▼                    ▼
   Domain Layer        Infrastructure      Shared Services
        │                    │                    │
        └────────────────────┼────────────────────┘
                             ▼
                        PostgreSQL
                             │
                             ▼
                           Prisma
                             │
                             ▼
                            Redis
                             │
                             ▼
                 External Football Providers
```

---

# Architectural Principles

The entire application follows these principles.

## Modularity

Each business capability belongs to a dedicated module.

Modules should remain independent.

Adding or removing a module should have minimal impact on the rest of the application.

---

## Separation of Concerns

Each layer has a clearly defined responsibility.

Presentation

↓

Application

↓

Domain

↓

Infrastructure

No layer should assume responsibilities belonging to another.

---

## Dependency Direction

Dependencies always point toward the domain.

Infrastructure depends on Domain.

Application depends on Domain.

Presentation depends on Application.

The Domain never depends on Infrastructure.

---

## Provider Independence

External football APIs are implementation details.

The application should never depend directly on any provider.

Changing providers should not require modifications to business logic.

---

## Testability

Every business rule should be independently testable.

Infrastructure should be mockable.

External APIs should never be required during unit testing.

---

# Frontend Architecture

The frontend follows a feature-based architecture.

```text
Frontend

src/

├── app/
├── routes/
├── modules/
├── components/
├── layouts/
├── hooks/
├── services/
├── store/
├── lib/
├── types/
├── utils/
└── assets/
```

---

## Responsibilities

### app

Application bootstrap.

* Providers
* Routing
* Global configuration

---

### routes

Application routing.

Protected routes.

Public routes.

Lazy loading.

---

### modules

Feature-based organization.

Example

```text
modules/

auth/

players/

teams/

matches/

competitions/

favorites/

admin/
```

Each module contains everything related to that feature.

---

### components

Reusable UI components.

Examples

* Button
* Modal
* Table
* Pagination
* SearchInput

Business logic should never exist here.

---

### services

HTTP communication.

Axios configuration.

API clients.

Interceptors.

---

### store

Global state using Zustand.

Only global state belongs here.

Server state belongs to TanStack Query.

---

### lib

Shared libraries.

Examples

* Axios instance
* Zod schemas
* Utility wrappers

---

### utils

Pure helper functions.

No business logic.

---

# Backend Architecture

The backend follows a modular architecture using NestJS.

```text
src/

modules/

shared/

config/

common/

main.ts
```

Every feature is implemented as an independent NestJS module.

---

# Module Structure

Every module follows the same structure.

```text
Players/

controllers/

services/

repositories/

dto/

entities/

mappers/

interfaces/

guards/

validators/

tests/

players.module.ts
```

---

# Module Responsibilities

## Controller

Receives HTTP requests.

Responsibilities

* Request validation
* Authentication
* Authorization
* Response formatting

Controllers should remain thin.

Business logic must never exist inside controllers.

---

## Service

Contains application use cases.

Coordinates repositories.

Coordinates providers.

Coordinates cache.

Contains business workflows.

---

## Repository

Responsible only for persistence.

Repositories never contain business rules.

Repositories never call external APIs.

---

## DTO

Defines request and response contracts.

Validation occurs here.

---

## Entities

Represent domain models.

Entities should remain independent of Prisma.

---

## Mapper

Converts between:

* External providers
* Database models
* Domain entities
* DTOs

Every transformation belongs here.

---

## Tests

Every module contains:

* Unit tests
* Integration tests

---

# Shared Layer

Shared functionality should live outside business modules.

Examples

```text
shared/

cache/

logging/

auth/

exceptions/

validators/

constants/
```

Shared code must remain generic.

Business-specific functionality does not belong here.

---

# Infrastructure Layer

Infrastructure contains implementation details.

Examples

* Prisma
* Redis
* Cloudinary
* External APIs
* Email providers

Infrastructure can change without affecting business logic.

---

# Database Architecture

The application uses PostgreSQL.

Persistence is handled through Prisma.

Every table follows these conventions.

```text
id UUID

createdAt

updatedAt

deletedAt (when applicable)
```

Soft Delete should only be used where historical data is valuable.

---

# Cache Architecture

Redis acts as a secondary storage layer.

Typical flow

```text
Request

↓

Redis

↓

Database

↓

External Provider

↓

Database Update

↓

Redis Update

↓

Response
```

Redis is never considered the source of truth.

PostgreSQL remains authoritative.

---

# External Provider Architecture

Football data providers are isolated.

```text
Provider

↓

Adapter

↓

Mapper

↓

Domain

↓

Repository
```

Example

```text
Api-Football

↓

ApiFootballAdapter

↓

PlayerMapper

↓

Player Entity

↓

PlayersRepository
```

Replacing the provider should only require implementing a new adapter.

---

# Authentication Flow

```text
User

↓

Login

↓

JWT Access Token

+

Refresh Token

↓

Protected Request

↓

JWT Validation

↓

Authorization

↓

Controller

↓

Service
```

Refresh Tokens are rotated after every successful refresh request.

---

# Authorization

Authorization follows RBAC.

Roles

* User
* Moderator
* Administrator

Permissions should be evaluated through Guards.

Permissions must never be hardcoded inside controllers.

---

# Data Flow

The application follows the following request lifecycle.

```text
Browser

↓

React

↓

Axios

↓

NestJS Controller

↓

Validation

↓

Authorization

↓

Service

↓

Repository

↓

Database

↓

Response

↓

TanStack Query

↓

UI
```

Business logic should never bypass this flow.

---

# Error Handling

Errors should be centralized.

Every exception should produce a consistent response.

Example

```json
{
  "statusCode": 404,
  "message": "Player not found",
  "error": "Not Found",
  "timestamp": "2026-07-15T18:00:00Z",
  "path": "/players/123"
}
```

Internal errors should never expose implementation details.

---

# Logging Architecture

Application logs should be categorized.

Authentication

* Login
* Logout
* Failed authentication

Business

* Synchronization
* Administrative actions

Infrastructure

* Database
* Redis
* External providers

System

* Startup
* Shutdown
* Fatal errors

Logs should support future integration with Sentry.

---

# Scalability Strategy

The architecture should support future growth.

Examples

* Multiple football providers.
* Multiple cache providers.
* Object storage replacement.
* Horizontal backend scaling.
* Background workers.
* Message queues.
* Microservice extraction if necessary.

Current implementation remains a modular monolith.

This provides lower complexity while preserving future scalability.

---

# Architectural Decisions

The project intentionally adopts a **Modular Monolith** instead of Microservices.

Reasons:

Advantages

* Easier deployment.
* Lower operational complexity.
* Faster development.
* Simpler debugging.
* Better suited for a portfolio project.

Future migration to microservices remains possible because module boundaries are strictly defined.

---

# Quality Attributes

The architecture is optimized for:

* Maintainability
* Readability
* Scalability
* Security
* Performance
* Testability
* Extensibility
* Provider Independence

Every architectural decision should improve at least one of these attributes without significantly degrading another.

---

# Related Documents

This document describes **how** the application is built.

For implementation details, refer to:

* DatabaseDesign
* ApiSpecification
* CodingStandards
* TechnicalDecisions

All implementation should conform to the architecture defined in this document.