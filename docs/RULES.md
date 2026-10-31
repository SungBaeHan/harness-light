# RULES — How the AI Agent Works

Goal: within the available time, produce the **smallest correct implementation that works, is verified, and can be explained**.

The human owns requirement interpretation, important technical decisions, scope, and final acceptance.
The agent assists.

---

## 1. Flow

```text
Understand → Scope → Design → Plan → [Human Checkpoint]
→ Implement core → Run → Verify → Self-review → Fix → Final verify → Summarize
```

- **One checkpoint**: after the plan, show it to the human and wait for confirmation.
- After that, work continuously. Do not pause for routine approval.

## 2. Understand

Read the whole task and inspect the repository (structure, languages, frameworks, tests, dependencies, runtime config) before touching code.

Record in `docs/SSOT.md`: objective, required functionality, constraints, acceptance criteria, ambiguities.

Ambiguity:

- **Non-blocking** → pick the simplest reasonable assumption, record it in SSOT, continue.
- **Blocking** (materially changes what must be built) → ask.

Do not invent requirements. Do not silently expand scope.

## 3. Scope

Classify every item:

| Class | Meaning |
| --- | --- |
| **MUST** | Required for the primary scenario |
| **SHOULD** | Worth doing after the primary scenario works |
| **PRODUCTION** | Explain, do not necessarily implement |

The first target is always the **minimum MUST end-to-end flow** — the smallest complete path that demonstrates the required behavior.

## 4. Design

Derive the design from the task, not from habit. Reuse the existing repository structure where it fits; do not assume a predefined architecture.
Do not introduce microservices, message brokers, databases, repository patterns, Docker, frontend frameworks, or distributed systems unless they materially help satisfy the task.

Prefer the simplest design that satisfies requirements, runs locally, can be verified, and can be explained.

Keep the implemented design and production design separate:

```text
Implemented: in-memory queue        Production: SQS / Kafka
Implemented: single worker          Production: distributed worker pool
```

Do not build production-scale infrastructure to demonstrate knowledge. Record it under PRODUCTION instead.

If the task involves concurrency, background jobs, or workers, explicitly consider job state, duplicate execution, worker failure, retries, and result persistence. Implement the minimum required; record the rest under PRODUCTION.
For data-heavy work, keep large data out of the control path (pass references, not payloads) when it matters for the task.

## 5. Plan (shown at the checkpoint)

Keep it short:

- interpreted requirements and key assumptions
- MUST / SHOULD / PRODUCTION
- minimum end-to-end flow
- design and technology choices
- files to create or modify, in order
- how the core path will be verified

## 6. Implement

- Build the core path first. Run it as soon as it exists. Do not expand until it works.
- Inspect before changing. Make the smallest change. Implement incrementally.
- Avoid speculative features, unrelated refactoring, premature abstraction, and large changes that are hard to verify.
- Add a dependency only if it is required or saves meaningful time without setup risk. Prefer what is already available.
- Prefer readable, explicit code over clever code.
- Do not silently swallow errors. Handle errors that affect the required flow; record the rest as limitations.
- Once the core path works, **protect it**: improve incrementally and rerun verification after important changes.

For reversible, non-blocking decisions: state the decision and reason in one line, then continue.

## 7. Verify

```text
Generated ≠ Implemented ≠ Verified
Executed + Expected Result Observed = Verified
```

Never mark anything done from code inspection alone when execution is possible.

Order:

1. Application starts
2. Core end-to-end flow
3. Acceptance criteria
4. Important failure paths (invalid input, missing resource, invalid state, dependency failure)
5. Secondary behavior (edge cases, concurrency, retries, persistence) — only if relevant

Use whatever executes: automated tests, `curl`/HTTP requests, CLI runs, logs, observable output.
Record the command and the observed result in SSOT.

When verification fails: capture the actual error → find the cause from evidence → make the smallest fix → rerun the failed check → rerun the core flow if it could be affected.

## 8. Self-review

After the core works, review only for:

- **Critical** — cannot start, core scenario fails, required function missing, wrong required result
- **Major** — acceptance criterion violated, significant state/concurrency defect, important error path broken

Skip cosmetics, naming, style, speculative refactoring, and optional features.
Fix Critical/Major, then rerun verification.

## 9. Time recovery

If the core end-to-end flow is not working by roughly the final third of the available time, **stop** adding features, refactoring, or expanding infrastructure.
Focus only on making the primary scenario work and verifying it.

A working reduced implementation beats an incomplete ambitious one.

## 10. Stop and ask

Stop for the human only when:

- the requirement is fundamentally ambiguous
- a destructive or irreversible operation is needed
- the implementation would conflict with an explicit constraint

## 11. Security

Never hardcode credentials, print secrets, commit tokens, or include them in reports.
Use environment variables or safe dummy values.

## 12. Documentation

Keep it light. Update `docs/SSOT.md` only where it preserves requirements, assumptions, design, verification, or limitations.
Do not create tickets, reports, or process artifacts unless asked. Documentation supports the work; it does not compete with it.

## 13. Final summary

Fill in the **Summary** section of `docs/SSOT.md` and report it:

- what was implemented
- how to run it: start command, primary demonstration, expected result
- the actual implemented flow
- important files changed
- verification commands and results
- key technical decisions and trade-offs
- known limitations
- production considerations

---

**Build the smallest correct system that works, verify it, and be ready to explain every important decision.**
