---
name: implement-feature
description: Implement a substantial product feature from a director request, roadmap item, or feature specification. Use when adding new user-visible behavior or a coherent new capability.
compatibility: Any coding agent with repository and development-tool access.
---

# Implement Feature

## Procedure

1. Bootstrap context according to `AGENTS.md`.
2. Determine the feature's source of truth:
   - existing spec,
   - explicit director instruction,
   - roadmap item.
3. If the feature is substantial and no spec exists, create a concise spec from `docs/specs/FEATURE_TEMPLATE.md`.
4. Ensure acceptance criteria are observable.
5. Inspect the existing architecture and relevant ADRs.
6. Design the smallest coherent implementation.
7. Implement in vertical slices where practical.
8. Add/update tests alongside behavior.
9. Run relevant validation.
10. Perform documentation sync.
11. Update `PROJECT_STATE.md` with actual status and exact next action.

## Decision rule

Do not ask the director about routine implementation choices. Escalate only material product, irreversible, costly, security-sensitive or scope-changing decisions.

## Completion

A feature is not complete until its acceptance criteria and relevant checks pass, or the exact exception is recorded.
