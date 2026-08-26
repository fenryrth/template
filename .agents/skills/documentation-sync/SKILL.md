---
name: documentation-sync
description: Reconcile project Markdown documentation with implemented repository reality. Use after material code changes, architecture changes, roadmap changes, product-scope changes, or when docs may be stale or contradictory.
compatibility: Any coding agent with repository file access.
---

# Documentation Sync

## Principle

Update durable facts in exactly one canonical place whenever possible.

## Procedure

1. Identify what materially changed.
2. Map each change to the canonical file defined in `AGENTS.md`.
3. Inspect the existing text before editing.
4. Remove or correct stale statements.
5. Keep `PROJECT_STATE.md` focused on now, not history.
6. Use Git history rather than creating a prose diary of routine code changes.
7. Create an ADR only for consequential decisions.
8. Update `CHANGELOG.md` only for user-visible changes.
9. Check cross-references after renames or moved files.

## Anti-patterns

Do not:

- copy the same architecture description into multiple files,
- dump session transcripts into Markdown,
- update timestamps without substantive change,
- claim an unverified implementation is complete,
- turn `AGENTS.md` into a project history document.
