---
name: codex-project-settings
description: "Set up or update a repository with reusable Codex project settings: AGENTS.md, CONTEXT.md, ACTIVE_CONTEXT.md, STATUS.md, and optional repo-local skills. Use when the user wants to initialize a repo for long-term Codex work, create or repair Codex settings, adapt the Codex Project Settings Framework to an existing or empty project, or add reference-backed project guidance."
---

# Codex Project Settings

Use this skill to turn any repository into a Codex-friendly project workspace. The output should be project-specific settings files, not a generic copied template.

## Core Rule

Do not generate Codex project settings before understanding the repository and confirming the intended project direction with the user.

## Workflow

### 1. Orient The Repository

Read `references/repo-orientation.md`.

Inspect:

- file tree and git status
- existing `AGENTS.md`, `CONTEXT.md`, `ACTIVE_CONTEXT.md`, `STATUS.md`, `.agents/`
- README, docs, package/config/build/test/deploy files
- main source entry points when present

Classify the repo as:

- `empty`: not enough files to infer the project
- `existing`: code/docs/config clearly show what the project is
- `unclear`: files exist, but project intent or direction is ambiguous

### 2. Confirm Project Understanding

Before writing settings:

- For `empty` or `unclear`, ask the user what the project is, target user, success criteria, constraints, and near-term direction.
- For `existing`, summarize what the repo appears to do, stack, commands, constraints, current state, and unknowns.
- Ask the user to confirm or correct the summary.

Do not proceed to file writes until the project understanding is confirmed or the user explicitly asks for a provisional setup.

### 3. Plan The Settings

Read `references/framework-files.md`.

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

If files already exist, merge with them. Do not overwrite user instructions, project facts, commands, or status history. Preserve local conventions and only add missing structure or update stale sections when there is evidence.

### 5. Add Reference Support When Needed

Read `references/reference-skill-template.md` only when the project needs research-backed decisions, papers, open-source repo comparisons, protocols, APIs, schemas, or reusable reference management.

Reference support must include the same understanding gate: first inspect the repo, then confirm project direction, then search or organize references.

### 6. Verify

After writing files:

- show the created or changed paths
- summarize the project understanding encoded into settings
- state what was intentionally left out
- run lightweight checks such as `git diff --check` when available
- report any files that were merged instead of replaced

## File Roles

- `AGENTS.md`: agent-facing entry rules, routing, and always-on constraints
- `CONTEXT.md`: durable project facts, commands, architecture, paths, constraints, and invariants
- `ACTIVE_CONTEXT.md`: current working direction, current goal, scope, decisions, and next step; overwrite when direction changes
- `STATUS.md`: human-facing brief project state, timeline, current thinking, next step, and risks
- `.agents/skills/`: repo-local optional workflows; do not create unless needed

## Output Rules

When done, return:

1. repository classification
2. confirmed project understanding
3. files created or updated
4. optional modules included or skipped
5. checks run
6. remaining questions or next setup step
