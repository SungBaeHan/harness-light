# SSOT — Coding Interview Single Source of Truth

This document is the **single source of truth for the current coding interview task**.

It records:

* the original task
* interpreted requirements
* constraints
* assumptions
* implementation scope
* important technical decisions
* current implementation status
* verification status
* known limitations

The actual interview task and explicit interviewer instructions always take priority over this document.

This document must reflect the **current state of the implementation**, not an imagined future state.

---

# 1. Interview Task

## Original Task

> Paste or record the interview task here without changing its meaning.

**Status:** NOT PROVIDED

---

# 2. Objective

Describe the primary outcome that must be demonstrated.

```text
TBD
```

---

# 3. Required Functionality

List only functionality explicitly required by the interview task.

* [ ] TBD

Do not add speculative features.

---

# 4. Constraints

Record explicit constraints from the interview.

Examples may include:

* implementation time
* required language
* required framework
* allowed AI tools
* prohibited libraries or services
* runtime environment
* required input/output format
* network restrictions

Current constraints:

```text
TBD
```

---

# 5. Acceptance Criteria

Define observable conditions for completion.

Each criterion should be verifiable.

* [ ] TBD

Avoid vague criteria such as:

```text
works correctly
good architecture
production ready
```

Prefer observable criteria such as:

```text
POST /jobs returns a job identifier.

A submitted job reaches a completed or failed state.

GET /jobs/{id} returns the current state and result.
```

These examples are illustrative only and must not be treated as actual requirements.

---

# 6. Scope Classification

## MUST

Required for the primary end-to-end scenario.

```text
TBD
```

## SHOULD

Important improvements only after all MUST items work.

```text
TBD
```

## PRODUCTION

Relevant production considerations that do not need implementation unless explicitly required.

```text
TBD
```

Do not begin SHOULD or PRODUCTION work while MUST functionality is incomplete.

---

# 7. Ambiguities

Record unclear requirements.

| ID   | Ambiguity | Impact | Resolution |
| ---- | --------- | ------ | ---------- |
| A-01 | TBD       | TBD    | TBD        |

If an ambiguity is non-blocking, record a reasonable assumption and continue.

Escalate only genuinely blocking ambiguities to the human engineer.

---

# 8. Assumptions

Record assumptions that affect implementation.

| ID    | Assumption | Reason |
| ----- | ---------- | ------ |
| AS-01 | TBD        | TBD    |

Assumptions must not silently become requirements.

---

# 9. Repository State

After inspecting the provided repository, record the actual environment.

## Languages

```text
TBD
```

## Frameworks

```text
TBD
```

## Existing Components

```text
TBD
```

## Existing Tests

```text
TBD
```

## Existing Dependencies

```text
TBD
```

## Runtime / Tooling

```text
TBD
```

Do not assume repository structure before inspection.

---

# 10. Minimum End-to-End Flow

Define the smallest complete path that demonstrates the MUST requirements.

```text
TBD
```

Example only:

```text
Input
  ↓
API
  ↓
Processing
  ↓
Result
  ↓
Output
```

Replace the example with the actual flow derived from the task.

---

# 11. Implementation Architecture

Record the architecture actually selected for the interview implementation.

## Components

| Component | Responsibility | Implementation |
| --------- | -------------- | -------------- |
| TBD       | TBD            | TBD            |

## Control Flow

```text
TBD
```

## Data Flow

```text
TBD
```

Detailed architectural reasoning belongs in `docs/ARCHITECTURE.md`.

This section should remain a concise summary.

---

# 12. Technical Decisions

Record decisions that materially affect the implementation.

| ID   | Decision | Reason | Trade-off |
| ---- | -------- | ------ | --------- |
| D-01 | TBD      | TBD    | TBD       |

Focus on decisions that may need to be explained during the interview.

Do not record trivial implementation details.

---

# 13. Implementation Plan

Keep the plan short and executable.

## Phase 1 — Core

* [ ] TBD

## Phase 2 — Verification

* [ ] TBD

## Phase 3 — Important Improvements

* [ ] TBD

## Phase 4 — Final Review

* [ ] TBD

The plan may change as implementation progresses.

Update this document when a major decision or scope change occurs.

---

# 14. Current Implementation Status

Update this section during development.

## Core End-to-End

**Status:** NOT STARTED

## MUST Requirements

**Status:** NOT STARTED

## SHOULD Requirements

**Status:** NOT STARTED

## Tests

**Status:** NOT STARTED

## Final Verification

**Status:** NOT STARTED

Use:

```text
NOT STARTED
IN PROGRESS
PASS
FAIL
BLOCKED
SKIPPED
```

Do not mark PASS without verification.

---

# 15. Verification Status

Record important executable verification.

| Verification        | Command / Method | Result  |
| ------------------- | ---------------- | ------- |
| Application startup | TBD              | NOT RUN |
| Core scenario       | TBD              | NOT RUN |
| Automated tests     | TBD              | NOT RUN |

Add only relevant verification.

---

# 16. Known Limitations

Record intentional simplifications or unresolved non-critical issues.

```text
None recorded yet.
```

A limitation is not necessarily a failure if it is outside the required scope.

---

# 17. Production Considerations

Record relevant differences between the interview implementation and a production system.

| Interview Implementation | Production Consideration | Reason |
| ------------------------ | ------------------------ | ------ |
| TBD                      | TBD                      | TBD    |

Do not implement these items merely because they are listed here.

They are primarily used to demonstrate production reasoning during the technical discussion.

---

# 18. Blocking Issues

Record only issues that currently prevent required functionality from working.

```text
None.
```

If a blocking issue exists:

1. describe the actual failure
2. record relevant evidence
3. identify the next corrective action

Do not speculate without evidence.

---

# 19. Final Status

Before the implementation period ends, update:

```text
Required Functionality: NOT VERIFIED
Core End-to-End: NOT VERIFIED
Tests: NOT VERIFIED
Critical Issues: UNKNOWN
Final Demonstration: NOT VERIFIED
```

Possible final values:

```text
PASS
PARTIAL
FAIL
NOT VERIFIED
```

`PASS` requires executable verification of the required primary scenario.

---

# 20. Final Summary

Complete this section after final verification.

## Implemented

```text
TBD
```

## Verified

```text
TBD
```

## Not Implemented

```text
TBD
```

## Important Decisions

```text
TBD
```

## Known Limitations

```text
TBD
```

## Production Evolution

```text
TBD
```

---

# Final Rule

This document describes **what is actually required, implemented, and verified**.

Never record planned behavior as completed behavior.

Never convert assumptions into requirements.

Never allow this document to override the actual interview task.

Priority:

```text
Interview Task
     ↓
Explicit Human Instructions
     ↓
SSOT
     ↓
Architecture
     ↓
Implementation
```

**If it is not verified, do not claim that it works.**
