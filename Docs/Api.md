# ApiSpecification

> **Project:** Football Hub (Working Title)
> **Version:** 1.0.0
> **Status:** Active
> **API Version:** v1
> **Protocol:** REST over HTTPS

---

# Overview

Football Hub exposes a RESTful API consumed by the React frontend.

The API is designed to be:

* Predictable
* Consistent
* Versioned
* Secure
* Easy to consume
* Fully documented with Swagger

All endpoints return JSON.

The API follows resource-oriented design principles.

---

# Base URL

Development

```text
http://localhost:3000/api/v1
```

Production

```text
https://api.footballhub.com/api/v1
```

Every endpoint is prefixed with:

```text
/api/v1
```

Future breaking changes should introduce a new version rather than modifying existing endpoints.

Example:

```text
/api/v2
```

---

# Authentication

Authentication is based on JWT.

Protected endpoints require:

```http
Authorization: Bearer <access_token>
```

Refresh Tokens are never sent through the Authorization header.

They are stored as secure HttpOnly cookies.

---

# Response Format

Every successful response follows a consistent structure.

Example

```json
{
    "success": true,
    "data": {},
    "meta": {},
    "timestamp": "2026-07-15T15:30:00Z"
}
```

---

# Error Format

Every error follows the same structure.

```json
{
    "success": false,
    "statusCode": 404,
    "message": "Player not found",
    "error": "Not Found",
    "timestamp": "2026-07-15T15:30:00Z",
    "path": "/players/123"
}
```

Clients should never need to guess the response format.

---

# HTTP Status Codes

The API uses standard HTTP status codes.

| Code | Description             |
| ---- | ----------------------- |
| 200  | Success                 |
| 201  | Resource Created        |
| 204  | No Content              |
| 400  | Validation Error        |
| 401  | Unauthorized            |
| 403  | Forbidden               |
| 404  | Resource Not Found      |
| 409  | Conflict                |
| 422  | Business Rule Violation |
| 429  | Too Many Requests       |
| 500  | Internal Server Error   |

---

# Pagination

Collections should never return unlimited data.

Example

```http
GET /players?page=2&limit=20
```

Response

```json
{
    "success": true,
    "data": [],
    "meta": {
        "page": 2,
        "limit": 20,
        "totalItems": 3521,
        "totalPages": 177
    }
}
```

Default page size:

```text
20
```

Maximum page size:

```text
100
```

---

# Sorting

Sorting follows a common format.

Example

```http
GET /players?sort=name
```

Descending

```http
GET /players?sort=-marketValue
```

Multiple fields

```http
GET /players?sort=country,-marketValue
```

---

# Filtering

Example

```http
GET /players?nationality=Spain
```

```http
GET /players?position=Forward
```

```http
GET /players?league=Premier League
```

Filters may be combined.

---

# Searching

Global search endpoint

```http
GET /search?q=Messi
```

Response

```json
{
    "players": [],
    "teams": [],
    "competitions": [],
    "coaches": []
}
```

Search results should be ordered by relevance.

---

# Authentication Endpoints

## Register

```http
POST /auth/register
```

Request

```json
{
    "username": "johnsmith",
    "email": "john@example.com",
    "password": "StrongPassword123!"
}
```

Response

```json
{
    "success": true,
    "message": "Verification email sent."
}
```

---

## Login

```http
POST /auth/login
```

Request

```json
{
    "email": "john@example.com",
    "password": "StrongPassword123!"
}
```

Response

```json
{
    "success": true,
    "data": {
        "accessToken": "...",
        "user": {}
    }
}
```

Refresh Token is returned as a secure HttpOnly cookie.

---

## Refresh Token

```http
POST /auth/refresh
```

Response

```json
{
    "success": true,
    "data": {
        "accessToken": "..."
    }
}
```

Refresh Token rotation is performed automatically.

---

## Logout

```http
POST /auth/logout
```

Response

```json
{
    "success": true
}
```

The active Refresh Token becomes invalid.

---

# Users Endpoints

## Current User

```http
GET /users/me
```

Returns the authenticated user's profile.

---

## Update Profile

```http
PATCH /users/me
```

Fields

* Username
* Avatar
* Biography

---

## Change Password

```http
PATCH /users/me/password
```

Requirements

* Current password
* New password

---

# Players Endpoints

## List Players

```http
GET /players
```

Supports

* Pagination
* Sorting
* Filtering

---

## Get Player

```http
GET /players/{id}
```

Returns

* Personal information
* Statistics
* Current club
* Career history
* Transfers

---

## Compare Players

```http
GET /players/compare?id=1&id=2
```

Returns comparative statistics.

---

## Follow Player

```http
POST /players/{id}/follow
```

Requires authentication.

---

# Teams Endpoints

```http
GET /teams
```

```http
GET /teams/{id}
```

```http
POST /teams/{id}/follow
```

---

# Competitions Endpoints

```http
GET /competitions
```

```http
GET /competitions/{id}
```

```http
GET /competitions/{id}/standings
```

```http
GET /competitions/{id}/matches
```

---

# Matches Endpoints

```http
GET /matches
```

```http
GET /matches/{id}
```

```http
GET /matches/upcoming
```

```http
GET /matches/live
```

Future support.

---

# Favorites Endpoints

```http
GET /favorites
```

```http
POST /favorites
```

```http
DELETE /favorites/{id}
```

---

# Lists Endpoints

```http
GET /lists
```

```http
POST /lists
```

```http
PATCH /lists/{id}
```

```http
DELETE /lists/{id}
```

---

# Comments Endpoints

```http
GET /comments
```

```http
POST /comments
```

```http
PATCH /comments/{id}
```

```http
DELETE /comments/{id}
```

---

# Notifications Endpoints

```http
GET /notifications
```

```http
PATCH /notifications/read
```

---

# Administration Endpoints

Accessible only by administrators.

Examples

```http
GET /admin/users
```

```http
PATCH /admin/users/{id}/role
```

```http
POST /admin/synchronization
```

```http
GET /admin/system
```

```http
GET /admin/logs
```

---

# Validation

Every request must be validated.

Validation occurs before reaching the business logic.

Invalid requests return

```http
400 Bad Request
```

Example

```json
{
    "success": false,
    "statusCode": 400,
    "message": [
        "email must be a valid email address"
    ]
}
```

---

# Rate Limiting

Authentication endpoints should have stricter limits.

Example

```text
POST /auth/login

5 requests

per minute

per IP
```

General endpoints

```text
100 requests

per minute

per IP
```

---

# API Documentation

Swagger documentation is automatically generated.

Available endpoints

Development

```text
http://localhost:3000/api/docs
```

Production

```text
https://api.footballhub.com/api/docs
```

Every endpoint must include:

* Summary
* Description
* Parameters
* Request body
* Response examples
* Error responses
* Authentication requirements

---

# API Design Rules

Every endpoint must follow these rules.

## Use nouns

Correct

```text
GET /players
```

Incorrect

```text
GET /getPlayers
```

---

## Use plural resources

Correct

```text
/players
```

Incorrect

```text
/player
```

---

## Stateless

The API must remain stateless.

Each request contains all information required for processing.

---

## Consistency

Naming conventions should remain identical across every module.

Example

```text
GET /players

GET /teams

GET /matches

GET /competitions
```

---

## Idempotency

Operations should respect HTTP semantics.

GET

Safe

PUT

Idempotent

PATCH

Partially idempotent

DELETE

Idempotent

POST

Non-idempotent

---

# Future API Extensions

The current architecture should allow future additions without breaking existing clients.

Potential future endpoints include:

* Live matches
* Advanced analytics
* AI recommendations
* Player similarity
* Public API keys
* Webhooks
* GraphQL gateway

These features should be introduced as new modules without modifying existing API contracts.

---

# Related Documents

This document defines the public communication layer of the application.

Related documents:

* Architecture
* DatabaseDesign
* CodingStandards
* TechnicalDecisions

Every endpoint described here should be implemented according to the architectural principles defined in those documents.