# ARCHITECTURE — Coding Interview

This document describes the architecture **actually selected and implemented for the current coding interview task**.

It is intentionally generic before the interview task is known.

Do not assume:

* a specific programming language
* a specific framework
* REST APIs
* databases
* message queues
* microservices
* containers
* frontend applications
* machine learning components

Architecture must be derived from the actual interview requirements.

The interview task and `docs/SSOT.md` take priority over this document.

---

# 1. Architecture Status

```text
Status: NOT DEFINED
```

Possible values:

```text
NOT DEFINED
PROPOSED
IMPLEMENTING
IMPLEMENTED
VERIFIED
```

Do not mark the architecture as `IMPLEMENTED` or `VERIFIED` until the corresponding implementation actually exists and runs.

---

# 2. Architecture Goal

Describe what the architecture must accomplish.

```text
TBD
```

Focus on the required system behavior rather than technologies.

---

# 3. Architecture Drivers

Record requirements that materially influence architecture.

Examples may include:

* synchronous vs asynchronous processing
* concurrency
* large data transfer
* background jobs
* persistence
* latency
* failure handling
* external integrations
* GPU workloads
* frontend interaction
* reproducibility

Current drivers:

```text
TBD
```

Only include drivers supported by the interview task.

---

# 4. Constraints

Record architectural constraints from the interview task or runtime environment.

| Constraint | Impact |
| ---------- | ------ |
| TBD        | TBD    |

Examples might include:

```text
Python required
No external services
Must run locally
Docker available
90-minute implementation period
```

Examples are illustrative only.

---

# 5. Implemented Architecture

Describe the architecture that is **actually being implemented**.

```text
TBD
```

Example only:

```text
Client
  ↓
API
  ↓
Application Service
  ↓
Worker
  ↓
Result Store
```

Replace this with the actual architecture.

Do not preserve an example that does not match the implementation.

---

# 6. Components

Record only components that actually exist or are actively being implemented.

| Component | Responsibility | Technology | Status      |
| --------- | -------------- | ---------- | ----------- |
| TBD       | TBD            | TBD        | NOT STARTED |

Possible status values:

```text
NOT STARTED
IN PROGRESS
IMPLEMENTED
VERIFIED
```

Avoid listing speculative production components as implemented components.

---

# 7. Component Responsibilities

For each important component, describe its responsibility.

## Component: TBD

**Responsibility**

```text
TBD
```

**Inputs**

```text
TBD
```

**Outputs**

```text
TBD
```

**Dependencies**

```text
TBD
```

Add sections only for components important enough to explain during the interview.

---

# 8. Control Flow

Describe how commands, requests, events, or jobs move through the system.

```text
TBD
```

Example only:

```text
1. Request enters the system.
2. Input is validated.
3. Work is submitted.
4. Processing occurs.
5. State/result is updated.
6. Result is returned or queried.
```

Replace with the actual flow.

---

# 9. Data Flow

Describe how important data moves through the system.

```text
TBD
```

For data-intensive tasks, explicitly distinguish **control flow** from **bulk data flow** when relevant.

Example only:

```text
Control:

Backend
   ↓
Job metadata
   ↓
Worker


Bulk data:

Dataset Storage
      ↓
    Worker
```

Do not introduce separate data paths unless the requirements justify them.

---

# 10. State Model

If the system has meaningful state transitions, record them here.

```text
Not required unless applicable.
```

Example only:

```text
PENDING
   ↓
RUNNING
   ↓
SUCCEEDED

or

FAILED
```

For asynchronous job systems, consider whether states such as `QUEUED`, `CANCELLED`, or `RETRYING` are required.

Do not implement states that provide no value for the task.

---

# 11. Interfaces

Record externally visible interfaces.

Examples:

* HTTP endpoints
* CLI commands
* functions
* events
* message formats
* frontend interactions

| Interface | Input | Output | Purpose |
| --------- | ----- | ------ | ------- |
| TBD       | TBD   | TBD    | TBD     |

Only document interfaces actually required or implemented.

---

# 12. Persistence

Describe persistence only if the task requires it.

```text
Persistence required: TBD
```

If persistence is not required, an in-memory implementation may be appropriate for the interview.

If persistence is required, record:

* stored entities
* storage technology
* important consistency requirements
* important indexes or keys if relevant

Do not introduce a database solely for architectural appearance.

---

# 13. Concurrency and Asynchronous Processing

Complete this section only when relevant.

```text
Concurrency required: TBD
Asynchronous processing required: TBD
```

If applicable, consider:

* number of concurrent workers
* task ownership
* duplicate execution
* race conditions
* shared state
* result synchronization
* worker failure

Implement only the behavior required for the interview.

Record other concerns under Production Considerations.

---

# 14. Job / Worker Model

Complete this section only when the task involves background processing or workers.

```text
Not applicable unless required.
```

If applicable, record:

## Job Creation

```text
TBD
```

## Job Dispatch

```text
TBD
```

## Worker Execution

```text
TBD
```

## Result Handling

```text
TBD
```

## Failure Handling

```text
TBD
```

---

# 15. ML / GPU Processing

Complete this section only if the task involves machine learning or GPU workloads.

```text
Not applicable unless required.
```

If applicable, consider:

* model execution boundary
* dataset location
* GPU allocation
* job scheduling
* result transfer
* failure/retry behavior

Avoid transferring large datasets through the backend unless explicitly required.

Prefer separating control flow from bulk data flow when appropriate.

---

# 16. Error Handling

Record important failure behavior.

| Failure | Expected Behavior | Implemented |
| ------- | ----------------- | ----------- |
| TBD     | TBD               | NO          |

Prioritize errors that affect required behavior.

Do not build an elaborate error framework unless required.

---

# 17. Dependency Boundaries

Record important dependency relationships.

```text
TBD
```

Prefer clear responsibility boundaries.

Avoid circular dependencies.

Do not introduce additional architectural layers unless they solve an actual problem.

---

# 18. Technical Decisions

Record important architectural decisions.

| ID     | Decision | Reason | Trade-off |
| ------ | -------- | ------ | --------- |
| ADR-01 | TBD      | TBD    | TBD       |

Only record decisions likely to matter during the technical discussion.

Examples:

* synchronous vs asynchronous execution
* in-memory vs persistent state
* direct call vs queue
* polling vs push
* single process vs separate worker

---

# 19. Interview Simplifications

Record intentional simplifications made because of the implementation time limit.

| Simplification | Reason | Consequence |
| -------------- | ------ | ----------- |
| TBD            | TBD    | TBD         |

Examples might include:

```text
In-memory storage instead of PostgreSQL
Single local worker instead of distributed workers
Dummy processing instead of actual GPU inference
```

Only record simplifications actually made.

---

# 20. Production Considerations

Describe how the interview implementation would need to evolve for production.

Consider only relevant areas such as:

* scalability
* durability
* availability
* retries
* idempotency
* observability
* authentication
* authorization
* persistent storage
* distributed workers
* resource scheduling
* deployment
* security

| Area | Interview Implementation | Production Direction |
| ---- | ------------------------ | -------------------- |
| TBD  | TBD                      | TBD                  |

Do not implement production complexity unless required.

---

# 21. Verification

Record how the architecture was verified.

| Area                | Verification Method | Result  |
| ------------------- | ------------------- | ------- |
| Application startup | TBD                 | NOT RUN |
| Core flow           | TBD                 | NOT RUN |

Architecture is not considered verified merely because the design looks reasonable.

The implemented system must run.

---

# 22. Known Limitations

Record known architectural limitations.

```text
None recorded yet.
```

Do not hide limitations.

Distinguish between:

* requirement failure
* intentional interview simplification
* production concern

These are not the same thing.

---

# 23. Final Architecture Summary

Complete this section near the end of the implementation period.

## Implemented Flow

```text
TBD
```

## Key Decisions

```text
TBD
```

## Verified Behavior

```text
TBD
```

## Main Limitations

```text
TBD
```

## Production Evolution

```text
TBD
```

---

# Final Rule

Architecture exists to support the required behavior.

Use this priority:

```text
Requirements
    ↓
Minimum Working Architecture
    ↓
Working Implementation
    ↓
Verification
    ↓
Production Evolution
```

Do not build architecture for its own sake.

**Prefer the simplest architecture that satisfies the task, works end-to-end, and can be clearly explained.**
