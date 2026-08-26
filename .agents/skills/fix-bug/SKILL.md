---
name: fix-bug
description: Diagnose and repair incorrect or failing software behavior. Use for bugs, regressions, crashes, failing tests, unexpected outputs, performance regressions, or reproducible defects.
compatibility: Any coding agent with repository and development-tool access.
---

# Fix Bug

## Procedure

1. Bootstrap repository context.
2. Reproduce the failure when feasible.
3. Identify the smallest reliable reproduction or failing test.
4. Trace the failure to a root cause; do not patch only the visible symptom unless that is intentionally the correct boundary.
5. Add or adjust a regression test when practical.
6. Implement the smallest safe fix.
7. Run targeted tests first, then relevant broader checks.
8. Inspect for adjacent regressions created by the same root cause.
9. Update durable documentation only if behavior, architecture, known issues or operating instructions changed.
10. Update `PROJECT_STATE.md`.

## Evidence discipline

Distinguish:

- reproduced,
- inferred,
- fixed,
- verified.

Never call a bug fixed solely because the code looks plausible.
