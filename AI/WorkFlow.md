# DevelopmentWorkflow

> **File:** DevelopmentWorkflow.md
> **Project:** Football Hub (Working Title)
> **Purpose:** Define the professional workflow for developing Football Hub using AI assistants with limited agent functionality.

---

# Development Model

Football Hub is developed using a **Human + AI Assisted Engineering Workflow**.

Because the available AI tools may not support persistent custom agents, the project uses a context-driven approach.

Instead of creating permanent AI agents inside the platform, each development session manually provides the AI with:

1. The required agent context.
2. The current project context.
3. The current development state.
4. The relevant technical documentation.
5. A specific development prompt.

The AI reconstructs the required role and project understanding from these files.

---

# AI Session Architecture

Each AI interaction should follow this structure:

```text id="m4p8x2"
AI Assistant

+

Agent Context File

+

Project Context Files

+

Current Memory Files

+

Feature Requirements

+

Development Prompt

=

Specialized Development Session
```

---

# Required Files Before Starting Any Session

The minimum context package should contain:

```text id="x7q3n9"
/Agents

The selected specialist agent.


/Context

Global project information.


/Memory

Current implementation state.


/Tasks

Current objectives.
```

---

# Context Loading Strategy

Not every file should be provided every time.

The developer should select the necessary context depending on the task.

---

# Always Include

These files should normally be included in almost every session:

```text id="q5m8v2"
00ContextProject.md

00ContextArchitecture.md

00ContextAgents.md

CurrentState.md
```

Reason:

The AI needs to understand:

* What Football Hub is.
* How the system is designed.
* Which engineering rules exist.
* What has already been implemented.

---

# Include Depending On The Task

## Backend Development

Include:

```text id="h8n4p6"
/Agents/Backend.md

/Agents/Database.md

/Agents/Security.md

/Agents/QA.md
```

Additional:

```text id="z3m7x9"
/Database documentation

/API documentation
```

---

## Frontend Development

Include:

```text id="w6q2m8"
/Agents/Frontend.md

/Agents/Product.md

/Agents/Performance.md

/Agents/QA.md
```

Additional:

```text id="r9x5n3"
/Frontend documentation

/UI requirements
```

---

## Database Changes

Include:

```text id="p4m8q1"
/Agents/Database.md

/Agents/Architect.md

/Agents/Backend.md
```

Additional:

```text id="n7q3x5"
/Database schema documentation

Current Prisma schema
```

---

## Security Changes

Include:

```text id="v8m2q6"
/Agents/Security.md

/Agents/Backend.md

/Agents/Architect.md
```

---

## Deployment Changes

Include:

```text id="k5n9x3"
/Agents/DevOps.md

/Agents/Security.md

/Agents/Architect.md
```

---

# Development Session Workflow

Every development session follows this process.

---

# Step 1: Define The Objective

Before opening the AI chat, define:

* Feature to implement.
* Expected behavior.
* Technical constraints.
* Related modules.

Example:

```text id="b7m4q8"
Implement the Player Search feature.

Requirements:

- Users can search players by name.
- Results must be paginated.
- Use existing football data architecture.
- Avoid direct external API calls.
- Use Redis caching where appropriate.
```

---

# Step 2: Select Required Agents

Choose the AI roles needed.

Example:

Feature:

"Implement player comparison."

Selected agents:

```text id="m9x3p7"
Primary:

Backend Agent


Support:

Frontend Agent

Database Agent

Performance Agent

QA Agent
```

---

# Step 3: Attach Context Files

The Copilot chat should receive:

Example:

```text id="t6q8n4"
00ContextProject.md

00ContextArchitecture.md

00ContextAgents.md

CurrentState.md

Backend.md

Database.md

QA.md
```

---

# Step 4: Use Development Prompt Template

Every AI request should follow this structure.

---

# Standard Development Prompt

```text
You are working as a Senior Software Engineer specialized in this project.

Project:

Football Hub.

Your role:

[INSERT AGENT ROLE]

You must follow the rules defined in the attached context files.

Before writing code:

1. Analyze the current architecture.
2. Review existing implementation.
3. Identify possible technical risks.
4. Explain your recommended approach.
5. Wait for approval before generating large amounts of code.

When implementing:

- Follow Clean Architecture principles.
- Respect existing project patterns.
- Avoid duplicated logic.
- Prioritize maintainability.
- Consider security and performance.
- Include necessary tests.
- Update relevant documentation.

Current objective:

[DESCRIBE FEATURE OR TASK]

Expected result:

[DESCRIBE WHAT SHOULD EXIST AFTER IMPLEMENTATION]
```

---

# Step 5: Analysis Before Implementation

The first AI response should not generate code.

The AI should provide:

```text id="c2m7x9"
Current understanding

↓

Possible solutions

↓

Recommended solution

↓

Architecture impact

↓

Implementation plan
```

---

# Step 6: Implementation Request

After reviewing the plan:

Use:

```text
Proceed with the implementation.

Generate the required files following the proposed architecture.

For each file explain:

- Purpose.
- Location.
- Why it is needed.

Include tests where applicable.
```

---

# Step 7: Validation Phase

After implementation:

Ask the AI to review:

```text
Review the implemented feature.

Act as:

- Senior Developer.
- Security Reviewer.
- QA Engineer.

Check:

- Architecture consistency.
- SOLID principles.
- Security issues.
- Performance problems.
- Missing tests.
- Possible technical debt.
```

---

# Step 8: Update Memory Files

At the end of every important session update:

---

# CurrentState.md

Purpose:

Store the current project reality.

Contains:

* Completed modules.
* Current implementation.
* Pending work.
* Known problems.

Example:

```text
Authentication module completed.

Implemented:

- User registration.
- Login.
- JWT authentication.
- Refresh token rotation.

Pending:

- Email verification.
- Password recovery.
```

---

# SessionLog.md

Purpose:

Store development history.

Contains:

* Date.
* Objective.
* Changes made.
* Problems discovered.
* Next action.

Example:

```text
Session:

Implemented Player module foundation.


Changes:

- Created Player entity.
- Added repository pattern.
- Added service layer.


Next:

Connect external football provider.
```

---

# Decisions.md

Purpose:

Store important architectural decisions.

Only include decisions with long-term impact.

Example:

```text
Decision:

Use modular monolith architecture.

Reason:

Provides scalability while reducing deployment complexity.
```

---

# Tasks.md

Purpose:

Maintain development roadmap.

Contains:

* Current tasks.
* Future improvements.
* Bugs.
* Technical debt.

Example:

```text
Current:

Implement player search.


Next:

Create team module.


Future:

AI football assistant.
```

---

# Daily Developer Routine

A normal development day:

```text id="y6m3q8"
1.

Open project.


2.

Review CurrentState.md.


3.

Select today's objective.


4.

Choose required AI agents.


5.

Attach context files.


6.

Send standard development prompt.


7.

Review AI analysis.


8.

Approve implementation.


9.

Test changes.


10.

Update memory files.


11.

Commit changes.
```

---

# Git Commit Workflow

Each completed task should create a meaningful commit.

Examples:

Feature:

```bash
git commit -m "feat(players): implement player search endpoint"
```

Bug fix:

```bash
git commit -m "fix(auth): validate refresh token expiration"
```

Documentation:

```bash
git commit -m "docs: update architecture documentation"
```

---

# Important Rules

## Never Start Coding Without Context

The AI should always know:

* Project architecture.
* Current state.
* Development objective.

---

## Never Give Only A Feature Name

Bad:

```text
Create authentication.
```

Good:

```text
Implement refresh token rotation in the existing authentication module.

Follow current security architecture.

Review database implications before coding.
```

---

## Never Trust Generated Code Without Review

Always verify:

* Architecture.
* Security.
* Tests.
* Maintainability.

---

# Final Workflow Objective

This workflow allows the developer to simulate a professional software team using free AI tools.

The AI does not permanently remember the project.

The project memory is created through:

* Context files.
* Agent files.
* Development state files.
* Technical decisions.

Every AI session reconstructs the development environment from these documents.

The result is a repeatable, scalable workflow where each new feature starts with the correct technical context and produces consistent professional-quality implementations.