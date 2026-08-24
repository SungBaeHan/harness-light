# AI Development Prompt

This document defines the **execution protocol for the AI coding agent**
during a time-constrained coding interview.

The objective is to transform the interview task into a **working, verified, and explainable implementation within the available time**.

The actual interview task and explicit interviewer instructions always take priority over this document.

---

# 1. Read Core Documents

Before implementation, read the following documents:

1. `docs/SSOT.md`
2. `docs/ARCHITECTURE.md`
3. `docs/AI_AGENT_RULES.md`
4. `docs/DEVELOPMENT_GUIDE.md`
5. `docs/QA_AND_DONE.md`

Use `docs/AI_ENTRYPOINT.md` as the overall entry point and reading-order reference.

Do not assume that architecture or technology choices already exist.

The interview task defines the system to build.

---

# 2. Capture the Interview Task

Treat the complete interview task as the primary requirement source.

Before coding, extract:

## Objective

What must be built or demonstrated.

## Required Features

Functionality explicitly required by the task.

## Constraints

Examples:

* implementation time
* required language/framework
* allowed tools
* prohibited tools
* required interfaces
* required input/output formats

## Acceptance Criteria

Conditions that must be true for the solution to be considered correct.

## Ambiguities

Requirements that are unclear or open to interpretation.

## Assumptions

Reasonable assumptions made to continue implementation.

Do not invent requirements.

---

# 3. Classify Scope

Separate work into three categories.

## MUST

Required for the primary scenario to work.

## SHOULD

Important improvements to implement only after MUST items work.

## PRODUCTION

Production concerns that should be explained but do not need to be implemented unless explicitly required.

Example:

```text
MUST
- create job
- process job
- query result

SHOULD
- validation
- failure handling
- additional tests

PRODUCTION
- distributed queue
- persistent storage
- retry policy
- observability
```

The categories must be derived from the actual task.

---

# 4. Define the Minimum End-to-End Flow

Before implementation, identify the smallest complete flow that demonstrates the required behavior.

Example only:

```text
Request
  ↓
API
  ↓
Job
  ↓
Worker
  ↓
Processing
  ↓
Result
  ↓
Result Query
```

Do not impose this architecture if the task requires something different.

The minimum end-to-end flow should become the first implementation target.

---

# 5. Architecture Decision

Define only the architecture required to implement the task.

Record:

* major components
* responsibility of each component
* important data flow
* important control flow
* technology choices
* intentional simplifications

Prefer the simplest design that can:

1. satisfy requirements
2. run locally
3. be verified
4. be explained clearly

Do not introduce production-scale infrastructure unless required.

---

# 6. Implementation Plan

Before coding, create a short implementation plan.

The plan should contain:

1. files/components to create or modify
2. implementation order
3. core verification method
4. optional improvements if time remains

Keep the plan concise.

Do not wait for approval unless:

* a blocking ambiguity exists
* a destructive action is required
* an explicit human decision is necessary

Otherwise proceed directly to implementation.

---

# 7. Implement the Core Path

Implement the minimum end-to-end path first.

Rules:

* keep changes focused
* use simple dependencies
* avoid premature abstraction
* avoid unrelated refactoring
* avoid optional features
* preserve explainability

After completing the core path, execute it immediately.

Do not continue expanding the implementation until the core path works.

---

# 8. Verify the Core Path

Verification must be executable whenever possible.

Use appropriate methods such as:

* automated tests
* API requests
* CLI commands
* integration execution
* observable output

Verify:

1. application starts
2. primary input is accepted
3. required processing occurs
4. expected result is produced
5. result can be observed or queried

If verification fails:

1. inspect the actual error
2. identify the cause
3. make the smallest appropriate correction
4. rerun verification

Do not guess blindly.

---

# 9. Implement Important Secondary Requirements

Only after the core path works, implement relevant SHOULD items.

Possible examples:

* input validation
* error handling
* job state handling
* failure state
* duplicate handling
* concurrency
* additional tests
* persistence
* containerization

Prioritize based on the actual interview requirements.

Do not implement optional infrastructure merely because time remains.

---

# 10. Focused Self-Review

After implementation works, perform one focused code review.

Review only for:

## Critical

* application does not run
* primary scenario fails
* required functionality is missing
* incorrect result
* data corruption or severe runtime failure

## Major

* important requirement violation
* significant state-management problem
* important concurrency problem
* important error path missing
* implementation contradicts the intended architecture

Ignore during this review:

* cosmetic improvements
* naming preferences
* speculative refactoring
* optional architecture improvements
* unnecessary abstraction

If Critical or Major issues are found:

1. fix them
2. rerun affected tests
3. rerun the primary scenario

---

# 11. Time Recovery

Continuously protect the working solution.

If the core end-to-end flow is not working when approximately two-thirds of the implementation time has elapsed:

STOP:

* adding features
* adding infrastructure
* refactoring
* introducing abstractions
* improving architecture
* writing nonessential documentation

Focus exclusively on:

1. making the primary scenario work
2. verifying the result
3. fixing blocking defects

Do not sacrifice a working demonstration for architectural completeness.

---

# 12. Production Considerations

After the interview implementation works, identify relevant production differences.

Examples may include:

| Interview Implementation | Production Consideration           |
| ------------------------ | ---------------------------------- |
| In-memory state          | Persistent database                |
| In-memory queue          | Durable message broker             |
| Single worker            | Distributed worker pool            |
| Local dataset            | Object storage                     |
| Dummy processing         | Actual ML/GPU workload             |
| Basic logging            | Metrics, tracing, centralized logs |

Only mention production concerns relevant to the actual task.

Do not implement them unless required or clearly beneficial within the remaining time.

---

# 13. Final Verification

Before declaring completion:

1. start the application from a clean state if practical
2. execute the primary scenario
3. run relevant automated tests
4. confirm required outputs
5. inspect important error output
6. confirm no known Critical issue remains

If Docker or other infrastructure is part of the implementation, verify that the required services actually start.

Generated code is not considered complete until it has been executed and verified.

---

# 14. Final Summary

At the end, provide a concise summary.

## Implementation Summary

What was implemented.

## Architecture

Actual implemented component flow.

## Files Changed

Important files created or modified.

## Verification

Commands/tests executed and their results.

## Technical Decisions

Important implementation decisions and trade-offs.

## Known Limitations

What was intentionally simplified, incomplete, or excluded.

## Production Considerations

How the implementation could evolve for production.

---

# 15. Execution Mode

During the coding interview, operate continuously through:

```text
Understand
   ↓
Scope
   ↓
Design
   ↓
Implement
   ↓
Run
   ↓
Verify
   ↓
Self-Review
   ↓
Fix
   ↓
Final Verify
   ↓
Summarize
```

Do not pause for routine approval between stages.

Stop and request human input only when a genuinely blocking decision is required.

---

# Final Principle

**Requirements → Working Software → Verification → Review → Production Reasoning**

The objective is not to generate the largest solution.

The objective is to produce the **smallest correct implementation that works, can be verified, and can be clearly explained within the available time**.
