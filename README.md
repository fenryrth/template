# AI-Directed Software Project Template

A model-agnostic repository template for software that is primarily implemented by AI coding agents while a human acts as director/product owner.

## The core idea

Use different files for different kinds of memory:

- `AGENTS.md` = **how the AI must work**
- `PROJECT.md` = **what/why the product is**
- `PROJECT_STATE.md` = **where the work is right now**
- `ROADMAP.md` = **what comes next**
- `ARCHITECTURE.md` = **how the current system is built**
- `docs/adr/` = **why important technical decisions were made**
- `docs/specs/` = **what substantial features must do**
- `.agents/skills/` = **repeatable procedures**
- `NEXT_SESSION_PROMPT.md` = **the generated bridge to a new chat**

The design intentionally separates project facts from tool-specific AI configuration.

## Why `AGENTS.md`

`AGENTS.md` is the canonical agent entry point. Tool-specific files should remain tiny adapters rather than independent sources of truth.

Included adapters:

- `CLAUDE.md` imports `AGENTS.md`.
- `.github/copilot-instructions.md` points Copilot to the canonical instructions.
- `.gemini/settings.json` configures Gemini CLI to use `AGENTS.md`.
- `.aider.conf.yml` asks Aider to read `AGENTS.md`.
- Cursor and several other agents can use `AGENTS.md` directly.

If an adapter becomes obsolete, remove the adapter — do not move project truth into a vendor-specific file.

## Why `.agents/skills/`

Agent Skills are procedures, not project memory.

This template keeps portable skills in the cross-client `.agents/skills/` convention. If a coding tool does not natively discover that location, `AGENTS.md` instructs it to inspect and load the matching `SKILL.md` manually.

Included skills:

- `session-bootstrap`
- `session-handoff`
- `documentation-sync`
- `implement-feature`
- `fix-bug`

## Start a new project

Create a new repository from this template, give it to a capable coding agent, then copy the prompt below and replace the `PROJECT DESCRIPTION` section with your idea.

```text
You are the lead designer and developer for this project. I am the project director.

Your job is to take responsibility for turning my project description into a designed, coded, documented, tested, and verified software product. Do not make me manually maintain the project Markdown files or choose ordinary implementation details that you can responsibly decide yourself.

Before substantial work:

1. Read and follow `AGENTS.md`.
2. Run the session bootstrap procedure in `.agents/skills/session-bootstrap/SKILL.md`.
3. Inspect the repository, current Git state, existing project files, and any existing code before making assumptions.
4. Use my project description below to populate and maintain `PROJECT.md`, `ARCHITECTURE.md`, `ROADMAP.md`, `PROJECT_STATE.md`, and relevant files in `docs/`.
5. Replace relevant `[TODO]` markers whenever the answer can be inferred responsibly from my description, the repository, established project decisions, or strong conventional defaults.
6. Before substantial implementation, assess whether you have enough information to proceed confidently. If essential product intent, constraints, expected behavior, or acceptance criteria are materially unclear, ask only the smallest useful set of focused questions, normally 1–3 at a time.
7. Do not ask me about details you can responsibly infer, decide as an implementation detail, discover from the repository, or safely defer.
8. For non-blocking unknowns, make the smallest sensible reversible assumption, document it when material, and continue. Keep a `[TODO]` only when a real unresolved decision remains.
9. Do not introduce new product requirements or materially change intended product behavior without my approval. You may infer reasonable implementation details, fix obvious defects, resolve inconsistencies, handle likely edge cases, and make low-risk improvements when they clearly support my stated intent.
10. Establish or update the initial architecture and roadmap, identify and verify the development commands, and keep `PROJECT_STATE.md` synchronized with repository reality.
11. After onboarding, briefly summarize your understanding of the project, identify any material assumptions or unresolved decisions, and continue with the highest-value next step unless a genuinely blocking decision requires my input.

Treat me as the director. Bring me decisions that materially affect product purpose, audience, scope, UX, business rules, brand direction, irreversible data choices, major architecture, external cost, security, privacy/legal matters, or other difficult-to-reverse choices. Handle routine design and engineering decisions autonomously.

Ask when ambiguity changes the product; infer when ambiguity only changes the implementation.

PROJECT DESCRIPTION:

[Describe what you want to build here. Write as much or as little as you naturally know: what the product is for, who it is for, what it should do, how it should feel, useful references, content or assets you already have, technical or platform requirements you already know, and anything you definitely want or do not want.]
```

You do not need to complete every detail before starting. The agent should use the repository, your description, existing decisions, and reasonable reversible assumptions to fill in ordinary gaps while bringing only material product decisions back to you.

## Normal working rhythm

You direct outcomes in ordinary language, for example:

> Implement the next item in the roadmap.

> Change the onboarding so a user can skip account creation.

> Investigate and fix the crash when an image upload is cancelled.

The agent is responsible for locating the relevant code, implementing, testing and synchronizing durable documentation.

## End a chat

Say something explicit such as:

> Round off now and prepare a handoff to a new AI chat.

The agent must follow the handoff protocol in `AGENTS.md` and `.agents/skills/session-handoff/SKILL.md`, then update `NEXT_SESSION_PROMPT.md` and give you the same prompt in its response.

## Template maintenance

Do not let instruction files grow indefinitely.

- Move procedures out of `AGENTS.md` and into Skills.
- Move detailed product behavior into specs.
- Move architecture rationale into ADRs.
- Keep only current operational state in `PROJECT_STATE.md`.
- Let Git history preserve normal implementation history.

## Recommended director rule

When a project-specific lesson becomes important enough that a future AI must know it, tell the current agent:

> Make this durable for future agents in the correct repository documentation.

The agent should choose the correct source-of-truth file rather than dumping everything into one memory file.
