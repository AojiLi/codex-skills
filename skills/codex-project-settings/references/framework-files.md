# Framework Files

Use these roles and selection rules when generating Codex project settings.

## Native Versus Framework Files

Among the four core files, only `AGENTS.md` has native Codex project-instruction discovery. Codex also supports `AGENTS.override.md` as a replacement instruction filename. The other core files are optional project conventions:

| File | Native discovery | Create when |
| --- | --- | --- |
| `AGENTS.md` | Yes | The repository needs persistent Codex rules, commands, verification, or routing |
| `CONTEXT.md` | No | Durable facts are not already clear in authoritative docs and will help across tasks |
| `ACTIVE_CONTEXT.md` | No | A multi-session workstream needs a small replaceable snapshot |
| `STATUS.md` | No | A separate human-facing snapshot adds value beyond existing project-management sources |

Do not create all four files by habit. When an optional file is created, add a precise route in `AGENTS.md` describing when to read it. Do not route every task through every file.

## Native AGENTS.md Discovery

Keep Codex's discovery behavior explicit:

- Codex reads global guidance from `CODEX_HOME`, normally `~/.codex`.
- For project guidance, Codex searches from the project root to the session's starting working directory, inclusive. It does not recursively load every descendant `AGENTS.md`.
- At each directory level, Codex loads at most one file in this order: `AGENTS.override.md`, `AGENTS.md`, then configured fallback filenames.
- `AGENTS.override.md` replaces `AGENTS.md` at the same directory level; it is not an additive local appendix.
- `project_doc_fallback_filenames` adds fallback names, not extra instruction files to load alongside `AGENTS.md`.
- Project instruction files have a combined byte limit controlled by `project_doc_max_bytes`, currently 32 KiB by default. Inspect the active configuration and current Codex documentation before changing it. This limit does not make optional context files native instructions.
- Use nested `AGENTS.md` for narrowly scoped subtree rules. Verify with a session whose working directory is inside that subtree when the workflow relies on those rules loading.

Primary references: [OpenAI AGENTS.md documentation](https://learn.chatgpt.com/docs/agent-configuration/agents-md), [OpenAI Codex customization guidance](https://developers.openai.com/codex/concepts/customization#agents-guidance), and the [`openai/codex` discovery implementation](https://github.com/openai/codex/blob/main/codex-rs/core/src/agents_md.rs).

## Context Budgets

These are framework policies for optional on-demand documents, not Codex or vendor limits:

| File | Soft budget | Hard budget |
| --- | ---: | ---: |
| `CONTEXT.md` | 1,000 English words (about 1,330 tokens) | 1,500 words (about 2,000 tokens) |
| `ACTIVE_CONTEXT.md` | 300 English words (about 400 tokens) | 500 words (about 670 tokens) |
| `STATUS.md` | 500 English words (about 670 tokens) | 800 words (about 1,070 tokens) |
| Combined optional context | 1,800 English words (about 2,400 tokens) | 2,800 words (about 3,740 tokens) |

- At the soft budget, prune duplication and stale detail during the next substantive update.
- At the hard budget, stop appending until content is removed, rewritten, or moved to a linked source of truth.
- For languages without reliable whitespace-delimited words, use approximate tokens or a project-calibrated character limit. Keep each file below 200 lines as a secondary guard.
- These files consume model context only when an instruction or task causes Codex to read them. Keep routing selective.

## AGENTS.md

Purpose: natively discovered repository instructions.

Include:

- a one- or two-sentence repository orientation only when it changes how Codex works
- exact setup, build, test, lint, and formatting commands Codex repeatedly needs
- repository-specific implementation and review rules
- safety, approval, and verification boundaries
- routes to optional context, authoritative docs, and repo-local skills
- nested-instruction guidance when different subtrees need different rules

Avoid:

- current task state or project status
- long project history or architecture narratives
- duplicated material already maintained in authoritative docs
- broad principles that do not change Codex behavior
- instructions to read every optional file on every task

Write rules as observable actions. Prefer `Run X after changing Y` over general advice such as `keep quality high`. Include exceptions and approval boundaries when they matter.

## CONTEXT.md

Purpose: optional durable project facts for agents.

Create it only when README files, architecture docs, ADRs, runbooks, schemas, and code do not already provide a concise durable orientation. Prefer linking to those sources over copying them.

Include:

- project purpose and target use case
- short architecture and data-flow summary
- important paths and source-of-truth documents
- external services and integrations
- invariants, constraints, and confirmed durable decisions
- assumptions that still need confirmation

Avoid:

- operational commands already required in `AGENTS.md`
- temporary task state
- detailed chronological status
- speculative plans that are not confirmed
- duplicated README, ADR, runbook, or schema content

Replace obsolete facts in place. Keep no chronology. Move subsystem explanations and decision history to authoritative documents, then retain only a short summary and link.

## ACTIVE_CONTEXT.md

Purpose: optional current working direction.

Create it for multi-session or handoff-heavy work where the active branch or direction cannot be recovered cheaply from the current task, plan, issue, or branch state.

Include:

- last updated date
- current broad direction and narrow focus
- current goal and scope boundaries
- confirmed decisions and unresolved questions
- the single next step

Avoid:

- old directions
- completed steps
- unrelated backlog
- durable facts that belong in authoritative docs or `CONTEXT.md`

Rewrite this file when the goal or phase changes. When no work is active, reduce it to an explicit idle state or remove it if it no longer adds value.

## STATUS.md

Purpose: optional human-facing project snapshot.

Create it only when the project lacks a sufficient issue tracker, changelog, release note, plan, dashboard, or other status source and a repository-local summary will be maintained.

Include:

- last updated date
- one-sentence status
- current main line and next checkpoint
- recent material changes
- current judgment, risks, and blockers

Update the snapshot in place. Keep at most seven recent material changes, normally from the last 30 days. Move older history to Git, release notes, a changelog, or completed plans.

## Git Tracking Policy

- Commit shared repository rules and durable team context so teammates, other computers, and remote Codex environments receive them.
- Put personal cross-repository preferences in `~/.codex/AGENTS.md` instead of a project file.
- Gitignore volatile, private, or machine-local state only when the user intentionally wants it unavailable elsewhere.
- State the consequence whenever a generated project file is ignored.
- Never add secrets to any project context file, tracked or ignored.

## Optional Repo-Local Skills

Create repo-local skills only when useful:

- `<reference-skill>` for project-specific reference collection and validation
- workflow skills for project-specific build, check, release, or eval loops

Do not copy optional skills into every project by default.
