# Codex Project Settings Framework

This is a selective Codex settings baseline for repositories. It is not a four-file template to copy everywhere. Its purpose is to define a small native instruction layer, optional on-demand context, and project-specific workflows without loading irrelevant material into every task.

Among the four core files, only `AGENTS.md` has native Codex project-instruction discovery; Codex also supports `AGENTS.override.md` as a replacement instruction filename. `CONTEXT.md`, `ACTIVE_CONTEXT.md`, and `STATUS.md` are optional ordinary Markdown documents. Codex reads them only when the current prompt, `AGENTS.md`, or another loaded workflow explicitly routes to them.

## Intended Use

- Start with a small root `AGENTS.md` when the repository needs persistent Codex guidance.
- Add `CONTEXT.md`, `ACTIVE_CONTEXT.md`, or `STATUS.md` only when each file has a distinct role that existing documentation, Git, issues, plans, or project-management tools do not already fill.
- Keep optional context bounded and route it by task instead of loading all project material every time.
- Put repo-local Codex workflow modules in `.agents/skills/` only when the project needs them.
- Use `<reference-skill>` when project decisions need support from papers, open-source repositories, protocols, APIs, schemas, or other references.
- Treat modules such as `builder-checker` as optional. Do not copy them into projects that do not need them.
- This framework defines how Codex should understand and move the project forward. Project-specific training, deployment, evaluation, and release loops belong in project docs, runbooks, scripts, or source files.

## New Project Setup

1. Inspect the repository and confirm the project understanding with the user.
2. Create or repair root `AGENTS.md` with exact recurring commands, repository rules, verification boundaries, and selective routing.
3. Create `CONTEXT.md` only when durable facts need a concise cross-task source that is not already provided by authoritative docs.
4. Create `ACTIVE_CONTEXT.md` only when a multi-session workstream needs a replaceable current-state snapshot.
5. Create `STATUS.md` only when a separate human-facing status snapshot will be useful and maintained.
6. Decide which files are shared and tracked versus intentionally local and ignored; state the consequences.
7. Apply the optional context budgets below and define how stale content is replaced or pruned.
8. If the project needs systematic research or reference-backed judgment, create `.agents/skills/<reference-skill>/`.
9. If the project needs a strict implementation, checking, evaluation, or release loop, add the relevant repo-local workflow skill.

## Repository Structure

```text
repository/
|-- AGENTS.md
|-- CONTEXT.md                         # optional durable context
|-- ACTIVE_CONTEXT.md                  # optional current workstream
|-- STATUS.md                          # optional human snapshot
`-- .agents/
    `-- skills/
        |-- builder-checker/              # optional
        |   |-- AGENTS.md
        |   |-- SKILL.md
        |   `-- references/
        |       `-- checker-rubric.md
        `-- <reference-skill>/            # optional, for reference-backed projects
            |-- AGENTS.md
            |-- SKILL.md
            |-- agents/
            |   `-- openai.yaml
            |-- evals/
            |   |-- fixtures/
            |   |   `-- <reference-eval-case>.json
            |   `-- rubrics/
            |       `-- <eval-rubric>.md
            `-- references/
                |-- reference-routing.md
                |-- coverage-gaps.md
                |-- review-queue/
                |   `-- <candidate-or-claim>.md
                |-- verification/
                |   |-- <reference-or-topic>.md
                |   `-- scorecards/
                |       `-- <reference-or-topic>.json
                |-- rubrics/
                |   |-- source-verifier.md
                |   |-- evidence-verifier.md
                |   `-- applicability-verifier.md
                |-- decisions/
                |   `-- <decision-topic>.md
                |-- papers/
                |   |-- README.md
                |   |-- digests/
                |   |   `-- <paper-or-topic>.md
                |   `-- conclusions/
                |       `-- <paper-or-topic>.json
                |-- repos/
                |   |-- README.md
                |   |-- digests/
                |   |   `-- <repo-or-topic>.md
                |   `-- evaluations/
                |       `-- <repo-or-topic>.json
                |-- design-notes/
                |   `-- <design-topic>.md
                |-- protocols/
                |   `-- <protocol-name>.md
                |-- apis/
                |   `-- <api-or-service>.md
                `-- schemas/
                    `-- <schema-name>.json
```

## Responsibility Map

```text
AGENTS.md
|-- natively discovered commands and work rules
|-- verification and safety boundaries
|-- optional workflow skill routing
`-- <reference-skill> routing

CONTEXT.md (optional, on demand)
`-- bounded durable project facts, paths, constraints, invariants, and authoritative links

ACTIVE_CONTEXT.md (optional, on demand)
`-- bounded current direction, goal, scope, and next step; overwrite it when the active direction changes

STATUS.md (optional, on demand)
`-- bounded human-readable snapshot: current state, recent material changes, next step, and risks

.agents/skills/<workflow-skill>/
|-- optional project workflow
`-- for example implementation/checking, evaluation, release, or other project-specific loops

.agents/skills/<reference-skill>/
|-- project reference collection, filtering, organization, and usage rules
|-- repository orientation and user confirmation before reference search
|-- multiple Discovery subagents for candidate collection
|-- three Verification subagents scoring candidates and key claims from different angles
|-- reference quality control through rubrics, coverage gaps, human review, and evals
`-- project decision support using papers, open-source repos, protocols, APIs, schemas, and other references
```

## Native Loading Model

- Global personal guidance belongs in `~/.codex/AGENTS.md` or the configured `CODEX_HOME`.
- Project guidance is discovered from the project root to the session's starting working directory, inclusive. Codex does not recursively load every descendant `AGENTS.md`.
- At each directory level, Codex loads at most one file: `AGENTS.override.md`, then `AGENTS.md`, then configured fallback filenames.
- `AGENTS.override.md` replaces `AGENTS.md` at the same level; it is not additive.
- `project_doc_fallback_filenames` supplies fallback names, not additional context files to read alongside `AGENTS.md`.
- The discovered project instruction chain is bounded by `project_doc_max_bytes`, currently 32 KiB by default. Inspect the active configuration before changing it.
- Use nested `AGENTS.md` for narrowly scoped subtree rules and verify from a working directory inside the intended subtree.

Primary references: [OpenAI AGENTS.md documentation](https://learn.chatgpt.com/docs/agent-configuration/agents-md), [OpenAI Codex customization guidance](https://developers.openai.com/codex/concepts/customization#agents-guidance), and the [`openai/codex` discovery implementation](https://github.com/openai/codex/blob/main/codex-rs/core/src/agents_md.rs).

## Optional Context Budgets

These are framework policy for optional on-demand files, not model or vendor limits:

| File | Soft budget | Hard budget |
| --- | ---: | ---: |
| `CONTEXT.md` | 1,000 English words (about 1,330 tokens) | 1,500 words (about 2,000 tokens) |
| `ACTIVE_CONTEXT.md` | 300 English words (about 400 tokens) | 500 words (about 670 tokens) |
| `STATUS.md` | 500 English words (about 670 tokens) | 800 words (about 1,070 tokens) |
| Combined optional context | 1,800 English words (about 2,400 tokens) | 2,800 words (about 3,740 tokens) |

- At the soft budget, prune during the next substantive update.
- At the hard budget, stop appending until stale, duplicated, or detailed material is removed, rewritten, or moved to a linked source of truth.
- For Chinese and other languages without reliable whitespace-delimited words, use approximate tokens or a project-calibrated character count. Keep every file below 200 lines as a secondary guard.
- When present, read `CONTEXT.md` for durable facts, `ACTIVE_CONTEXT.md` for the current workstream, and `STATUS.md` only for progress, handoff, onboarding, or project-state questions.
- Optional context consumes model context only when Codex is routed to read it. Do not route every task through every file.
- Keep no chronology in `CONTEXT.md`, no previous directions in `ACTIVE_CONTEXT.md`, and no more than seven recent material changes in `STATUS.md`.
- During setup or maintenance, measure each file and the combined total, then report the final size against both budgets. For English prose, `wc -w` is an acceptable audit proxy.

## Git Tracking Policy

- Commit shared repository rules and durable team context so they reach teammates, other computers, and remote Codex environments.
- Put personal cross-repository preferences in `~/.codex/AGENTS.md`.
- Gitignore volatile, private, or machine-local state only when that is intentional.
- Explain that ignored files will not travel with the repository.
- Never store secrets in any project context file, tracked or ignored.

## Reference Verification Area

```text
references/
|-- coverage-gaps.md
|-- review-queue/
|   `-- <candidate-or-claim>.md
`-- verification/
    |-- <reference-or-topic>.md
    `-- scorecards/
        `-- <reference-or-topic>.json
```

- `coverage-gaps.md` stores missing references, unresolved questions, and directions that still need verification.
- `review-queue/` stores candidate references, disputed claims, and pending investigation items that are not yet verified.
- `verification/` stores independent verification records, including who checked what, source evidence, conflicts, and conclusions.
- `verification/scorecards/` stores structured scoring from the three verification agents.
- Only verified conclusions may be written to `papers/conclusions/*.json` or `repos/evaluations/*.json`.

## Reference Rubrics

```text
references/rubrics/
|-- source-verifier.md
|-- evidence-verifier.md
`-- applicability-verifier.md
```

- `source-verifier.md` defines scoring for source authenticity, dates, original source, authors or institutions, license, and link stability.
- `evidence-verifier.md` defines scoring for claims, evidence type, support from experiments, code, official docs, or data, and overclaim risk.
- `applicability-verifier.md` defines scoring for project fit, implementation cost, safety boundaries, maintenance cost, and tradeoffs.
- Rubrics should include concrete `0-5` examples to reduce scoring drift across agents.

## Reference Decision Records

```text
references/decisions/
`-- <decision-topic>.md
```

Each decision record captures one concrete choice:

- background and problem
- candidate options
- selected option
- rejected options and reasons
- supporting references and scorecards
- risks and consequences
- conditions that should trigger re-evaluation
- human review status

Accepted decisions should not be directly rewritten. If the judgment changes, create a superseding decision and link the old and new records.

## Reference Evals

```text
evals/
|-- fixtures/
|   `-- <reference-eval-case>.json
`-- rubrics/
    `-- <eval-rubric>.md
```

- `fixtures/` stores known cases that test whether `<reference-skill>` can detect fake sources, stale information, license risk, exaggerated claims, or inapplicable references.
- `rubrics/` stores eval scoring criteria.
- When a class of reference mistakes repeats, add an eval case instead of only adding more prose to `SKILL.md`.

## Reference Scorecard

```text
<reference-or-topic>.json
|-- schema_version
|-- topic
|-- candidate_id
|-- checked_on
|-- status
|-- scores
|   |-- source_verifier
|   |   |-- score
|   |   |-- reasons[]
|   |   `-- blockers[]
|   |-- evidence_verifier
|   |   |-- score
|   |   |-- reasons[]
|   |   `-- blockers[]
|   `-- applicability_verifier
|       |-- score
|       |-- reasons[]
|       `-- blockers[]
|-- conflicts[]
|-- required_followups[]
|-- lifecycle
|   |-- last_checked
|   |-- expires_on
|   |-- refresh_reason
|   `-- superseded_by
|-- human_review
|   |-- required
|   |-- accepted_by
|   |-- accepted_on
|   `-- notes
`-- final_decision
    |-- decision
    |-- rationale
    `-- allowed_use
```

- `source_verifier` checks source authenticity, date, author or institution, original link, license, and whether the source is primary.
- `evidence_verifier` checks whether the claim is actually supported by a paper, code, experiment, official docs, or data.
- `applicability_verifier` checks whether the reference fits current project constraints, risks, safety boundaries, and implementation cost.
- Scores use `0-5`: `0` is unusable, `3` is barely usable as a lead, `4` can be cited cautiously, and `5` is high confidence.
- Do not rely on averages. Stable conclusions require `source_verifier >= 4`, `evidence_verifier >= 4`, `applicability_verifier >= 3`, and no blockers.
- High-risk project conclusions require all three scores to be `>= 4` and no unresolved conflicts.
- High-risk references require human review. Without human review, `allowed_use` must be at most `provisional`.
- Expired references must be revalidated. When new evidence overturns a reference, use `superseded_by` to point to the new scorecard or decision.

## Paper References

```text
references/papers/
|-- README.md
|-- digests/
|   `-- <paper-or-topic>.md
`-- conclusions/
    `-- <paper-or-topic>.json
```

## Open-Source Repository References

```text
references/repos/
|-- README.md
|-- digests/
|   `-- <repo-or-topic>.md
`-- evaluations/
    `-- <repo-or-topic>.json
```

## Paper Conclusion JSON

```text
<paper-or-topic>.json
|-- schema_version
|-- topic
|-- updated
`-- papers[]
    |-- id
    |-- metadata
    |   |-- title
    |   |-- authors[]
    |   |-- year
    |   |-- venue
    |   `-- links
    |       |-- paper
    |       |-- doi
    |       `-- arxiv
    |-- summary
    |   |-- one_sentence
    |   |-- problem
    |   |-- method
    |   |-- result
    |   |-- why_it_matters
    |   |-- applicability
    |   `-- limitations
    |-- claims[]
    |   |-- id
    |   |-- claim
    |   |-- evidence_type
    |   |-- evidence
    |   |-- source_location
    |   |-- conditions
    |   |-- limitations
    |   `-- confidence
    |-- verification
    |   |-- status
    |   |-- verified_by[]
    |   |-- checked_on
    |   |-- source_checks[]
    |   |-- scorecard
    |   |   |-- path
    |   |   |-- source_score
    |   |   |-- evidence_score
    |   |   `-- applicability_score
    |   |-- conflicts[]
    |   `-- unresolved_questions[]
    |-- lifecycle
    |   |-- last_checked
    |   |-- expires_on
    |   |-- refresh_reason
    |   `-- superseded_by
    |-- human_review
    |   |-- required
    |   |-- accepted_by
    |   |-- accepted_on
    |   `-- notes
    |-- decision_links[]
    |-- project_use
    |   |-- relevance
    |   |-- status
    |   |-- decision
    |   |-- related_files[]
    |   `-- next_action
    `-- review
        |-- read_by
        |-- reviewed_on
        `-- notes
```

## CONTEXT.md

Optional. Create only when durable project facts are not already clear in authoritative docs and will help across tasks. Target: 1,000 English words. Hard limit: 1,500 words. Replace stale facts in place and link to detailed source-of-truth documents.

```md
# Project Context

Last updated: YYYY-MM-DD

## Purpose

The stable project purpose and the problem it solves.

## Target Users Or Use Case

Who the project serves and the durable use case.

## System Shape

- Stack:
- Runtime:
- Data flow:

## Architecture And Important Paths

- Architecture summary:
- Important paths:
- Authoritative docs:

## External Services And Integrations

- Service or integration:

## Invariants And Constraints

- Invariant:
- Constraint:

## Known Decisions

- Decision:

## Assumptions To Confirm

- Assumption:
```

## ACTIVE_CONTEXT.md

Optional. Create only for a multi-session workstream that needs a replaceable current-state snapshot. Target: 300 English words. Hard limit: 500 words. Rewrite the file when the active goal or phase changes; keep no completed or abandoned directions.

```md
# Active Context

Last updated: YYYY-MM-DD

## Current Broad Direction

The broad direction the project currently belongs to.

## Current Narrow Focus

The specific focus being worked on now.

## Current Goal

What this round of work should accomplish.

## Scope Boundaries

- In scope:
- Out of scope:

## Current Judgment

- Confirmed:
- Still uncertain:

## Next Step

The single most useful next step.
```

## STATUS.md

Optional. Create only when a separate human-facing repository snapshot adds value beyond issues, Git, changelogs, plans, or project-management tools. Target: 500 English words. Hard limit: 800 words. Update the current snapshot in place and keep at most seven recent material changes, normally from the last 30 days.

```md
# Project Status

Last updated: YYYY-MM-DD

## One-Line Status

One sentence explaining where the project currently stands.

## Current Main Line

- Broad direction:
- Current focus:
- Next step:

## Recent Material Changes

- YYYY-MM-DD: What changed; why it changed; result or evidence.

## Current Thinking

- Core judgment:
- Main tradeoff:
- Not doing:

## Risks

- Risk:
- Blocker:
```

## Root AGENTS.md

```md
# Agent Instructions

This file contains natively discovered repository-level instructions. Keep exact recurring commands, implementation rules, verification requirements, and selective routing here. Optional project context lives in separate files only when those files exist and add value.

## Repository Commands

- Setup: `<command>`
- Run: `<command>`
- Test: `<command>`
- Lint or format: `<command>`

## Always-On Work Rules

- Keep technical identifiers, file paths, commands, API names, topics, and schema names accurate.
- Prefer current code, config, logs, and authoritative project docs over remembered context.
- Keep edits small and focused, preserve local style, and avoid unrelated refactors.
- Do not call anything latest/current unless its date or source has been checked.
- Do not overwrite uncommitted changes from the user or another agent.

## Optional Context Routing

- If `CONTEXT.md` exists, read it only for project-wide purpose, architecture, invariants, constraints, or durable decisions not already clear from authoritative docs.
- If `ACTIVE_CONTEXT.md` exists, read it only when continuing or handing off the current multi-session workstream. Overwrite it when that direction changes; do not retain old directions.
- If `STATUS.md` exists, read it only for progress, handoff, onboarding, or project-state requests. Update its snapshot only after a material state change.
- Keep each optional file within the framework's soft and hard budgets; at a hard limit, compact before appending.
- Do not create a missing optional context file unless the project needs that role.

## Scoped Guidance

- Put subsystem-specific rules in a nested `AGENTS.md` only when they should apply to sessions started inside that subtree.
- Do not expect Codex to recursively load descendant `AGENTS.md` files from a repository-root session.

## Optional Workflow Skill Routing

- If the project enables `builder-checker`, load `.agents/skills/builder-checker/AGENTS.md` for non-trivial code changes.
- Builder owns the smallest viable implementation and relevant checks.
- Checker independently reviews the diff, evidence, and validation result.
- Detailed workflow lives in `.agents/skills/builder-checker/SKILL.md`.
- Checker criteria live in `.agents/skills/builder-checker/references/checker-rubric.md`.
- If the project does not enable this workflow skill, delete this section or replace it with the project's own workflow routing.

## <reference-skill> Routing

- When the project needs references collected, organized, or used, load `.agents/skills/<reference-skill>/AGENTS.md`.
- Typical references include papers, open-source repositories, design notes, protocols, APIs, and schemas.
- Before starting a new round of reference collection, analyze the current repository and classify it as empty, existing, or unclear.
- If the repository is empty or unclear, ask the user what the project should be. Send the project understanding back to the user for confirmation before looking for references.
- If the repository already exists, summarize current purpose, stack, known constraints, and inferred direction. Ask the user whether the thinking is correct or needs changes. Start reference search only after confirmation.
- New references must be collected by multiple Discovery subagents, then scored independently by three Verification subagents from different angles.
- Unverified or conflicting material may only enter `references/review-queue/`; it must not enter stable conclusion JSON.
- Key reference gaps go into `references/coverage-gaps.md`.
- Verified references that affect project direction should enter `references/decisions/` as traceable decisions.
- High-risk references must not be marked accepted without human review.
- If a task requires both code changes and reference-backed guidance, and the project enables `builder-checker`, load both `builder-checker` and `<reference-skill>`.
- Project-specific training, deployment, evaluation, release, and other runtime loops do not belong in this framework. Put them in authoritative runbooks, docs, scripts, or source files, then route to them when needed.
```

## .agents/skills/builder-checker/AGENTS.md (Optional Example)

```md
# Builder Checker Governance

This skill owns the general implementation and review workflow. It does not store project facts and does not organize references. Durable facts come from authoritative project docs and, when present, `CONTEXT.md`; reference-backed judgment is provided by `<reference-skill>`.

## Load Order

1. Read root `AGENTS.md` if it has not already been loaded.
2. Read this file.
3. Read `.agents/skills/builder-checker/SKILL.md`.
4. When Checker needs detailed criteria, read `references/checker-rubric.md`.
5. If the task needs reference-backed judgment, also read `.agents/skills/<reference-skill>/AGENTS.md`; if `CONTEXT.md` exists and the task needs durable project facts not clear elsewhere, read it selectively.

## Governance

- Builder and Checker are roles, not fixed identities.
- Builder may edit files; Checker is read-only by default unless the user explicitly asks for fixes.
- For non-trivial, cross-module, deployment, security, or destructive-data changes, prefer an independent Checker subagent.
- If no independent subagent is available, still perform a separate read-only Checker pass.
- Checker does not depend on Builder's private reasoning. Checker uses only the user goal, diff, touched files, and validation output.
- Final responses should state Builder changes, Checker results, validation results, and residual risk.
```

## .agents/skills/builder-checker/SKILL.md (Optional Example)

```md
---
name: builder-checker
description: General Builder / Checker code workflow. Use for non-trivial code changes, code review, risk checks, validation loops, and tasks that need an independent Checker pass.
---

# Builder Checker

## Builder Pass

1. Clarify the user goal.
2. Define the write scope.
3. Read current source and necessary context.
4. Make the smallest coherent and explainable change.
5. Run relevant checks, or record why they cannot run.
6. Provide a Checker handoff:
   - user goal
   - changed files
   - diff summary
   - checks run
   - skipped checks
   - known risks

## Checker Pass

1. Read the user goal, diff, changed files, and validation output.
2. Read `references/checker-rubric.md`.
3. Independently review requirement fit, correctness, integration, safety, tests, evidence, and maintainability.
4. Order findings by severity.
5. Each finding includes file/line, impact, evidence, and suggested fix.
6. If no issues are found, say so clearly and list residual risk.

## Integration Pass

1. Accept or reject Checker findings.
2. Apply the smallest follow-up fix for accepted findings.
3. Rerun relevant checks.
4. Final response states:
   - what Builder changed
   - whether Checker found issues
   - which checks passed
   - which checks were not run and why
```

## .agents/skills/builder-checker/references/checker-rubric.md (Optional Example)

```md
# Checker Rubric

## 1. Requirement Fit

- Does the diff satisfy the user's real request?
- Did it solve the core problem instead of a nearby problem?
- Did it change anything outside scope?

## 2. Correctness

- Are there logic errors, edge cases, state bugs, race conditions, or wrong assumptions?
- Are inputs, outputs, types, schemas, and API contracts still consistent?
- Are error paths and empty states reasonable?

## 3. Integration

- Does it fit the existing architecture and local style?
- Are related call sites, tests, docs, and configs updated where needed?
- Does it preserve public APIs and backward compatibility unless explicitly requested otherwise?

## 4. Safety And Impact

- Could this affect deployment, data integrity, permissions, secrets, hardware, money, or user-visible behavior?
- Are dangerous operations guarded?
- Are failures explicit instead of silent?

## 5. Tests And Verification

- Were the most relevant checks run?
- Do checks cover the changed behavior?
- Is the reason for skipped checks acceptable?
- Is there a smaller, more direct, or higher-level check that should run?

## 6. Evidence Quality

- Are conclusions backed by source, diff, logs, tests, or docs?
- Were latest/current/safe/works claims verified from real sources?
- Are newly introduced issues separated from pre-existing issues?

## 7. Maintainability

- Is the solution simple enough?
- Did it introduce unnecessary abstraction, duplication, hidden coupling, or stale comments?
- Will a future maintainer understand the change?

## Output Format

- Findings first, ordered by severity.
- Each finding includes file/line, impact, evidence, and suggested fix.
- Then list missing tests or residual risk.
- If no issues are found, explicitly write: no blocking issues found.
```

## .agents/skills/<reference-skill>/AGENTS.md

```md
# <Reference Skill> Governance

This skill owns project reference collection, filtering, organization, indexing, and usage rules. It does not define the project's training, deployment, evaluation, or release loops. Project facts come from authoritative docs and optional context files; project-specific processes live in runbooks, docs, scripts, or source files.

## Load Order

1. Read root `AGENTS.md` if it has not already been loaded.
2. Read this file.
3. Read `.agents/skills/<reference-skill>/SKILL.md`.
4. Before new reference collection, project direction judgment, or reference system initialization, run Repository Orientation.
5. If `CONTEXT.md` exists, read it only when durable project background is needed and not already clear from authoritative docs.
6. If `ACTIVE_CONTEXT.md` exists, read it only when the current multi-session workstream matters.
7. If `STATUS.md` exists, read it only when the user asks about progress, handoff, onboarding, or stage status.
8. When unsure which references to search, read `references/reference-routing.md`.
9. If the task involves code changes and the project enables `builder-checker`, also read `.agents/skills/builder-checker/AGENTS.md`.
10. Read only the references, code, config, logs, or docs needed for the current task.

## Repository Orientation

Before Discovery or Verification, classify the repository:

1. Inspect the file tree and git status.
2. Prefer `README*`, `AGENTS.md`, `CONTEXT.md`, `ACTIVE_CONTEXT.md`, `STATUS.md`, package/config files, main entry points, and docs.
3. Classify the repository as:
   - `empty`: not enough files to explain what the project is.
   - `existing`: code, docs, or config explain the project purpose.
   - `unclear`: files exist, but the project direction cannot be judged reliably.
4. Do not determine the project goal from directory name, old conversation, or guesses alone.

Confirmation rules:

- `empty` or `unclear`: first ask the user what to build, who the target user is, what success means, and what constraints matter. Summarize the project understanding and wait for confirmation or correction.
- `existing`: summarize the current purpose, stack, key constraints, known direction, and unknowns. Ask whether the understanding is correct and whether direction or constraints should change.
- Before user confirmation, do not start external reference search, write stable conclusions, or write decisions.
- After user confirmation, update the project's existing source of truth. Create or update `CONTEXT.md`, `ACTIVE_CONTEXT.md`, or `STATUS.md` only when the framework's selection criteria justify that file.

## Governance

- Root `AGENTS.md` contains natively discovered commands, repository rules, verification boundaries, and selective routing.
- `SKILL.md` contains only reference collection, filtering, organization, reuse, and citation rules.
- When present, `CONTEXT.md` stores durable project facts, paths, architecture, constraints, invariants, and authoritative links; replace stale facts in place and keep no chronology.
- When present, `ACTIVE_CONTEXT.md` stores the current active direction, goal, scope, and next step; it keeps only current state, not history.
- When present, `STATUS.md` stores the bounded human-readable project snapshot: one-line status, up to seven recent material changes, current thinking, next step, and risk.
- `references/` stores project-specific long-form references, including papers, open-source repos, design notes, protocols, APIs, and schemas.
- `references/coverage-gaps.md` stores missing evidence and questions that need more verification.
- `references/rubrics/` stores scoring standards and calibration examples for the three verifier roles.
- `references/decisions/` stores project decision records backed by references.
- `evals/` stores regression test cases and scoring criteria for this reference skill.
- Write newly discovered durable project facts to the existing authoritative source; use `CONTEXT.md` only when it is the selected source for that role.
- When `ACTIVE_CONTEXT.md` exists and the current direction changes, overwrite it.
- When `STATUS.md` exists and the project main line, key thinking, next step, or risks change materially, update it in place and prune changes beyond the rolling window.
- Apply the framework optional context budgets only to files that exist; at a hard limit, compact before appending.
- Update this skill only when reference collection, filtering, organization, or reference routing rules change.
- Project-specific runtime loops do not belong in this skill; put them in runbooks, docs, test scripts, or source files as needed.
- Reference collection must be based on confirmed project understanding. Before confirmation, only repository reading and clarification dialogue are allowed.
- Discovery subagents collect candidates. Three Verification subagents independently score source quality, evidence quality, and project applicability; they must not be the same source of conclusions as Discovery.
- Unverified, source-unclear, date-unclear, unreproducible, or conflicting references may only enter `references/review-queue/`.
- References that affect project direction, safety, dependency choice, architecture, or long-term maintenance cost require human review before becoming accepted decisions.
```

## .agents/skills/<reference-skill>/SKILL.md

```md
---
name: <reference-skill>
description: This project's reference skill. Use it to collect, filter, organize, and reuse papers, open-source repositories, design notes, protocols, APIs, schemas, and other references, and to use those references for project design and implementation judgment.
---

# <Reference Skill>

## Request Modes

| Mode | Typical request | Behavior |
| --- | --- | --- |
| Orient | First use of the reference skill, find references for this repo, establish the project reference system | Analyze repository state, classify it as empty/existing/unclear, and confirm project understanding with the user before reference search |
| Discover | Find papers, open-source projects, or existing approaches | Search multiple sources and record candidate references, links, applicability, and risks |
| Digest | Summarize this paper or repo | Compress raw material into a reusable digest while preserving key evidence and limitations |
| Verify | Verify candidate references and key claims | Use three independent subagents to score source quality, evidence quality, and project applicability |
| Conclude | Extract what can and cannot be used | Write only verified stable conclusions to JSON, including evidence, conditions, confidence, and project use |
| Decide | Form a project decision | Convert verified references that affect direction into decision records with tradeoffs, consequences, and re-evaluation conditions |
| Advise | Use references to guide the next step | Read relevant references and provide design advice, implementation paths, tradeoffs, and risks |
| Refresh | Update references | Recheck sources, dates, links, and conclusions for staleness |
| Eval | Test the reference skill | Use fixtures and rubrics to check whether the skill catches wrong references, stale information, and inapplicable conclusions |

## Workflow

1. Repository Orientation: read context in load order, then inspect the file tree, README, project config, entry points, docs, and existing references. Classify the repo as `empty`, `existing`, or `unclear`.
2. Human Understanding Gate:
   - `empty` or `unclear`: clarify what the project should be, target users, success criteria, constraints, and unknowns. Summarize the project understanding and wait for confirmation.
   - `existing`: summarize current purpose, stack, key constraints, known direction, and unknowns. Ask whether the understanding is correct and whether direction or constraints should change.
3. Confirmation pass: after user confirmation, update the existing project source of truth. Create or update optional context files only when their selection criteria are met. Before confirmation, do not start reference search.
4. Scope pass: define the specific question, design direction, or decision that needs reference support; read `references/reference-routing.md` and `references/coverage-gaps.md` when needed.
5. Discovery pass: assign multiple subagents to search papers, open-source repositories, protocols, APIs, schemas, and negative evidence from different sources or angles.
6. Candidate pass: write candidate references, key claims, source links, dates, and initial applicability to `references/review-queue/`.
7. Verification pass: assign three independent subagents to score the candidates; verifiers must not merely repeat Discovery conclusions.
8. Skeptic pass: check selection bias, stale sources, unreproducible results, license risk, project-constraint conflicts, and exaggerated claims.
9. Scorecard pass: write the three-way scoring to `references/verification/scorecards/*.json`.
10. Human review gate: high-risk references or references affecting long-term direction need human review; without review, mark them at most `provisional`.
11. Synthesis pass: only conclusions that pass scoring thresholds and required human review can be written to digests and structured JSON. Conflicting items remain in `review-queue/`.
12. Decision pass: for conclusions affecting project direction, write `references/decisions/*.md` with background, tradeoffs, consequences, and re-evaluation conditions.
13. Eval pass: if the work reveals a new reference risk, add a fixture or rubric under `evals/`.
14. Use references to advise the project: what to borrow, how to borrow it, what limits apply, and what should be verified next.

## Multi-Agent Verification Rules

- Split Discovery into at least two directions; for high-risk projects, prefer paper, repo, official docs/protocol, and negative evidence lanes.
- Verification always uses three independent subagents.
- `source_verifier` checks source authenticity, dates, original source, author or institution, license, and link stability.
- `evidence_verifier` checks whether key claims are supported by original evidence and whether there is exaggeration or secondhand retelling.
- `applicability_verifier` checks whether the reference fits current project constraints, implementation conditions, safety boundaries, and maintenance cost.
- Key claims need original source, location, applicable conditions, limitations, verifier, and check date.
- If the original source cannot be found, the material is only secondhand, the link is dead, the date is unclear, the license is unclear, or results cannot be reproduced, mark it `unverified`.
- When sources conflict, mark the item `disputed`; do not write it as a stable project conclusion.
- Normal conclusion threshold: source score `>= 4`, evidence score `>= 4`, applicability score `>= 3`, and no blocker.
- High-risk conclusion threshold: all three scores `>= 4` and no unresolved conflicts.
- Do not let an average score hide failure in a critical dimension. When source or evidence is below threshold, use the item only as an investigation lead.
- If reference error could affect design or implementation safety, prefer no conclusion over using unverified material to guide code.
- High-risk conclusions require human review; without human review, `allowed_use` can only be `candidate` or `provisional`.
- Each verifier should score against examples in `references/rubrics/`. If the rubric does not cover a new risk, first record a coverage gap.
- References that change over time must have `expires_on` or a clear refresh condition.

## Decision Record Rules

- Write a decision record only when a reference affects project direction, architecture, dependency choice, safety boundaries, or long-term maintenance cost.
- Keep decision records short: conclusion first, then background, tradeoffs, evidence, and consequences.
- Do not directly rewrite accepted decisions; if judgment changes, create a superseding decision.
- Decision records must link supporting conclusions, evaluations, and scorecards.
- Record missing evidence in `references/coverage-gaps.md`; do not fill a decision with guesses.

## Eval Rules

- When an agent incorrectly accepts a reference, or human review finds scoring drift, add an eval fixture.
- An eval fixture should include input question, candidate reference, expected status, risks that must be detected, and scoring criteria.
- Evals do not replace human review; they prevent repeated failures of the same class.

## Reference Use

- Project facts and invariants come from authoritative project docs and, when present, `CONTEXT.md`.
- The current active direction comes from the current task or plan and, when present, `ACTIVE_CONTEXT.md`.
- Project status comes from the project's status source and, when present, `STATUS.md`.
- Reference routing comes from `references/reference-routing.md`.
- Missing evidence and investigation directions come from `references/coverage-gaps.md`.
- Verifier scoring standards come from `references/rubrics/*.md`.
- Paper conclusions come from `references/papers/conclusions/*.json`.
- Open-source repo evaluations come from `references/repos/evaluations/*.json`.
- Unverified material comes from `references/review-queue/`; use it only as investigation leads, not project conclusions.
- Verification records come from `references/verification/`.
- Three-way scores come from `references/verification/scorecards/*.json`.
- Project decisions come from `references/decisions/*.md`.
- Regression cases for this skill come from `evals/`.
- Code changes use the workflow skill enabled by the project. If the project enables `builder-checker`, it owns the code implementation/checking workflow. This skill only provides reference-backed guidance.
- Project-specific training, deployment, evaluation, and release loops do not belong in this skill; the project defines those itself.
```
