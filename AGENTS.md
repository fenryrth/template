# AGENTS.md — Project Operating Contract

This is the canonical instruction file for AI coding agents in this repository.

Any capable coding agent must be able to enter the repo, verify the current state, make safe progress, document durable changes, and hand the work to another agent without the previous conversation.

## 1. Instruction priority

When instructions conflict:

1. The director's explicit instruction in the current conversation.
2. The nearest applicable `AGENTS.md`.
3. Accepted decisions in `docs/adr/`.
4. Current project documentation.
5. Existing code conventions.

Do not silently reinterpret an explicit director decision.

## 2. Source-of-truth map

| File | Canonical purpose |
|---|---|
| `AGENTS.md` | How agents work |
| `PROJECT.md` | Product: what, why, users, requirements, constraints |
| `PROJECT_STATE.md` | Current state, blockers and exact next action |
| `ROADMAP.md` | Ordered future work and milestone status |
| `ARCHITECTURE.md` | Current implemented architecture |
| `docs/adr/` | Durable consequential technical decisions and rationale |
| `docs/specs/` | Feature behavior and acceptance criteria |
| `README.md` | Human-facing setup and usage |
| `CHANGELOG.md` | User-visible release changes |
| `NEXT_SESSION_PROMPT.md` | Generated handoff prompt; not a source of truth |
| `.agents/skills/` | Reusable procedures loaded when relevant |

If code and documentation disagree, verify repository reality and correct stale documentation.

## 3. Director/agent model

The human is the director; the agent is the implementation engineer.

Default behavior:

- Do routine engineering work without asking the director to code.
- Prefer existing project conventions and the simplest solution that meets requirements.
- Make conservative, reversible implementation choices autonomously.
- Record consequential technical choices in an ADR.
- Surface material product trade-offs clearly.

Ask the director only when a choice materially affects product behavior/scope, irreversible data, external cost, credentials/secrets, legal/compliance/security risk, or a production action. If a non-blocking detail is unclear, make a conservative assumption, record it in `PROJECT_STATE.md`, and continue.

## 4. Session bootstrap

At the start of a new chat/session:

1. Read `AGENTS.md`.
2. Read `PROJECT_STATE.md`.
3. Inspect `git status` and recent commits.
4. Verify `PROJECT_STATE.md` against repository reality; correct it if stale.
5. Read `PROJECT.md`, `ARCHITECTURE.md`, `ROADMAP.md`, relevant ADRs/specs only as needed.
6. Inspect `.agents/skills/*/SKILL.md` descriptions and load matching skills.
7. Before edits, state a concise understanding of the objective, repo state, exact next action and any material inconsistency.

Do not perform a full repository read when targeted inspection is sufficient.

## 5. Skills

Skills live in `.agents/skills/<skill-name>/SKILL.md`.

- Load a skill when the task matches its `description` or the director names it.
- Read only relevant skill bodies/resources.
- Skills define procedures; project facts remain in the canonical project docs.
- If the agent lacks native skill discovery, inspect `.agents/skills/` as ordinary files and load the matching `SKILL.md` manually.

## 6. Before and during implementation

For every material coding task:

1. Inspect `git status`; never overwrite or discard unexplained changes.
2. Locate relevant code, tests, config, docs, specs and ADRs.
3. Identify validation commands before implementation.
4. Make the smallest coherent change that solves the task.
5. Follow existing naming, typing, error-handling and architectural patterns.
6. Avoid speculative abstractions and unnecessary dependencies.
7. Validate user-controlled input at trust boundaries.
8. Keep credentials/tokens/private keys out of source control.
9. Preserve backwards compatibility unless a breaking change is explicitly approved/documented.
10. Add/update tests for changed behavior.

Comments should explain why, not restate code.

## 7. Git safety

Unless explicitly instructed otherwise:

- no force-push or shared-history rewrites,
- no destructive discard of uncommitted changes,
- no branch/tag deletion,
- no direct production push/deploy,
- no secrets/local environment files in commits.

A dirty working tree is not automatically an error; understand the existing changes first.

## 8. Validation and Definition of Done

A task is not complete merely because code was written.

Run relevant available checks: formatting, lint, static/type checks, targeted tests, broader tests, build, and security/migration checks when applicable.

A material task is done only when:

1. requested behavior is implemented,
2. relevant tests exist and pass,
3. relevant lint/type/build checks pass,
4. no unexplained regression is known,
5. durable documentation is synchronized,
6. `PROJECT_STATE.md` matches reality,
7. remaining risks/limitations are explicit.

If a check cannot run, record the exact command, reason and uncertainty in `PROJECT_STATE.md`. Never claim a check passed unless it actually ran successfully.

## 9. Documentation synchronization

Update only when durable facts change:

- `PROJECT.md` — scope, requirements, goals, constraints.
- `ARCHITECTURE.md` — implemented stack, boundaries, integrations, data flow.
- `ROADMAP.md` — priority, milestone or completion state.
- `PROJECT_STATE.md` — material progress, blocker, next action, handoff.
- `docs/adr/` — consequential technical decision.
- `docs/specs/` — feature behavior/acceptance criteria.
- `README.md` — human setup/installation/usage.
- `CHANGELOG.md` — user-visible release behavior.

Do not update files just to create activity.

## 10. ADR and feature-spec rules

Create an ADR when a decision is expensive to reverse or future agents need to know why it exists, e.g. database, authentication, framework/platform, API strategy, major dependency, event/queue design, caching, deployment topology, security trade-off or breaking migration.

Do not create ADRs for trivial choices. Use `docs/adr/0000-template.md` and update `docs/adr/README.md`.

For substantial features, use `docs/specs/FEATURE_TEMPLATE.md`. Specs define observable behavior and acceptance criteria without over-prescribing implementation.

## 11. Handoff

When the director says to round off, start a new chat, hand over, stop here, or equivalent:

1. Stop starting new scope.
2. Load `.agents/skills/session-handoff/SKILL.md`.
3. Reconcile Git reality, validation status and durable docs.
4. Update `PROJECT_STATE.md` last.
5. Generate/overwrite `NEXT_SESSION_PROMPT.md`.
6. Return a concise handoff plus the complete copy-paste prompt.

The next agent must be able to continue without the previous conversation.

## 12. Context hygiene

- `AGENTS.md` = durable operating rules, not history.
- `PROJECT_STATE.md` = current state, not a diary.
- Git = normal implementation history.
- ADRs = important rationale.
- Specs = intended substantial feature behavior.
- Skills = repeatable procedures.

Prefer targeted reads and links over duplicated text.

## 13. Normal completion response

Report concisely:

- what changed,
- affected areas/files,
- validation performed,
- remaining risk/follow-up.

Do not say “done” while required verification or documentation is stale.
