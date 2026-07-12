# Framework Files

Use these roles when generating Codex project settings.

## Contents

- Memory budgets and loading rules
- `AGENTS.md`
- `CONTEXT.md`
- `ACTIVE_CONTEXT.md`
- `STATUS.md`
- Optional repo-local skills

## Memory Budgets

Treat these as engineering policy inferred from context-management research, not vendor limits:

| File | Soft budget | Hard budget |
| --- | ---: | ---: |
| `CONTEXT.md` | 1,000 English words (about 1,330 tokens) | 1,500 words (about 2,000 tokens) |
| `ACTIVE_CONTEXT.md` | 300 English words (about 400 tokens) | 500 words (about 670 tokens) |
| `STATUS.md` | 500 English words (about 670 tokens) | 800 words (about 1,070 tokens) |
| Combined | 1,800 English words (about 2,400 tokens) | 2,800 words (about 3,740 tokens) |

- At the soft budget, prune duplication and stale detail during the next substantive update.
- At the hard budget, stop appending until content is removed, rewritten, or moved to a linked source-of-truth document.
- For Chinese and other languages without reliable whitespace-delimited words, use an approximate token budget or a project-calibrated character limit. Use line count only as a secondary guard and keep each file below 200 lines.
- Use `AGENTS.md` as a router. Read `CONTEXT.md` for durable project facts, `ACTIVE_CONTEXT.md` for the current workstream, and `STATUS.md` only for progress, handoff, onboarding, or project-state questions.

## AGENTS.md

Purpose: agent-facing repository entrypoint.

Include:

- where durable context lives
- always-on work rules
- how to handle current direction and status files
- routing to optional repo-local skills
- safety rules for local changes and verification

Avoid:

- long project history
- detailed architecture narratives
- large checklists better placed in `CONTEXT.md` or repo-local skills

## CONTEXT.md

Purpose: durable project facts for agents.

Include:

- project purpose
- target users or use case
- tech stack
- important commands
- architecture summary
- important paths
- external services and integrations
- invariants and constraints
- known decisions
- assumptions that need confirmation

Avoid:

- temporary task state
- detailed chronological status
- speculative plans that are not confirmed

Replace obsolete facts in place. Do not retain chronology here. Move detailed subsystem explanations, runbooks, schemas, decision history, and large command catalogs to authoritative documents, then keep a short summary and link.

## ACTIVE_CONTEXT.md

Purpose: current working direction. Overwrite it when the active direction changes.

Include:

- last updated date
- current broad direction
- current narrow focus
- current goal
- scope boundaries
- confirmed and uncertain judgments
- next step

Avoid:

- old directions
- long history
- unrelated backlog

Rewrite this file when the active goal or phase changes. Remove completed steps, resolved blockers, rejected options, and previous directions instead of appending them. When no work is active, reduce it to an explicit idle state and the next intended decision.

## STATUS.md

Purpose: human-facing scan of project state.

Include:

- last updated date
- one-sentence status
- current main line
- concise timeline
- current thinking
- next step
- risks or blockers

Update the current snapshot in place. Keep at most seven recent material changes; normally keep only the last 30 days, while allowing older entries when a slow-moving project needs them to explain the current state. Move older history to Git, release notes, a changelog, or completed plans.

## Optional .agents/skills

Create repo-local skills only when useful:

- `<reference-skill>` for project-specific reference collection and validation
- workflow skills for project-specific build/check/release/eval loops

Do not copy optional skills into every project by default.
