# Repository Orientation

Use this before creating or updating Codex project settings.

## Inspect First

Read enough to understand the project:

- `git status --short` and current branch
- top-level file tree
- `README*`, `AGENTS.md`, `CONTEXT.md`, `ACTIVE_CONTEXT.md`, `STATUS.md`
- `docs/`, `runbook*`, design notes, or project planning files
- package manager and build/test config
- deploy, CI, env, schema, migration, or infrastructure config
- main source entry points when present

Do not infer the project only from directory name or old conversation.

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

If the user asks for a provisional setup, mark uncertain facts as assumptions in `CONTEXT.md`.
