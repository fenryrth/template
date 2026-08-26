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

Give the repository to a capable coding agent and use a prompt like:

> Initialize this repository from the template. Read `AGENTS.md`, then interview the existing project files and my project description. Replace all relevant `[TODO]` placeholders, establish the initial architecture and roadmap, verify the development commands, and update `PROJECT_STATE.md`. Do not introduce new product requirements or materially change intended product behavior without my approval. You may infer reasonable implementation details, fix obvious defects, resolve inconsistencies, handle likely edge cases, and make low-risk improvements when they clearly support my stated intent. Where a product choice remains materially ambiguous, mark it clearly rather than inventing it.

You can also paste your full app idea into the same prompt.

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
