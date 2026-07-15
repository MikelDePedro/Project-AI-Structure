# TechnicalDecisions

> **Project:** Football Hub (Working Title)
> **Version:** 1.0.0
> **Status:** Active

---

# Overview

This document records the most important architectural and technical decisions made during the development of Football Hub.

Each decision documents:

* The problem being solved.
* The chosen solution.
* Alternative approaches.
* Advantages.
* Disadvantages.
* Long-term consequences.

The purpose of this document is to preserve architectural knowledge and prevent future contributors from revisiting decisions that have already been evaluated.

Every significant architectural decision should be added to this document.

---

# Decision Format

Each decision follows the same structure.

```text
Decision ID

Status

Date

Context

Decision

Alternatives Considered

Advantages

Disadvantages

Consequences
```

---

# ADR-001

## Modular Monolith Architecture

**Status**

Accepted

---

### Context

Football Hub contains many independent business domains:

* Authentication
* Players
* Teams
* Competitions
* Matches
* Statistics
* Favorites
* Administration

The application must remain scalable while keeping operational complexity low.

---

### Decision

The backend will be implemented as a **Modular Monolith** using NestJS.

Each feature will be isolated in its own module with clear boundaries.

---

### Alternatives Considered

#### Microservices

Advantages

* Independent deployment.
* Independent scaling.

Disadvantages

* Higher infrastructure complexity.
* Distributed debugging.
* Increased operational costs.
* Excessive complexity for a portfolio project.

---

#### Traditional Layered Monolith

Advantages

* Simple implementation.

Disadvantages

* Weak module boundaries.
* Higher coupling.
* Difficult long-term maintenance.

---

### Why the Modular Monolith Was Chosen

It provides:

* Excellent maintainability.
* Lower infrastructure costs.
* Simpler deployment.
* Clear module separation.
* Easy migration to microservices if required.

---

### Consequences

Future extraction of individual modules into microservices remains possible.

---

# ADR-002

## PostgreSQL as Primary Database

**Status**

Accepted

---

### Context

The application stores highly relational football data.

Examples include:

* Players
* Teams
* Competitions
* Seasons
* Transfers
* Statistics

---

### Decision

Use PostgreSQL.

---

### Alternatives Considered

MongoDB

Advantages

* Flexible schema.

Disadvantages

* Poor fit for highly relational data.
* More complex reporting.
* More duplicated data.

---

MySQL

Advantages

* Mature ecosystem.

Disadvantages

* Prisma integration and PostgreSQL feature set better match project requirements.

---

### Why PostgreSQL

* Excellent relational capabilities.
* Strong indexing.
* Mature ecosystem.
* Advanced query support.
* Free hosting available through Neon.

---

### Consequences

The domain model should remain normalized.

---

# ADR-003

## Prisma ORM

**Status**

Accepted

---

### Context

Database access should remain type-safe.

Migrations should be automated.

---

### Decision

Use Prisma ORM.

---

### Alternatives

TypeORM

Drizzle

Raw SQL

---

### Why Prisma

* Excellent TypeScript support.
* Strong developer experience.
* Safe migrations.
* Generated types.
* Active ecosystem.

---

### Consequences

All schema changes must be introduced through Prisma Migrations.

---

# ADR-004

## JWT Authentication

**Status**

Accepted

---

### Decision

Authentication uses:

* JWT Access Tokens
* Refresh Tokens
* Refresh Token Rotation

Passwords use Argon2 hashing.

---

### Alternatives

Session Authentication

Advantages

* Simpler.

Disadvantages

* Reduced scalability.

---

### Why JWT

* Stateless.
* Widely adopted.
* Suitable for REST APIs.
* Easy frontend integration.

---

### Consequences

Refresh Tokens must be securely stored and rotated.

---

# ADR-005

## Redis Cache

**Status**

Accepted

---

### Context

Football information changes infrequently.

Repeated external API requests should be avoided.

---

### Decision

Redis will cache:

* Search results.
* Player pages.
* Team pages.
* Standings.
* External provider responses.

---

### Alternatives

No Cache

Advantages

* Simpler.

Disadvantages

* Slow responses.
* Excessive API usage.
* Higher provider dependency.

---

### Why Redis

* Extremely fast.
* Mature ecosystem.
* Supported by Upstash free tier.
* Easy integration.

---

### Consequences

A cache invalidation strategy must always accompany cached resources.

---

# ADR-006

## External Provider Abstraction

**Status**

Accepted

---

### Context

Football Hub depends on external football APIs.

Providers may change in the future.

---

### Decision

Create an abstraction layer.

```text
External Provider

↓

Adapter

↓

Mapper

↓

Domain

↓

Repository
```

---

### Alternatives

Consume provider models directly.

---

### Why the Abstraction Layer

Benefits

* Provider independence.
* Easier testing.
* Cleaner domain.
* Easier migrations.

---

### Consequences

Every provider requires its own adapter.

---

# ADR-007

## Feature-Based Frontend

**Status**

Accepted

---

### Decision

Frontend modules are organized by business feature instead of technical type.

Example

```text
Players

Teams

Competitions

Authentication
```

---

### Alternative

Organize by:

Components

Pages

Hooks

Services

---

### Why Feature-Based

Improves:

* Discoverability.
* Maintainability.
* Scalability.
* Module ownership.

---

# ADR-008

## REST API

**Status**

Accepted

---

### Decision

Expose a REST API.

---

### Alternatives

GraphQL

Advantages

* Flexible queries.

Disadvantages

* Increased complexity.
* More difficult caching.
* Unnecessary for current requirements.

---

### Why REST

* Mature.
* Predictable.
* Excellent tooling.
* Swagger integration.
* Simpler frontend development.

---

### Future

GraphQL may be introduced later as an additional API layer.

---

# ADR-009

## RBAC Authorization

**Status**

Accepted

---

### Decision

Authorization follows Role-Based Access Control.

Permissions are stored in the database.

No permission should be hardcoded.

---

### Why

Future roles should be configurable without code changes.

---

### Consequences

Authorization logic remains centralized.

---

# ADR-010

## Docker Development Environment

**Status**

Accepted

---

### Decision

Every local environment should run through Docker Compose.

Containers

* Backend
* PostgreSQL
* Redis

---

### Why

Benefits

* Reproducibility.
* Easy onboarding.
* Consistent environments.

---

### Consequences

The project should never depend on manual local installation of PostgreSQL or Redis.

---

# ADR-011

## GitHub Actions CI/CD

**Status**

Accepted

---

### Decision

Every Pull Request triggers automated pipelines.

Pipeline stages

* Install dependencies.
* Lint.
* Unit Tests.
* Integration Tests.
* Build.

Deployments occur only after successful validation.

---

### Why

Ensures repository stability.

---

# ADR-012

## Clean Architecture

**Status**

Accepted

---

### Decision

The backend follows Clean Architecture.

Layers

```text
Presentation

↓

Application

↓

Domain

↓

Infrastructure
```

---

### Why

Benefits

* Testability.
* Low coupling.
* Easier maintenance.
* Technology independence.

---

### Consequences

Infrastructure should never contain business rules.

---

# ADR-013

## Server State Management

**Status**

Accepted

---

### Decision

Server state uses TanStack Query.

Global UI state uses Zustand.

---

### Why

Different responsibilities require different tools.

Server data should never be duplicated in Zustand.

---

# ADR-014

## Zod for Frontend Validation

**Status**

Accepted

---

### Decision

Frontend validation uses:

* React Hook Form
* Zod

Backend validation remains independent using class-validator.

---

### Why

Shared validation logic where appropriate.

Excellent TypeScript support.

---

# ADR-015

## Logging Strategy

**Status**

Accepted

---

### Decision

Logs are categorized into:

* Authentication
* Business
* Infrastructure
* System

Sensitive data must never appear in logs.

Future Sentry integration should require minimal configuration.

---

# Pending Decisions

The following topics remain open for future evaluation.

* Background job scheduler.
* Search engine (PostgreSQL vs Meilisearch).
* CDN strategy.
* Image optimization.
* Email provider.
* Notification provider.
* Internationalization.
* Advanced analytics.

These decisions should only be documented after a complete architectural evaluation.

---

# Decision Review Policy

A decision should only be modified if:

* Business requirements change.
* Security concerns arise.
* Performance becomes unacceptable.
* A superior architectural solution is identified.
* Infrastructure constraints change.

Architectural decisions should not be changed solely because another technology becomes popular.

---

# Related Documents

This document explains **why** the architecture has been designed in its current form.

It complements:

* Vision
* Architecture
* DatabaseDesign
* CodingStandards

Future architectural decisions should be added to this document using the same ADR format.