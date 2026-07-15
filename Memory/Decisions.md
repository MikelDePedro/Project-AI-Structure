# Decisions

> **Project:** Football Hub (Working Title)
> **Status:** Active

---

# Purpose

This document records **only the decisions made during the project's development**.

Unlike `TechnicalDecisions.md` in the `Docs` folder, which explains the architectural rationale behind the system, this document acts as a **living decision log**.

Every entry represents a decision that affects the implementation moving forward.

The objective is to answer questions such as:

* Why was this change made?
* When was it introduced?
* What alternatives were considered?
* Does this affect future development?

---

# Decision Rules

Only record decisions that:

* Change the project architecture.
* Modify development workflows.
* Introduce a new technology.
* Replace an existing solution.
* Affect multiple modules.
* Impact future implementations.

Do **not** record:

* Bug fixes.
* Small refactors.
* Formatting changes.
* Dependency updates.
* Temporary workarounds.

---

# Decision Format

Each decision follows the structure below.

```text id="t1g0bh"
Date

Decision

Context

Reason

Impact

Status
```

---

# Decision History

---

## 2026-07-15

### Decision

Use a **Modular Monolith** instead of Microservices.

### Context

The project architecture was evaluated before implementation.

### Reason

A modular monolith provides:

* Lower operational complexity.
* Faster development.
* Easier debugging.
* Simpler deployment.
* Clear module boundaries.

It also allows future migration to microservices if required.

### Impact

All backend modules must remain isolated and independent.

### Status

Accepted

---

## 2026-07-15

### Decision

Adopt **Clean Architecture** as the foundation for every backend module.

### Context

The project required strong separation between business logic and infrastructure.

### Reason

This architecture improves:

* Maintainability.
* Testability.
* Scalability.
* Long-term flexibility.

### Impact

Business rules must never depend directly on Prisma, Redis, HTTP clients, or external providers.

### Status

Accepted

---

## 2026-07-15

### Decision

Store football information locally instead of querying external APIs on every request.

### Context

External football APIs have request limits and variable response times.

### Reason

Using PostgreSQL and Redis reduces:

* API usage.
* Latency.
* Provider dependency.

### Impact

Every external provider must synchronize data into the local database before it becomes available to the application.

### Status

Accepted

---

## 2026-07-15

### Decision

Introduce a provider abstraction layer.

### Context

The project should remain independent from any specific football API.

### Reason

Changing providers should not require modifications to business logic.

### Impact

Every provider must implement the same internal interface.

Provider models must never reach the domain layer.

### Status

Accepted

---

## 2026-07-15

### Decision

All project documentation will be written in English.

### Context

The project is intended for an international audience and technical interviews.

### Reason

English is the standard language for professional software development.

### Impact

Documentation, comments, commit messages (when possible), and future technical artifacts should use English consistently.

### Status

Accepted

---

## 2026-07-15

### Decision

Separate project knowledge into two independent folders.

### Context

A single documentation folder would mix permanent information with constantly changing development context.

### Reason

The project now distinguishes between:

* `Docs/` → Stable documentation.
* `Memory/` → Current development context.

This reduces duplicated information and improves AI context loading.

### Impact

Permanent architectural knowledge belongs in `Docs`.

Development progress belongs in `Memory`.

### Status

Accepted

---

# Pending Decisions

The following topics have not yet been decided.

* Football data provider.
* Background job scheduler.
* Search implementation strategy.
* Email provider.
* Image optimization strategy.
* Monitoring provider configuration.
* Scheduled synchronization frequency.
* Backup strategy.

These decisions should only be added once they have been evaluated and accepted.

---

# Review Policy

A previous decision may be modified only when:

* Business requirements change.
* A significant technical limitation is discovered.
* Security concerns arise.
* Infrastructure changes make the current approach unsuitable.

Every change should create a new decision entry rather than rewriting history whenever possible.

---

# Current Architectural Direction

The project is currently committed to:

* Modular Monolith.
* Clean Architecture.
* REST APIs.
* PostgreSQL.
* Prisma ORM.
* Redis caching.
* JWT authentication.
* RBAC authorization.
* Docker-based development.
* Free deployment infrastructure.
* Feature-based frontend architecture.

Any future decision should remain compatible with these principles unless a new accepted decision explicitly replaces them.

---

# Usage

Before implementing a significant feature:

1. Review this document.
2. Verify whether a previous decision already defines the expected approach.
3. If a new long-term decision is required, add a new entry before implementation.
4. Keep historical decisions intact whenever possible.

This document should become the chronological record of the project's evolution throughout its development lifecycle.