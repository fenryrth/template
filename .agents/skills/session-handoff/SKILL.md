---
name: session-handoff
description: Close a coding session and prepare a clean takeover by another AI. Use when the director asks to round off, stop, hand over, prepare a new chat, summarize the current coding state, or generate a prompt for the next agent.
compatibility: Any coding agent with repository file access and git inspection.
---

# Session Handoff

## Goal

Make the repository self-explanatory to a fresh agent that has no access to the current conversation.

## Procedure

### 1. Freeze scope

Do not begin new feature work after handoff starts. Finish only work needed to leave the current change coherent or explicitly mark it incomplete.

### 2. Establish repository truth

Inspect:

- `git status`
- current diff
- recent commits
- relevant tests/build/type/lint results

Do not infer Git state from memory.

### 3. Reconcile durable documentation

Update only what actually changed:

- `PROJECT.md` for product truth
- `ARCHITECTURE.md` for current architecture
- `ROADMAP.md` for priority/completion
- `docs/adr/` for consequential decisions
- `docs/specs/` for feature behavior/acceptance criteria
- `README.md` for human setup/usage
- `CHANGELOG.md` for user-visible release notes

### 4. Update `PROJECT_STATE.md` last

It must contain:

- timestamp
- current branch
- reference commit or clear uncommitted state
- working-tree condition
- current objective
- what is completed
- what is in progress
- one exact next action
- short next queue
- blockers/director decisions
- active assumptions
- verification status with commands/results
- relevant known issues
- high-value files for continuation

Remove stale state instead of appending an endless diary.

### 5. Generate `NEXT_SESSION_PROMPT.md`

Overwrite it with a self-contained prompt for the next agent.

The prompt must tell the next agent to:

1. read `AGENTS.md`,
2. read `PROJECT_STATE.md`,
3. inspect Git state/history,
4. verify docs against repository reality,
5. read only relevant project docs/ADRs/specs/skills,
6. summarize its understanding,
7. continue from the exact next action unless the director overrides it.

Add task-specific context from the handoff, but do not paste large code or duplicate entire documentation files.

### 6. Final response to director

Provide:

- Completed
- Validation
- Unresolved / risk
- Exact next action
- A complete copy-paste next-session prompt

The prompt shown to the director must match the intent of `NEXT_SESSION_PROMPT.md`.

## Quality check

Before finishing, ask internally:

> Could a competent agent with only this repository and the generated prompt continue correctly without this chat?

If not, the handoff is incomplete.
