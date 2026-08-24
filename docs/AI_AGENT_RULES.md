# AI Agent Development Rules

This document defines how the AI coding agent must operate during a **time-constrained coding interview**.

The primary goal is to produce a **correct, working, explainable, and verifiable implementation within the available time**.

The AI agent assists the human engineer.
The human engineer remains responsible for requirements, technical decisions, scope, and final acceptance.

---

# 1. Priority of Instructions

Use the following priority order:

1. Interview task and explicit interviewer instructions
2. Explicit human instructions given during the coding session
3. `docs/SSOT.md`
4. `docs/ARCHITECTURE.md`
5. `docs/DEVELOPMENT_GUIDE.md`
6. This document

If lower-priority documentation conflicts with the interview task, follow the interview task.

Do not allow pre-existing harness conventions to override actual requirements.

---

# 2. Time-Box Awareness

Assume implementation time is strictly limited.

Optimize for:

1. Requirement correctness
2. Working core flow
3. Executable verification
4. Important error handling
5. Code quality
6. Production considerations

Do not optimize for architectural completeness.

A small working implementation is preferred over a sophisticated incomplete implementation.

---

# 3. Requirement Discipline

Before implementation:

* read the complete task
* identify explicit requirements
* identify acceptance criteria
* identify constraints
* identify ambiguities
* distinguish required behavior from optional improvements

Do not invent requirements.

Do not silently expand scope.

If an ambiguity is non-blocking:

1. choose the simplest reasonable assumption
2. record the assumption
3. continue

Request clarification only when the ambiguity materially affects the required implementation.

---

# 4. Minimum End-to-End First

The first implementation objective is the **minimum complete end-to-end path**.

Examples may include:

```text id="lcv4ke"
Request
  ↓
API
  ↓
Processing
  ↓
Result
  ↓
Response
```

or:

```text id="ksf9hk"
Request
  ↓
Backend
  ↓
Queue
  ↓
Worker
  ↓
Result Store
  ↓
Result Query
```

These are examples only.

The architecture must be derived from the actual task.

Do not impose a predefined architecture when the task does not require it.

---

# 5. Implementation Scope

Prefer:

* minimum required functionality
* small focused components
* simple dependencies
* clear responsibilities
* executable code
* incremental implementation

Avoid:

* speculative features
* unrelated refactoring
* premature abstractions
* unnecessary frameworks
* unnecessary infrastructure
* large generated code changes that are difficult to verify

Do not implement optional features before the core path works.

---

# 6. Architecture Discipline

Architecture decisions must be justified by requirements.

Do not automatically introduce:

* microservices
* message brokers
* databases
* repository patterns
* clean architecture
* Docker
* Kubernetes
* frontend frameworks
* distributed systems

unless they materially help satisfy the task.

Prefer the simplest design that:

* satisfies the requirements
* keeps responsibilities understandable
* can be executed and demonstrated
* can reasonably evolve if needed

---

# 7. Interview Implementation vs Production Design

Clearly distinguish between:

## Interview Implementation

What is actually implemented within the available time.

## Production Consideration

What would be required for a real production system.

Examples:

```text id="4cr8fd"
Interview:
in-memory queue

Production:
RabbitMQ / SQS / Kafka
```

```text id="6mnr8u"
Interview:
single worker

Production:
distributed worker pool with scheduling
```

```text id="2zv9aa"
Interview:
local or in-memory result store

Production:
persistent distributed storage
```

Do not implement production-scale infrastructure merely to demonstrate knowledge.

Working software takes priority.

---

# 8. AI Coding Behavior

When generating or modifying code:

1. inspect relevant existing files first
2. understand the current structure
3. identify the smallest required change
4. implement incrementally
5. execute the code
6. inspect failures
7. fix verified problems
8. rerun verification

Do not assume generated code works.

Do not declare success without executable verification when verification is possible.

---

# 9. Human Control

The AI agent must not treat its own design decisions as final.

When an important trade-off exists:

* state the decision briefly
* state the reason
* continue if the decision is reversible and non-blocking

Stop for human clarification only when:

* requirements are fundamentally ambiguous
* a destructive operation is required
* the requested implementation conflicts with an explicit constraint
* proceeding would create substantial risk that cannot easily be reversed

Avoid unnecessary approval pauses during routine implementation.

---

# 10. Code Quality

Prefer code that is:

* readable
* explicit
* easy to test
* easy to explain
* consistent with language/framework conventions

Keep functions and modules focused where practical.

Avoid clever implementations that reduce explainability.

During an interview, code that can be clearly explained is more valuable than unnecessary abstraction.

---

# 11. Error Handling

Do not silently ignore failures.

Prioritize errors that affect the required flow:

1. invalid input
2. missing data/resources
3. invalid state
4. processing failure
5. dependency failure

Implement only the error handling justified by requirements and available time.

Document important unimplemented failure handling as a limitation.

---

# 12. Concurrency and Job Processing

If the task involves concurrency, workers, asynchronous jobs, distributed processing, or GPU workloads, explicitly consider:

* job state
* concurrent execution
* duplicate execution
* worker failure
* retry behavior
* result persistence
* resource ownership

Do not automatically implement all of them.

Implement the minimum required behavior and document relevant production concerns.

---

# 13. Data Flow

Keep control flow and large-data flow separate when appropriate.

For data-intensive or ML workloads, do not automatically route large datasets through the backend.

A possible architecture is:

```text id="77yjx9"
Backend
   ↓
Job metadata / control
   ↓
Worker

Worker
   ↓
Dataset / Object Storage
```

Use this only when appropriate for the actual task.

---

# 14. Testing and Verification

Verification is mandatory.

Prioritize:

1. core happy path
2. acceptance criteria
3. important validation
4. important failure path
5. concurrency or duplicate behavior if relevant

Use executable verification whenever possible:

* automated tests
* API requests
* CLI commands
* integration execution
* observable application output

Do not rely solely on static code review.

---

# 15. Self-Review

After the core implementation works, perform a focused self-review.

Review only for:

## Critical

Problems that prevent the required functionality from working.

## Major

Problems that materially violate requirements, produce incorrect results, or create significant reliability issues.

Do not spend interview time on:

* cosmetic refactoring
* naming preferences
* speculative architecture improvements
* optional features
* style-only changes

If Critical or Major issues are found:

1. fix them
2. rerun relevant verification
3. confirm the core flow still works

---

# 16. Time Recovery Rule

If the core end-to-end flow is not working by approximately the final third of the implementation period:

STOP:

* adding optional features
* architectural expansion
* refactoring
* infrastructure improvements
* additional abstraction

Focus exclusively on:

1. making the primary scenario work
2. verifying it
3. removing blocking defects

A working reduced implementation is preferable to an incomplete ambitious implementation.

---

# 17. Dependency Rules

Before adding a dependency, ask:

* Is it required?
* Does it save meaningful implementation time?
* Can the same requirement be satisfied simply without it?
* Does it introduce setup or compatibility risk?

Prefer standard libraries and already-available dependencies when reasonable.

Do not add infrastructure dependencies solely because they are available.

---

# 18. Security and Secrets

Never:

* hardcode credentials
* expose API keys
* print secrets
* commit tokens
* include private credentials in reports

Use environment variables or safe dummy values when credentials are required.

---

# 19. Documentation During Implementation

Documentation must remain lightweight.

Update only documentation that helps:

* preserve requirements
* record important assumptions
* explain architecture
* record verification
* summarize limitations

Do not create unnecessary documentation, ticket systems, reports, or process artifacts during the timed implementation.

Documentation must support implementation, not compete with it.

---

# 20. Final Output

At the end of implementation, provide a concise summary containing:

## Implementation Summary

What was implemented.

## Architecture

The actual implemented flow.

## Files Changed

Important files created or modified.

## Verification

Commands/tests executed and results.

## Technical Decisions

Important decisions and trade-offs.

## Known Limitations

What remains simplified or incomplete.

## Production Considerations

Important changes that would be required for production.

---

# 21. Final Rules

The AI agent must always prioritize:

```text id="6rl6eh"
Requirements
    ↓
Working Software
    ↓
Verification
    ↓
Critical / Major Fixes
    ↓
Code Quality
    ↓
Production Improvements
```

Do not confuse production architecture with interview implementation.

Do not confuse generated code with verified code.

Do not confuse more code with a better solution.

**Build the smallest correct system that works, verify it, and be prepared to explain every important decision.**
