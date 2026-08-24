# Development Guide for AI Agents

This guide defines the development workflow for a **time-constrained coding interview** using AI-assisted development.

The primary objective is to produce a **small, working, verifiable end-to-end implementation** within the available time.

When this document conflicts with the actual interview requirements, the **interview requirements always take priority**.

---

# 1. Core Development Principle

The implementation should prioritize:

1. Correct understanding of requirements
2. Minimum viable architecture
3. Working end-to-end flow
4. Verification and testing
5. Clear technical decisions
6. Incremental improvement if time remains

Do not optimize for code volume or architectural complexity.

A small working system is preferred over a large incomplete system.

---

# 2. Requirement-First Workflow

Before writing code:

1. Read the complete interview task.
2. Extract explicit requirements.
3. Identify constraints and acceptance criteria.
4. Identify unclear or ambiguous requirements.
5. Separate:

   * Must implement
   * Should implement if time allows
   * Production considerations that do not need implementation
6. Define the minimum end-to-end flow.
7. Define how the implementation will be verified.

Do not invent requirements that are not present in the task.

If an ambiguity does not block implementation, make a reasonable assumption, document it, and continue.

Ask for clarification only when the ambiguity materially changes the required implementation.

---

# 3. Time-Boxed Development Strategy

Assume implementation time is limited.

Recommended priority:

## Phase 1 — Understand

* Analyze requirements.
* Identify the core user/system flow.
* Define the minimum deliverable.
* Choose the simplest appropriate technology and structure.

## Phase 2 — Build the End-to-End Path

Implement the smallest complete path first.

Example:

```text
Input
  ↓
API / Entry Point
  ↓
Application Logic
  ↓
Worker / Processing
  ↓
Result
  ↓
Output / Query
```

The exact architecture must be derived from the interview task.

Do not impose this example when it does not fit the requirements.

## Phase 3 — Verify

Verify the core flow immediately after it works.

Prefer executable verification such as:

* automated tests
* API requests
* CLI execution
* integration tests
* observable output

Do not rely only on code inspection.

## Phase 4 — Harden

Only after the core flow works, consider:

* validation
* error handling
* concurrency
* idempotency
* retries
* persistence
* additional tests
* containerization
* observability

Implement only items relevant to the task and available time.

## Phase 5 — Final Review

Before stopping:

* run the application
* execute the primary scenario
* run available tests
* review changed files
* identify known limitations
* record production alternatives where relevant

---

# 4. Architecture Rules

Architecture must be driven by the task.

Do not automatically impose:

* microservices
* clean architecture
* repository pattern
* message brokers
* databases
* Docker
* Kubernetes
* frontend frameworks

unless they provide clear value for the given requirements.

Prefer the **simplest architecture that preserves clear responsibilities and can be demonstrated working**.

---

# 5. Separation of Responsibilities

Even in a small implementation, avoid mixing unrelated responsibilities unnecessarily.

Typical responsibilities may include:

* interface / API
* application logic
* processing / worker
* persistence
* external integrations

Use only the layers actually needed by the task.

For example, a backend and asynchronous processing task may reasonably use:

```text
API
 ↓
Application Service
 ↓
Queue
 ↓
Worker
 ↓
Result Store
```

This is an example, not a mandatory architecture.

---

# 6. Interview Implementation vs Production Architecture

The implementation may intentionally use simplified components because of the time limit.

Examples:

| Interview Implementation | Possible Production Alternative  |
| ------------------------ | -------------------------------- |
| In-memory dictionary     | PostgreSQL / distributed storage |
| In-memory queue          | RabbitMQ / Kafka / SQS           |
| Local file               | Object storage                   |
| Single worker            | Distributed worker pool          |
| Dummy processing         | Actual ML / GPU workload         |
| Simple logging           | Centralized observability        |

Do not implement production infrastructure merely to demonstrate architectural knowledge.

Instead:

1. Make the interview implementation work.
2. Clearly identify its limitations.
3. Explain how it could evolve for production.

---

# 7. AI-Assisted Development Rules

AI tools may assist with:

* requirement analysis
* repository inspection
* implementation planning
* code generation
* test generation
* debugging
* code review
* documentation

The human remains responsible for technical decisions.

AI-generated code must not be accepted blindly.

Before considering a generated change complete:

1. Understand what was changed.
2. Check that it matches the requirement.
3. Execute it.
4. Verify the result.
5. Correct problems before continuing.

Prompts should reflect an intentional engineering workflow rather than delegating the entire task without review.

---

# 8. Code Modification Rules

Prefer:

* small focused changes
* readable code
* explicit behavior
* existing language/framework conventions
* simple dependencies
* testable components

Avoid:

* speculative features
* unrelated refactoring
* premature abstractions
* unnecessary dependencies
* large generated code dumps
* architecture that cannot be explained

---

# 9. Error Handling

Handle errors that materially affect the required flow.

Prioritize:

1. invalid input
2. missing resources
3. processing failure
4. external dependency failure
5. invalid state transitions

Do not spend excessive time building a complete error framework unless explicitly required.

Avoid silent failures.

---

# 10. Concurrency and Asynchronous Work

If the task involves background processing, jobs, workers, or distributed execution:

Consider:

* job state
* ownership
* concurrency
* duplicate execution
* retries
* failure state
* result storage

Possible job states:

```text
PENDING
  ↓
QUEUED
  ↓
RUNNING
  ↓
SUCCEEDED

or

FAILED
```

Implement only the complexity required by the task.

Document production concerns that cannot reasonably be implemented within the time limit.

---

# 11. Data and External Resources

For large data or ML workloads, avoid routing bulk data through the application backend unless required.

Prefer separating:

* control flow
* data flow

For example:

```text
Backend
   ↓
Job metadata
   ↓
Worker

Worker
   ↓
Dataset / Object Storage
```

The backend may coordinate jobs while workers access large datasets directly.

This is a design option, not a mandatory rule.

---

# 12. Testing Strategy

Testing should focus on the most important behavior first.

Recommended order:

1. Core happy path
2. Input validation
3. Important failure path
4. State transition
5. Concurrency / duplicate behavior if relevant

Prefer a few meaningful tests over many superficial tests.

At minimum, demonstrate that the required end-to-end scenario actually works.

---

# 13. Docker and Infrastructure

Docker may be used when it makes the implementation easier to reproduce or when infrastructure components are required.

Do not use Docker merely because it is available.

Examples where Docker Compose may be useful:

* PostgreSQL
* Redis
* RabbitMQ
* multiple cooperating services

If an in-memory implementation satisfies the interview requirement, complete that version first.

Containerization can be added after the core flow is working.

---

# 14. Implementation Report

At the end of implementation, provide a concise report containing:

## Summary

What was implemented.

## Architecture

The implemented component flow and major responsibilities.

## Files Changed

Important files created or modified.

## Verification

Commands or steps executed and their results.

## Technical Decisions

Important choices and why they were made.

## Limitations

What was intentionally simplified or not implemented.

## Production Considerations

How the implementation could evolve for production use.

---

# 15. Final Completion Criteria

The implementation is considered complete for the coding interview when:

* [ ] Required functionality is implemented
* [ ] Core end-to-end flow runs successfully
* [ ] Important requirements are verified
* [ ] Tests or equivalent executable verification have been performed
* [ ] No known critical failure blocks the primary scenario
* [ ] Major technical decisions can be explained
* [ ] Known limitations are identified
* [ ] The implementation can be demonstrated

---

# Final Principle

**Working software first. Production reasoning second.**

Build the smallest correct system that demonstrates the required behavior.

Then use the remaining time to improve reliability, tests, architecture, and production readiness.
