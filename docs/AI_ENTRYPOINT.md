# AI Entry Point

This file is the **starting point for the AI coding agent** during a time-constrained coding interview.

Read this document first.

The goal is to produce a **working, verified, and explainable implementation within the available time**.

The actual interview task and explicit interviewer instructions always take priority over this harness.

---

# 1. Read the Core Documents

Before implementation, read the following documents in order:

1. `docs/SSOT.md`
2. `docs/ARCHITECTURE.md`
3. `docs/AI_AGENT_RULES.md`
4. `docs/DEVELOPMENT_GUIDE.md`
5. `docs/AI_DEV_PROMPT.md`
6. `docs/QA_AND_DONE.md`

Each document has a specific role:

| Document               | Purpose                                                                        |
| ---------------------- | ------------------------------------------------------------------------------ |
| `SSOT.md`              | Current task, requirements, constraints, assumptions, and implementation state |
| `ARCHITECTURE.md`      | Architecture and important technical decisions for the current task            |
| `AI_AGENT_RULES.md`    | AI behavior, scope control, verification, and safety rules                     |
| `DEVELOPMENT_GUIDE.md` | Time-constrained development strategy                                          |
| `AI_DEV_PROMPT.md`     | Execution protocol from analysis through final verification                    |
| `QA_AND_DONE.md`       | Verification and completion criteria                                           |

Do not repeatedly reread every document unless needed.

---

# 2. Understand the Interview Task

Treat the interview task as the primary source of requirements.

Before coding:

1. read the complete task
2. identify required functionality
3. identify constraints
4. identify acceptance criteria
5. identify ambiguities
6. identify the minimum end-to-end flow

Do not invent requirements.

Do not allow existing harness conventions to override the actual task.

---

# 3. Inspect the Repository

Before creating or modifying code:

1. inspect the current repository structure
2. identify existing languages and frameworks
3. identify relevant files
4. identify available tests
5. identify existing dependencies and runtime configuration

Reuse existing structure when appropriate.

Do not assume that the repository follows any predefined architecture.

---

# 4. Define the Minimum Solution

Classify the work into:

## MUST

Required for the primary scenario.

## SHOULD

Important improvements after the primary scenario works.

## PRODUCTION

Production considerations that should be explained but do not necessarily need implementation.

The first implementation target is always the smallest complete **MUST end-to-end flow**.

---

# 5. Plan Briefly, Then Implement

Before coding, provide a concise plan containing:

* interpreted requirements
* important assumptions
* proposed architecture
* files/components to create or modify
* implementation order
* verification approach

Do not spend excessive time documenting the plan.

Do not wait for routine approval.

If no genuinely blocking ambiguity exists, proceed directly to implementation.

---

# 6. Execute Continuously

Follow this execution flow:

```text id="jb6rso"
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
Fix Critical / Major Issues
   ↓
Final Verify
   ↓
Summarize
```

The implementation is not complete merely because code has been generated.

Run and verify the actual implementation.

---

# 7. Protect the Working Solution

Once the core end-to-end flow works:

* preserve the working path
* avoid unnecessary rewrites
* add improvements incrementally
* rerun relevant verification after important changes

If time becomes constrained, reduce scope rather than risking the working solution.

Working software takes priority over architectural completeness.

---

# 8. Human Control

The AI agent assists the human engineer.

The human engineer owns:

* requirement interpretation
* important technical decisions
* scope
* final acceptance

Request human input only when a decision is genuinely blocking or high-risk.

For reversible, non-blocking decisions:

1. state the assumption or decision briefly
2. continue implementation

---

# 9. Final Output

Before finishing:

1. verify the primary scenario
2. run relevant tests
3. confirm no known Critical issue remains
4. identify important limitations
5. distinguish interview simplifications from production considerations

Provide a concise final summary containing:

* implementation
* architecture
* files changed
* verification results
* technical decisions
* known limitations
* production considerations

---

# Final Rule

Use the following priority:

```text id="77kh3t"
Interview Requirements
        ↓
Human Instructions
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

**Build the smallest correct system that works, verify it, and keep it explainable.**
