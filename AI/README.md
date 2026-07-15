# README

> **Project Example:** Football Hub
> **Purpose:** AI-Assisted Development Project Structure Example

---

# Overview

This repository is an example project structure designed to demonstrate how a software application should be organized when working with Artificial Intelligence assistants during development.

The objective of this architecture is not only to organize the source code, but also to provide AI tools with the necessary context to understand:

* The project purpose.
* The technical architecture.
* The current development state.
* The responsibilities of each area.
* The decisions made during development.

This structure allows AI assistants such as GitHub Copilot or other AI development tools to work more effectively by providing specific context files, documentation, and development memory.

---

# Project Example

The example application used in this documentation is:

## Football Hub

A professional full-stack football information platform inspired by applications such as Transfermarkt, SofaScore, and FBref.

The objective of Football Hub is to demonstrate how a real-world SaaS application could be structured using:

* Frontend.
* Backend.
* Database.
* External APIs.
* Authentication.
* Security.
* Deployment.
* Testing.

---

# AI-Oriented Project Structure

The project is organized so that Artificial Intelligence can understand the application context efficiently.

Example structure:

```text
FootballHub/

├── Agents/

├── Context/

├── Memory/

├── Tasks/

├── Docs/

├── Backend/

├── Frontend/

├── Database/

├── Infrastructure/

└── README.md
```

---

# Purpose of Each Folder

## Agents

Contains the definitions of the different technical roles that an AI assistant can assume.

Examples:

```text
Agents/

├── Architect.md

├── Backend.md

├── Frontend.md

├── Database.md

├── Security.md

├── DevOps.md

└── Performance.md
```

Each file describes:

* Responsibilities.
* Technical criteria.
* Development rules.
* Decisions that the AI agent must consider.

The developer can attach only the necessary agents depending on the task.

---

## Context

Contains permanent information about the project.

Examples:

```text
Context/

├── 00ContextProject.md

├── 00ContextArchitecture.md

└── 00ContextAgents.md
```

This information rarely changes.

It defines:

* What the application is.
* Technologies used.
* Architecture principles.
* Global development rules.

---

## Memory

Contains the current state of the project.

Examples:

```text
Memory/

├── CurrentState.md

├── SessionLog.md

└── Decisions.md
```

Unlike Context files, Memory files change continuously.

They allow AI assistants to know:

* What has already been implemented.
* What was changed recently.
* What decisions were made.
* What should be done next.

---

## Tasks

Contains project planning information.

Examples:

```text
Tasks/

├── CurrentTasks.md

├── Roadmap.md

└── TechnicalDebt.md
```

Used to provide AI with:

* Current objectives.
* Pending features.
* Improvements.

---

## Docs

Contains technical documentation.

Examples:

```text
Docs/

├── Architecture/

├── Backend/

├── Frontend/

├── Database/

├── API/

└── Deployment/
```

This documentation explains how the system works.

It helps AI understand implementation details without analyzing the complete codebase.

---

# AI Development Workflow

When implementing a new feature, the developer provides AI with:

```text
Selected Agent

+

Project Context

+

Architecture Context

+

Current Memory

+

Task Description

+

Development Prompt
```

Example:

To implement player search:

```text
Agents/

Backend.md

Database.md

Performance.md


Context/

00ContextProject.md

00ContextArchitecture.md


Memory/

CurrentState.md


Task:

Implement player search functionality.
```

---

# Development Process

The recommended workflow is:

```text
1. Define the objective

↓

2. Select required AI agents

↓

3. Provide project context

↓

4. Ask AI for architectural analysis

↓

5. Review proposed solution

↓

6. Implement changes

↓

7. Test functionality

↓

8. Update Memory files

↓

9. Commit changes
```

---

# Objective

This repository structure is an example of how a professional software project can be organized to maximize productivity when working with Artificial Intelligence.

The objective is to create a development environment where AI assistants can act as specialized collaborators while maintaining:

* Architectural consistency.
* Project knowledge.
* Development history.
* Technical decision tracking.

This approach allows future projects to start with a reusable AI-assisted development framework.