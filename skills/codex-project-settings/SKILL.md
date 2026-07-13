---
name: codex-project-settings
description: "Set up or update a repository with native Codex AGENTS.md guidance plus optional on-demand CONTEXT.md and repo-local skills. Use when the user wants to initialize a repo for long-term Codex work, create or repair Codex settings, adapt the Codex Project Settings Framework to an existing or empty project, add reference-backed project guidance, reduce project-instruction context, or ensure Codex has explicit repository coverage before writing durable settings."
---

# Codex Project Settings

Use this skill to turn a repository into a Codex-friendly workspace. Produce only project-specific files that have a clear role; do not copy the full framework by default.

## Core Rule

Do not generate durable project settings before understanding the repository and confirming the intended direction with the user. Do not claim broad repository understanding unless the evidence read, coverage limits, and unresolved unknowns are explicit.

Treat `AGENTS.md` as the natively discovered project-guidance file. Codex also supports `AGENTS.override.md` as a replacement instruction filename. Treat `CONTEXT.md` as an optional ordinary Markdown document that Codex reads only when the prompt, `AGENTS.md`, or another loaded workflow explicitly routes to it. Never describe it as Codex-native memory or assume it is automatically loaded.

## Workflow

### 1. Orient The Repository

Read `references/repo-orientation.md`.

Inspect:

- file tree and git status
- existing `AGENTS.md`, `AGENTS.override.md`, `CONTEXT.md`, `.agents/`
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

Apply its native-discovery rules, conditional file criteria, loading routes, retention policy, Git policy, and soft/hard budgets.

Choose which files to create or update:

- `AGENTS.md`: create or repair unless the user declines or the existing guidance is already sufficient
- `CONTEXT.md`: create only when durable project facts are not already clear in authoritative checked-in docs and would help across tasks
- `.agents/skills/<reference-skill>/`: optional for reference-backed project decisions
- `.agents/skills/<workflow-skill>/`: optional for project-specific coding, eval, release, or research workflows

Keep optional files and modules out unless the user or project needs them. Avoid duplicating commands, rules, architecture, or status across files; choose one source of truth and link to it.

For each selected file, decide whether it is shared or local:

- commit shared repository rules and durable team context
- keep personal defaults in `~/.codex/AGENTS.md`
- gitignore volatile or private local state only when that behavior is intentional
- explain that ignored files will not reach another machine, teammate, or remote Codex environment

Keep native discovery accurate:

- Codex reads one project instruction file per directory, from the project root to the session's starting working directory
- `AGENTS.override.md` replaces `AGENTS.md` at the same directory level; it is not additive
- `project_doc_fallback_filenames` provides fallback names, not extra files to load alongside `AGENTS.md`
- use nested `AGENTS.md` only for subtree-specific rules, and verify the intended working directory when relying on it

### 4. Merge Safely

Read `references/merge-rules.md`.

If files already exist, merge with them. Do not silently discard user instructions, durable project facts, commands, or useful history. Preserve local conventions and update stale facts in place when there is evidence.

When two files repeat the same fact or rule, preserve one canonical copy and replace the duplicate with a short link or routing instruction. Do not move operational commands out of `AGENTS.md` when Codex needs them on every relevant task.

### 5. Add Reference Support When Needed

Read `references/reference-skill-template.md` only when the project needs research-backed decisions, papers, open-source repo comparisons, protocols, APIs, schemas, or reusable reference management.

Reference support must include the same understanding gate: first inspect the repo, then confirm project direction, then search or organize references.

### 6. Verify

After writing files:

- show the created or changed paths
- summarize the project understanding encoded into settings
- summarize repository coverage and blind spots
- distinguish native `AGENTS.md` instructions from optional on-demand context
- report the selected Git tracking policy and its consequences
- report optional context-file size against the soft and hard budgets
- report the combined discovered project-instruction size against Codex's configured limit when practical
- verify any nested guidance from the working directory that is expected to load it
- state what was intentionally left out
- run lightweight checks such as `git diff --check` when available
- report any files that were merged instead of replaced

## File Roles

- `AGENTS.md`: natively discovered repository rules, exact commands, verification requirements, and optional-document routing
- `CONTEXT.md`: optional bounded durable project facts, architecture summary, constraints, invariants, and links to authoritative docs; update facts in place
- `.agents/skills/`: repo-local optional workflows; do not create unless needed

## Output Rules

When done, return:

1. repository classification
2. confirmed project understanding
3. repository coverage read and remaining blind spots
4. files created or updated
5. native loading and on-demand routing behavior
6. Git tracking choices
7. optional files and modules included or skipped, with reasons
8. checks run
9. remaining questions or next setup step
