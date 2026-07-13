# Repository Orientation

Use this before creating or updating Codex project settings.

## Inspect First

Read enough to understand the project:

- `git status --short` and current branch
- top-level file tree
- `README*`, `AGENTS.md`, `AGENTS.override.md`, `CONTEXT.md`
- `docs/`, `runbook*`, design notes, or project planning files
- package manager and build/test config
- deploy, CI, env, schema, migration, or infrastructure config
- main source entry points when present

Do not infer the project only from directory name or old conversation.

## Coverage Standard

Build a coverage map before giving durable advice:

- docs and product intent: `README*`, `docs/`, planning notes, ADRs, runbooks
- build and tooling: package manager files, lockfiles, scripts, formatter/linter/test config
- source shape: main entry points, module boundaries, domain folders, shared libraries
- tests and quality: test directories, fixtures, CI checks, coverage or eval setup
- runtime and deployment: env examples, Docker, CI/CD, infrastructure, migrations, schemas
- project guidance and optional context: existing `AGENTS.md`, `AGENTS.override.md`, `CONTEXT.md`, `.agents/`

For small repositories, inspect these directly. For large or multi-domain repositories, use subagent fan-out when available:

- docs/product lane
- build/tooling lane
- source architecture lane
- tests/quality lane
- deploy/data/integration lane

Each lane should return only evidence read, important paths, what the area appears to do, constraints, and unknowns. Do not pass conclusions between lanes before they report.

If subagents are not available, manually sample representative paths and state that the coverage is manual. Never present sampled coverage as complete.

## Classify

- `empty`: no meaningful files, or only git metadata/placeholders.
- `existing`: repo has code, docs, config, or tests that make its purpose clear.
- `unclear`: repo has files, but purpose, owner, direction, or constraints are ambiguous.

## Understanding Summary

Before writing files, summarize:

```text
Repository classification:
Project appears to be:
Evidence read:
Coverage read:
Coverage not read:
Likely stack:
Known commands:
Important paths:
Current state:
Constraints:
Unknowns:
```

## Confirmation Gate

- For `empty`, ask the user what to build, target user, success criteria, constraints, and first milestone.
- For `unclear`, ask the smallest set of questions needed to disambiguate direction.
- For `existing`, ask the user to confirm or correct the summary before writing durable project facts.

If the user asks for a provisional setup and `CONTEXT.md` is justified, mark uncertain facts there as assumptions. Otherwise keep them in the setup response or the project's existing planning source rather than creating `CONTEXT.md` solely for provisional notes.
