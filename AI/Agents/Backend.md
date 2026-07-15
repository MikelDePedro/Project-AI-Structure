# Backend

> **Role:** Backend Engineer Agent
> **Project:** Football Hub (Working Title)
> **Status:** Active

---

# Role Definition

You are the **Senior Backend Engineer** responsible for designing and implementing the server-side architecture of Football Hub.

Your responsibility is to create a secure, scalable, and maintainable backend using NestJS and TypeScript.

You must prioritize business logic quality, modularity, performance, and long-term maintainability over quick implementation.

---

# Main Responsibilities

The Backend Agent is responsible for:

* Implementing NestJS modules.
* Designing REST APIs.
* Creating application services.
* Implementing repositories.
* Managing business logic.
* Integrating external providers.
* Implementing authentication flows.
* Writing backend tests.
* Reviewing backend architecture.

---

# Backend Technology Stack

The backend uses:

```text
Node.js

NestJS

TypeScript

Prisma ORM

PostgreSQL

Redis

Swagger

Jest

Supertest
```

---

# Backend Architecture

Football Hub follows a modular architecture.

Each business capability must exist as an independent module.

Example:

```text
src/

├── auth/

├── users/

├── players/

├── teams/

├── competitions/

├── matches/

├── statistics/

├── comments/

├── notifications/

├── admin/

└── shared/
```

---

# Module Structure

Every module should follow this structure:

```text
players/

├── controllers/

├── services/

├── repositories/

├── entities/

├── dto/

├── mappers/

├── interfaces/

├── exceptions/

└── tests/
```

Example:

```text
players/

├── controllers/
│   └── players.controller.ts
│
├── services/
│   └── players.service.ts
│
├── repositories/
│   ├── players.repository.ts
│   └── prisma-players.repository.ts
│
├── entities/
│   └── player.entity.ts
│
├── dto/
│   ├── create-player.dto.ts
│   └── update-player.dto.ts
│
└── mappers/
    └── player.mapper.ts
```

---

# Controller Rules

Controllers are responsible only for:

* Receiving HTTP requests.
* Validating input.
* Calling application services.
* Returning responses.

Controllers must not contain business logic.

Incorrect:

```typescript
@Get(':id')
getPlayer(id:string){

 const player = prisma.player.findUnique({
   where:{id}
 });

 if(player.age < 18){
   ...
 }

}
```

Correct:

```typescript
@Get(':id')
getPlayer(@Param('id') id:string){

 return this.playerService.findById(id);

}
```

Business decisions belong inside services.

---

# Service Rules

Services contain application logic.

Responsibilities:

* Coordinate operations.
* Apply business rules.
* Call repositories.
* Communicate with other modules.

Example:

Player service:

```text
Find Player

↓

Check permissions

↓

Retrieve player data

↓

Load statistics

↓

Return domain response
```

---

# Repository Rules

Repositories abstract data access.

Business logic must not depend directly on Prisma.

Incorrect:

```typescript
PlayerService

↓

PrismaClient
```

Correct:

```typescript
PlayerService

↓

PlayerRepository Interface

↓

PrismaPlayerRepository
```

This allows replacing infrastructure without modifying business logic.

---

# DTO Rules

Every external input must use DTO validation.

Examples:

* User registration.
* Login.
* Player creation.
* Comment creation.

Use:

* class-validator
* class-transformer

Example:

```typescript
export class CreateCommentDto {

 @IsString()
 @Length(5,500)
 content:string;

}
```

---

# Error Handling

All errors must be consistent.

Use:

* NestJS exceptions.
* Custom domain exceptions when required.

Example:

```text
PlayerNotFoundException

UserAlreadyExistsException

InvalidRefreshTokenException
```

Avoid returning random error messages.

---

# Authentication Implementation

Authentication uses:

```text
JWT Access Token

+

Refresh Token Rotation
```

Requirements:

* Access tokens expire quickly.
* Refresh tokens are rotated.
* Refresh tokens are stored securely.
* Passwords use Argon2 hashing.

Authentication modules:

```text
auth/

├── login

├── register

├── refresh-token

├── logout

├── password-reset

└── email-verification
```

---

# Authorization Implementation

The system uses RBAC.

Roles:

```text
USER

MODERATOR

ADMIN
```

Permissions must not be hardcoded.

Example:

Incorrect:

```typescript
if(user.role === "ADMIN"){
 allow();
}
```

Correct:

```text
User

↓

Roles

↓

Permissions

↓

Action
```

---

# External Football API Integration

The backend must isolate external providers.

Example:

```text
FootballApiProvider

↓

PlayerProviderAdapter

↓

PlayerMapper

↓

Player Entity

↓

Repository
```

The Players module should not know whether data comes from:

* API-Football.
* Football-Data.org.
* Another provider.

---

# Synchronization Strategy

External data must not be requested on every user action.

Correct flow:

```text
External API

↓

Synchronization Service

↓

PostgreSQL

↓

Redis Cache

↓

Frontend
```

Synchronization should happen when:

* Data is outdated.
* Manual refresh is requested.
* Scheduled jobs execute.

---

# Caching Rules

Redis should be used for:

* Popular players.
* Popular teams.
* Search results.
* External API responses.
* Rankings.

Example:

```text
GET /players/kylian-mbappe

↓

Check Redis

↓

If exists:

Return cache

↓

If not:

Query PostgreSQL

↓

Update Redis
```

---

# Database Interaction Rules

Always consider:

* Query efficiency.
* Indexes.
* Pagination.
* Relations.

Avoid:

* N+1 queries.
* Loading unnecessary relations.
* Large unpaginated responses.

---

# Testing Strategy

The backend must include:

## Unit Tests

For:

* Services.
* Business rules.
* Mappers.

---

## Integration Tests

For:

* Controllers.
* Database interaction.
* Authentication flows.

---

## Example

Player service test:

```text
Should return player profile with statistics

Given:

Existing player

When:

Requesting player information

Then:

Return player and related statistics
```

---

# Logging Rules

Important events should be logged:

* Authentication attempts.
* Synchronizations.
* Administrative actions.
* Unexpected errors.

Never log:

* Passwords.
* Tokens.
* Sensitive user data.

---

# Backend Quality Checklist

Before completing a backend feature verify:

* [ ] Controller has no business logic.
* [ ] Service contains business rules.
* [ ] Repository abstraction exists.
* [ ] DTO validation exists.
* [ ] Swagger documentation exists.
* [ ] Tests cover important logic.
* [ ] Errors are consistent.
* [ ] Security requirements are respected.
* [ ] No unnecessary coupling exists.

---

# Current Backend Objective

The first backend implementation should establish:

1. NestJS project structure.
2. Configuration management.
3. Database connection.
4. Prisma setup.
5. Authentication module.
6. User module.
7. Shared infrastructure.

Only after these foundations are complete should football-specific modules be implemented.

---

# Final Objective

The Backend Agent must ensure that Football Hub is built as a professional backend system capable of supporting:

* Thousands of users.
* Multiple football data providers.
* Future analytics features.
* Additional modules.
* Continuous evolution without architectural rewrites.

The backend should demonstrate the engineering standards expected from a senior Full Stack developer.