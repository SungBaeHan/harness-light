# QA & Definition of Done — Coding Interview

This document defines the **verification strategy and Definition of Done (DoD)** for a time-constrained coding interview.

The objective is not to achieve production completeness.

The objective is to demonstrate that the **required behavior actually works and has been verified within the available time**.

The actual interview task and `docs/SSOT.md` take priority over this document.

---

# 1. Definition of Done

The interview implementation is considered complete when:

* [ ] MUST requirements are implemented
* [ ] Acceptance Criteria are satisfied
* [ ] Core end-to-end flow runs successfully
* [ ] Required outputs are observable and correct
* [ ] Relevant tests or executable verification have been run
* [ ] No known Critical issue blocks the primary scenario
* [ ] Important technical decisions can be explained
* [ ] Known limitations are identified
* [ ] Interview simplifications are distinguished from production considerations

Do not mark an item complete based only on code inspection.

---

# 2. Verification Principle

Use this rule:

```text id="1qzqvw"
Generated
    ≠
Implemented

Implemented
    ≠
Verified

Executed + Expected Result Observed
    =
Verified
```

Whenever practical, verification must involve actual execution.

---

# 3. Verification Priority

Verify in this order:

## Priority 1 — Application Starts

Confirm that the implementation can actually run.

Examples:

* application starts without fatal error
* required service starts
* CLI executes
* container starts

---

## Priority 2 — Core End-to-End Flow

Execute the primary scenario from beginning to end.

Example only:

```text id="v7qig3"
Input
  ↓
Entry Point
  ↓
Processing
  ↓
Result
  ↓
Observable Output
```

The actual flow must come from `docs/SSOT.md`.

This is the highest-value verification.

---

## Priority 3 — Acceptance Criteria

Verify each required Acceptance Criterion.

Use observable evidence whenever possible.

Do not infer that one criterion passes merely because another criterion passes.

---

## Priority 4 — Important Failure Paths

Verify failure behavior that materially affects the task.

Possible examples:

* invalid input
* missing resource
* processing failure
* invalid state
* dependency failure

Do not attempt exhaustive failure testing during the interview.

---

## Priority 5 — Secondary Behavior

If time remains, verify:

* additional edge cases
* concurrency
* duplicate execution
* retry behavior
* persistence
* restart behavior
* additional API scenarios

Only test these when relevant to the task.

---

# 4. Minimum QA Checklist

Before declaring completion:

```text id="0n0pqc"
[ ] Application starts
[ ] Core end-to-end scenario works
[ ] MUST requirements verified
[ ] Acceptance Criteria checked
[ ] Relevant automated tests executed
[ ] No known Critical issue remains
[ ] Final demonstration path confirmed
```

If any required item cannot be verified, record it explicitly.

Do not hide unverified behavior.

---

# 5. Automated Tests

Prefer a small number of meaningful tests.

Recommended priority:

1. core happy path
2. important validation
3. important failure path
4. state transition
5. concurrency / duplicate behavior if relevant

Do not spend excessive time maximizing test count or coverage percentage.

A few tests that validate required behavior are more valuable than many superficial tests.

---

# 6. Manual / Executable Verification

When automated tests do not sufficiently demonstrate the system, use direct execution.

Possible methods:

* `curl`
* HTTP client
* CLI invocation
* browser interaction
* application logs
* Docker execution
* direct function invocation
* integration script

Record the exact method used.

---

# 7. API Verification

If the task exposes an API, verify relevant aspects such as:

* status code
* response body
* required fields
* state transition
* validation behavior
* error response

Example only:

```text id="y6h6bu"
POST /jobs
→ 202
→ job_id returned

GET /jobs/{job_id}
→ status = completed
→ result available
```

Do not treat this example as an actual requirement.

---

# 8. Asynchronous / Worker Verification

If the implementation contains asynchronous jobs or workers, verify the complete lifecycle where practical.

Example only:

```text id="1gg9ml"
Submit
  ↓
Queued
  ↓
Running
  ↓
Completed
```

Verify relevant aspects such as:

* job creation
* worker receives work
* processing actually occurs
* state changes correctly
* result becomes observable

If failure behavior is required, verify it separately.

---

# 9. Concurrency Verification

Only when concurrency matters to the task, consider verifying:

* multiple jobs can execute
* shared state remains valid
* jobs do not overwrite each other
* duplicate processing behavior
* race conditions relevant to requirements

Do not add concurrency tests merely for architectural appearance.

---

# 10. Data / ML / GPU Verification

If the task involves data processing, machine learning, or GPU workloads, verify the required boundary.

Possible checks:

* input data is accessible
* worker receives correct metadata
* processing function executes
* result is returned or persisted
* failures become observable

If actual GPU or model execution is unavailable, clearly distinguish:

```text id="ew4gqo"
Verified:
job orchestration and processing boundary

Not Verified:
actual GPU execution
```

Never claim unexecuted GPU or model behavior was verified.

---

# 11. Docker Verification

If Docker is part of the solution, verify it explicitly.

Possible checks:

```text id="88e2lq"
docker compose up --build
docker compose ps
```

Then execute the core scenario against the running system.

A successful Docker build alone does not prove the application works.

If Docker is not required by the task or solution, skip this section.

---

# 12. Regression Verification

If modifying an existing repository, verify that important existing behavior affected by the change still works.

Focus only on behavior reasonably related to the change.

Do not attempt full-system regression testing unless explicitly required.

For a new standalone implementation, this section may be skipped.

---

# 13. Self-Review

After the implementation works, perform one focused review.

## Critical

Examples:

* application cannot start
* core scenario fails
* required functionality missing
* incorrect required result
* severe runtime failure

## Major

Examples:

* important Acceptance Criterion violated
* significant state-management defect
* important concurrency defect
* important error path broken
* implementation materially contradicts intended design

Ignore during the timed review:

* cosmetic style
* naming preferences
* speculative refactoring
* optional abstractions
* production improvements not required by the task

Fix Critical issues first.

Fix Major issues when time permits without destabilizing the working solution.

After a fix, rerun affected verification.

---

# 14. Verification Evidence

Record important verification in `docs/SSOT.md`.

Recommended format:

| Verification           | Method           | Result      |
| ---------------------- | ---------------- | ----------- |
| Application startup    | command / action | PASS / FAIL |
| Core scenario          | command / action | PASS / FAIL |
| Automated tests        | command          | PASS / FAIL |
| Important failure case | command / action | PASS / FAIL |

Do not create a separate QA report unless explicitly useful or requested.

The SSOT should remain the concise record of actual verification.

---

# 15. Failure Handling During QA

If verification fails:

1. capture the actual failure
2. inspect error output
3. identify the most likely root cause from evidence
4. make the smallest corrective change
5. rerun the failed verification
6. rerun the core scenario if the change could affect it

Avoid broad rewrites during the final verification period.

---

# 16. Time-Constrained QA

If time is running out, use this priority:

```text id="mp5kw9"
Core Scenario
     ↓
MUST Requirements
     ↓
Acceptance Criteria
     ↓
Critical Failures
     ↓
Automated Tests
     ↓
Major Failures
     ↓
Secondary / Edge Cases
```

Do not sacrifice verification of the primary scenario in order to test optional behavior.

---

# 17. Final Demonstration Check

Before the implementation period ends, confirm that the demonstration path is known.

Record:

## Start Command

```text id="uk2kr3"
TBD
```

## Primary Demonstration

```text id="a33f6k"
TBD
```

## Expected Result

```text id="ijm6xi"
TBD
```

The final demonstration should use the shortest reliable path that proves the required functionality.

---

# 18. Final Completion Status

At the end, classify the result.

## PASS

Use only when:

* required primary behavior works
* MUST requirements are satisfied
* core flow has been executed successfully
* no known Critical issue blocks the solution

## PARTIAL

Use when:

* some required behavior works
* but one or more required elements remain incomplete or unverified

## FAIL

Use when:

* the primary required scenario does not work

## NOT VERIFIED

Use when:

* implementation exists
* but executable verification was not completed

Do not convert `PARTIAL` or `NOT VERIFIED` into `PASS` for presentation purposes.

---

# 19. Final QA Summary

Before finishing, update `docs/SSOT.md` with:

```text id="qz8otn"
Application Startup:
Core End-to-End:
MUST Requirements:
Acceptance Criteria:
Automated Tests:
Critical Issues:
Final Demonstration:
```

Use actual observed results.

---

# Final Principle

Use this quality hierarchy:

```text id="2plr0v"
Required Behavior
      ↓
Executable Verification
      ↓
Correctness
      ↓
Critical / Major Reliability
      ↓
Code Quality
      ↓
Production Completeness
```

**If it was not executed and observed, do not claim that it works.**
