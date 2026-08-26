---
name: session-bootstrap
description: Establish reliable context at the beginning of a new coding session or handoff. Use when an agent takes over a repository, starts a new chat, resumes work, or must determine where the previous agent stopped.
compatibility: Any coding agent with repository file access and git inspection.
---

# Session Bootstrap

## Goal

Reach a verified understanding of the current project state with minimal context loading.

## Procedure

1. Read repository-root `AGENTS.md`.
2. Read repository-root `PROJECT_STATE.md`.
3. Inspect `git status`.
4. Inspect recent commit history.
5. Compare repository reality with `PROJECT_STATE.md`.
6. If inconsistent:
   - investigate the relevant files/diff,
   - correct `PROJECT_STATE.md`,
   - do not continue based on stale state.
7. Read only the project documents relevant to the active task:
   - `PROJECT.md` for product truth,
   - `ROADMAP.md` for priority,
   - `ARCHITECTURE.md` for technical boundaries,
   - matching files in `docs/adr/`,
   - matching files in `docs/specs/`.
8. Identify any other relevant skill in `.agents/skills/` by its description.

## Bootstrap output

Before edits, state briefly:

- current objective,
- branch/working-tree condition,
- what the previous agent completed,
- exact next action,
- any blocker or inconsistency.

Then proceed unless the director has given a newer instruction.

## Guardrails

- Do not read the entire repository when targeted inspection is enough.
- Do not assume `PROJECT_STATE.md` is correct without checking Git.
- Do not discard unexplained uncommitted changes.
