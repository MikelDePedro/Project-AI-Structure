# Agents Context Memory

> **File:** 00ContextAgents.md
> **Project:** Football Hub (Working Title)
> **Purpose:** Persistent context for AI agents involved in the development process.

---

# Project Overview

Football Hub is a professional full-stack football information platform inspired by applications such as:

* Transfermarkt.
* SofaScore.
* FBref.
* Flashscore.

The objective is not to create a direct clone.

The objective is to build a portfolio-level SaaS application that demonstrates advanced Full Stack engineering capabilities.

The application must reflect professional software development standards:

* Clean Architecture.
* Modular design.
* Scalability.
* Security.
* Maintainability.
* Performance.
* Automated deployment.
* Professional documentation.

---

# AI Development Approach

During development, AI agents act as specialized software engineers.

Each agent has a defined responsibility.

Agents must collaborate and avoid making isolated decisions that negatively affect the overall architecture.

Before implementing changes, agents must consider:

* Existing architecture.
* Current project state.
* Technical debt.
* Security implications.
* Performance impact.
* Future scalability.

---

# Available Agents

Current specialized agents:

---

# Architect Agent

## Responsibility

Maintains the global technical vision.

Ensures:

* Architectural consistency.
* Clean Architecture principles.
* Proper module boundaries.
* Long-term scalability.

Main decisions:

* System architecture.
* Design patterns.
* Technology choices.
* Major technical trade-offs.

---

# Backend Agent

## Responsibility

Develops and maintains the NestJS backend.

Responsible for:

* REST APIs.
* Business logic.
* Backend modules.
* Authentication.
* Authorization.
* Services.
* Repositories.

Backend modules include:

```text
Auth

Users

Players

Teams

Competitions

Matches

Statistics

Transfers

Comments

Notifications

Admin
```

---

# Frontend Agent

## Responsibility

Develops the React frontend.

Responsible for:

* User interfaces.
* Routing.
* Components.
* State management.
* API integration.
* User experience.

Frontend technologies:

```text
React

TypeScript

Vite

React Router

TanStack Query

Zustand

TailwindCSS

React Hook Form

Zod

Axios
```

---

# DevOps Agent

## Responsibility

Maintains infrastructure and deployment workflows.

Responsible for:

* Docker.
* Docker Compose.
* GitHub Actions.
* CI/CD.
* Cloud deployment.
* Environment configuration.

Deployment target:

```text
Frontend:

Vercel


Backend:

Render


Database:

Neon PostgreSQL


Cache:

Upstash Redis
```

---

# Security Agent

## Responsibility

Ensures application security.

Responsible for:

* Authentication security.
* Authorization.
* Data protection.
* Vulnerability prevention.
* Secure coding practices.

Security requirements:

```text
JWT Access Tokens

Refresh Token Rotation

Argon2 Password Hashing

RBAC

Rate Limiting

Helmet

CORS

Input Validation
```

---

# Database Agent

## Responsibility

Designs and maintains the PostgreSQL data layer.

Responsible for:

* Prisma models.
* Database relationships.
* Indexes.
* Migrations.
* Query optimization.

Database principles:

* Preserve historical football data.
* Avoid unnecessary duplication.
* Maintain data integrity.

---

# QA Agent

## Responsibility

Maintains software quality.

Responsible for:

* Testing strategy.
* Unit tests.
* Integration tests.
* Regression prevention.

Testing stack:

```text
Jest

Vitest

Supertest
```

---

# Product Agent

## Responsibility

Ensures features provide real user value.

Responsible for:

* Feature definition.
* Requirements.
* User flows.
* Prioritization.

The Product Agent prevents unnecessary complexity.

---

# Data Integration Agent

## Responsibility

Manages external football data providers.

Responsible for:

* API integrations.
* Provider abstraction.
* Data mapping.
* Synchronization processes.

Architecture:

```text
External API

↓

Provider Adapter

↓

Mapper

↓

Domain Model

↓

Database
```

---

# Documentation Agent

## Responsibility

Maintains project knowledge.

Responsible for:

* README.
* Architecture documentation.
* API documentation.
* Technical decisions.

Documentation must always match the real implementation.

---

# Performance Agent

## Responsibility

Maintains application efficiency.

Responsible for:

* Frontend optimization.
* Backend optimization.
* Database performance.
* Caching strategies.

Focus areas:

* Response times.
* Query efficiency.
* Bundle size.
* Redis usage.

---

# AI Agent

## Responsibility

Designs future artificial intelligence capabilities.

Responsible for:

* AI integrations.
* AI architecture.
* Intelligent features.

AI must always be isolated from core business logic.

---

# Agent Collaboration Rules

Agents must follow these rules:

---

## Rule 1: Respect Architecture

No agent should introduce solutions that violate established architectural decisions.

Example:

Incorrect:

```text
Backend module directly calling external football API
```

Correct:

```text
Backend module

↓

Provider Interface

↓

External Adapter
```

---

## Rule 2: Avoid Duplicate Responsibilities

Each agent owns a specific area.

Example:

Database Agent defines schemas.

Backend Agent uses repositories.

Architect Agent validates design.

---

## Rule 3: Evaluate Impact

Before implementing changes, evaluate:

* Security impact.
* Performance impact.
* Maintenance cost.
* Future scalability.

---

## Rule 4: Prefer Professional Solutions

The objective is not only making features work.

The objective is creating a project that demonstrates professional engineering practices.

---

# Current Project Development Stage

Current stage:

```text
Architecture Definition
```

Completed:

* Project vision.
* Technology stack.
* Agent responsibilities.
* Initial architecture rules.

Not yet completed:

* Backend implementation.
* Frontend implementation.
* Database implementation.
* External API integration.
* Deployment configuration.

---

# Development Priority

Implementation order:

```text
1. Project initialization

↓

2. Backend foundation

↓

3. Database setup

↓

4. Authentication system

↓

5. Football data integration

↓

6. Core football features

↓

7. Frontend implementation

↓

8. Testing

↓

9. Deployment

↓

10. Advanced features
```

---

# Decision-Making Context

When uncertain, agents should prioritize:

1. Maintainability.
2. Security.
3. Scalability.
4. Performance.
5. Developer experience.
6. Implementation speed.

The easiest solution is not always the correct solution.

---

# Final Objective

All agents work together to transform Football Hub into a professional full-stack application suitable for:

* Portfolio presentation.
* Technical interviews.
* Demonstrating advanced software engineering skills.

The project should represent how an experienced development team would design and build a modern SaaS application.