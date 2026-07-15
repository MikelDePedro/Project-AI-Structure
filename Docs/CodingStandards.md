# CodingStandards

> **Project:** Football Hub (Working Title)
> **Version:** 1.0.0
> **Status:** Active

---

# Purpose

This document defines the coding standards for the Football Hub project.

The objective is to ensure that every contributor writes code with the same conventions, making the codebase predictable, maintainable, and easy to review.

Code consistency is considered as important as code correctness.

---

# General Principles

Every contribution should follow these principles:

* Readability over cleverness.
* Simplicity over premature optimization.
* Composition over inheritance.
* Explicitness over implicit behavior.
* Consistency over personal preference.
* Maintainability over short-term convenience.

Before writing code, always ask:

* Is this the simplest solution?
* Does this scale?
* Does this introduce technical debt?
* Does this follow the project architecture?

---

# Clean Code

Code should be self-explanatory.

Comments should explain **why**, not **what**.

Prefer this:

```ts
const isPasswordExpired = user.passwordExpiresAt < new Date();
```

Instead of:

```ts
const x = user.passwordExpiresAt < new Date();
```

Avoid abbreviations unless they are universally recognized.

---

# SOLID Principles

Every module should respect SOLID principles.

## Single Responsibility Principle

Each class should have one responsibility.

Good

```text
PlayerService
```

Bad

```text
PlayerService

Authentication

Logging

Cache

Email

Synchronization
```

---

## Open / Closed Principle

Prefer extension instead of modification.

Example:

Adding a new football provider should not require modifying the existing provider implementation.

---

## Liskov Substitution Principle

Implementations should always be interchangeable.

Example:

```text
FootballProvider

↓

ApiFootballProvider

↓

FootballDataProvider
```

---

## Interface Segregation Principle

Interfaces should remain small.

Avoid large interfaces containing unrelated methods.

---

## Dependency Inversion Principle

Depend on abstractions.

Never depend directly on concrete implementations.

---

# Naming Conventions

## Files

Use **PascalCase**.

Examples

```text
PlayerService.ts

PlayersController.ts

UserRepository.ts

AuthenticationGuard.ts
```

---

## Context Files

Every folder that requires contextual information contains a file named:

```text
00ContextMemory.md
```

This file should always be the first document read inside that folder.

It contains:

* Folder purpose
* Architectural rules
* AI instructions
* Development guidelines

---

## Classes

PascalCase

```ts
PlayerService

PlayerRepository

AuthenticationGuard
```

---

## Interfaces

Prefix with **I** only when necessary.

Prefer descriptive names.

Good

```ts
FootballProvider
```

Instead of

```ts
IFootballProvider
```

unless differentiation is required.

---

## Variables

camelCase

```ts
currentPlayer

currentSeason

accessToken
```

---

## Constants

UPPER_SNAKE_CASE

```ts
MAX_LOGIN_ATTEMPTS

CACHE_TTL

JWT_EXPIRATION
```

---

## Enums

PascalCase

Enum members

UPPER_CASE

Example

```ts
enum UserRole {
    USER,
    MODERATOR,
    ADMIN
}
```

---

# Folder Structure

The folder hierarchy should remain shallow.

Every feature belongs to its own module.

Example

```text
Players/

Controllers/

Services/

Repositories/

DTO/

Entities/

Mappers/

Tests/
```

Avoid deeply nested folders unless they significantly improve organization.

---

# Import Order

Imports should always follow this order.

```ts
// External libraries

// Internal shared modules

// Feature modules

// Relative imports
```

Example

```ts
import { Injectable } from '@nestjs/common';

import { PrismaService } from '@/shared/database';

import { PlayerRepository } from '../repositories';

import { Player } from '../entities';
```

---

# Functions

Functions should:

* Have a single responsibility.
* Be small.
* Have descriptive names.
* Avoid side effects whenever possible.

Prefer

```ts
calculatePlayerAge()
```

Instead of

```ts
calculate()
```

---

# Parameters

Avoid long parameter lists.

Prefer objects.

Bad

```ts
createPlayer(
    firstName,
    lastName,
    birthDate,
    nationality,
    club,
    position
);
```

Better

```ts
createPlayer(createPlayerDto);
```

---

# Business Logic

Business logic belongs exclusively in Services.

Never place business logic inside:

* Controllers
* Repositories
* React Components
* DTOs

---

# Controllers

Controllers should:

* Receive requests.
* Validate input.
* Call services.
* Return responses.

Controllers should not:

* Query the database.
* Perform calculations.
* Access Redis.
* Access external APIs.

---

# Services

Services contain:

* Business rules.
* Application workflows.
* Coordination between repositories.
* Cache interaction.
* External provider orchestration.

Services should remain framework-independent whenever possible.

---

# Repositories

Repositories are responsible only for persistence.

Repositories should not:

* Validate business rules.
* Call external APIs.
* Perform authorization.
* Implement workflows.

---

# Error Handling

Use custom exceptions whenever appropriate.

Avoid generic errors.

Bad

```ts
throw new Error();
```

Better

```ts
throw new PlayerNotFoundException(playerId);
```

Errors should always include meaningful messages.

Sensitive information must never be exposed.

---

# Validation

Every external input must be validated.

Backend

* class-validator
* DTO Validation

Frontend

* Zod
* React Hook Form

Never trust client input.

---

# Logging

Use structured logging.

Log:

* Authentication events.
* Synchronization.
* Errors.
* Administrative actions.

Never log:

* Passwords.
* JWTs.
* Refresh Tokens.
* API secrets.
* Environment variables.

---

# Asynchronous Code

Always use async/await.

Avoid nested Promise chains.

Bad

```ts
.then()
.then()
.then()
```

Better

```ts
await service.execute();
```

---

# React Standards

Components should remain focused.

Preferred order

```text
Imports

Types

Hooks

State

Effects

Handlers

Render
```

Components should avoid containing business logic.

Business logic belongs in hooks or services.

---

# State Management

Use the right tool for the right responsibility.

## Zustand

Global UI state.

Examples

* Theme
* Sidebar
* User preferences

---

## TanStack Query

Server state.

Examples

* Players
* Teams
* Competitions
* Matches

Avoid storing API data inside Zustand.

---

# Styling

Use TailwindCSS exclusively.

Avoid inline styles unless absolutely necessary.

Reusable styles should become reusable components.

---

# API Communication

Axios should be the only HTTP client.

Create a single configured Axios instance.

All requests should pass through this instance.

Responsibilities include:

* Authentication
* Token refresh
* Error interception

---

# Testing Standards

Every business feature should include tests.

Unit tests

* Services
* Utilities
* Domain logic

Integration tests

* Controllers
* API endpoints

Critical workflows should always be tested.

---

# Git Standards

Branch naming

```text
feature/player-comparison

feature/player-search

fix/login-bug

refactor/player-module

docs/api-specification
```

Commit messages

```text
feat(players): add comparison endpoint

fix(auth): refresh token rotation

docs(database): update relationships

refactor(cache): improve invalidation strategy
```

Follow Conventional Commits whenever possible.

---

# Pull Requests

Every Pull Request should:

* Pass CI.
* Include tests when applicable.
* Avoid unrelated changes.
* Update documentation if necessary.
* Be reviewed before merging.

---

# Code Review Checklist

Before approving code, verify:

* Architecture is respected.
* SOLID principles are followed.
* No duplicated logic exists.
* Naming conventions are respected.
* Tests are included.
* Documentation is updated.
* Security implications were considered.
* Performance impact was evaluated.

---

# AI Development Guidelines

AI-generated code should:

* Respect the project architecture.
* Follow naming conventions.
* Avoid introducing unnecessary dependencies.
* Reuse existing abstractions.
* Keep modules independent.
* Avoid duplicated implementations.

Before generating code, the AI should check whether an equivalent implementation already exists.

If multiple solutions are possible, the AI should recommend the one with the lowest long-term maintenance cost.

---

# Definition of Done

A feature is considered complete only if:

* The implementation follows this document.
* Tests pass.
* Documentation is updated.
* No architectural principles are violated.
* Security has been considered.
* Code review feedback has been addressed.

Writing functional code alone is not sufficient.

---

# Related Documents

This document defines **how code should be written**.

It complements:

* Architecture
* ApiSpecification
* DatabaseDesign
* TechnicalDecisions

Every contribution to the project should comply with the standards described in this document.