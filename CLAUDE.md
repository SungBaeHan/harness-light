# Claude Instructions

This repository uses **harness-light**.

Before analyzing, planning, or modifying code, read `docs/RULES.md` and follow it.

## Sources of truth

1. `task/ORIGINAL_TASK.md` — the original task. Authoritative. **Never modify it.**
2. Explicit instructions from the human during the session.
3. `docs/SSOT.md` — your interpretation: requirements, assumptions, scope, design, status, verification.
4. `docs/RULES.md` — how to work.

If anything in this harness conflicts with the task or the human, follow the task and the human.

## Priority

```text
Requirements → Working Software → Verification → Critical/Major Fixes → Code Quality → Production Reasoning
```
