---
name: codex-project-settings
description: "Set up or update a repository with reusable Codex project settings: AGENTS.md, CONTEXT.md, ACTIVE_CONTEXT.md, STATUS.md, and optional repo-local skills. Use when the user wants to initialize a repo for long-term Codex work, create or repair Codex settings, adapt the Codex Project Settings Framework to an existing or empty project, add reference-backed project guidance, or ensure Codex has explicit repository coverage before writing durable settings."
---

# Codex Project Settings

Use this skill to turn any repository into a Codex-friendly project workspace. The output should be project-specific settings files, not a generic copied template.

## Core Rule

Do not generate Codex project settings before understanding the repository and confirming the intended project direction with the user. Do not claim broad repository understanding unless the evidence read, coverage limits, and unresolved unknowns are explicit. Keep project memory bounded: stable facts stay in `CONTEXT.md`, only the current narrow direction stays in `ACTIVE_CONTEXT.md`, and `STATUS.md` remains a rolling human-readable snapshot rather than an append-only history.

## Workflow

### 1. Orient The Repository

Read `references/repo-orientation.md`.

Inspect:

- file tree and git status
- existing `AGENTS.md`, `CONTEXT.md`, `ACTIVE_CONTEXT.md`, `STATUS.md`, `.agents/`
- README, docs, package/config/build/test/deploy files
- main source entry points when present

Build an explicit coverage map before summarizing. For non-trivial repositories, inspect representative docs, configs, source entry points, tests, CI/deploy, data/schema, and domain modules. When the repository is large or spans multiple areas and subagents are available, use subagent fan-out for independent coverage lanes; keep their outputs concise and evidence-based. If subagents are unavailable or unnecessary, do the coverage manually and state the limit.

Classify the repo as:

- `empty`: not enough files to infer the project
- `existing`: code/docs/config clearly show what the project is
- `unclear`: files exist, but project intent or direction is ambiguous

### 2. Confirm Project Understanding

Before writing settings:

- For `empty` or `unclear`, ask the user what the project is, target user, success criteria, constraints, and near-term direction.
- For `existing`, summarize what the repo appears to do, stack, commands, constraints, current state, coverage read, coverage not read, and unknowns.
- Ask the user to confirm or correct the summary.

Do not proceed to file writes until the project understanding is confirmed or the user explicitly asks for a provisional setup.

### 3. Plan The Settings

Read `references/framework-files.md`.

Apply its loading, retention, and soft/hard memory budgets when creating or updating the files.

Choose which files to create or update:

- `AGENTS.md`: always recommended
- `CONTEXT.md`: always recommended
- `ACTIVE_CONTEXT.md`: recommended when there is an active direction
- `STATUS.md`: recommended when the project is ongoing
- `.agents/skills/<reference-skill>/`: optional for reference-backed project decisions
- `.agents/skills/<workflow-skill>/`: optional for project-specific coding, eval, release, or research workflows

Keep optional modules out unless the user or project needs them.

### 4. Merge Safely

Read `references/merge-rules.md`.

If files already exist, merge with them. Do not silently discard user instructions, durable project facts, commands, or useful history. Preserve local conventions, update stale facts in place when there is evidence, replace confirmed obsolete active state, and keep status history within the rolling retention window defined in `references/framework-files.md`.

### 5. Add Reference Support When Needed

Read `references/reference-skill-template.md` only when the project needs research-backed decisions, papers, open-source repo comparisons, protocols, APIs, schemas, or reusable reference management.

Reference support must include the same understanding gate: first inspect the repo, then confirm project direction, then search or organize references.

### 6. Verify

After writing files:

- show the created or changed paths
- summarize the project understanding encoded into settings
- summarize repository coverage and blind spots
- report memory-file size against the soft and hard budgets
- state what was intentionally left out
- run lightweight checks such as `git diff --check` when available
- report any files that were merged instead of replaced

## File Roles

- `AGENTS.md`: agent-facing entry rules, routing, and always-on constraints
- `CONTEXT.md`: bounded durable project facts, commands, architecture, paths, constraints, and invariants; update facts in place
- `ACTIVE_CONTEXT.md`: bounded current working direction, goal, scope, decisions, and next step; overwrite when direction changes and keep no old directions
- `STATUS.md`: bounded human-facing project snapshot, recent material changes, current thinking, next step, and risks
- `.agents/skills/`: repo-local optional workflows; do not create unless needed

## Output Rules

When done, return:

1. repository classification
2. confirmed project understanding
3. repository coverage read and remaining blind spots
4. files created or updated
5. optional modules included or skipped
6. checks run
7. remaining questions or next setup step
