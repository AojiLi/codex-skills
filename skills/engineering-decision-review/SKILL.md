---
name: engineering-decision-review
description: Review non-trivial software engineering decisions with explicit repository coverage before giving advice. Use when the user asks for architecture, refactoring, implementation strategy, module design, technical tradeoff, risk review, or engineering plan recommendations and the answer depends on understanding an existing repository or turning a software idea into an executable engineering path.
---

# Engineering Decision Review

Use this skill to prevent premature engineering advice. The core rule is: no relevant repo coverage, no engineering advice.

## Non-Negotiables

- Do not give architecture, refactoring, risk, or implementation-strategy advice after reading only a few files.
- Do not treat directory names, stale memory, or isolated snippets as system facts.
- Do not make risk claims without reading relevant call sites, tests, configuration, data boundaries, and deployment or runtime constraints.
- If repository coverage is incomplete, label the conclusion `tentative` and state exactly what has not been inspected.
- Subagents provide evidence, not final authority. The main agent must verify critical evidence before recommending.

## Workflow

### 1. Frame The Decision

Clarify the engineering decision before scanning deeply:

- decision or question
- user goal and success criteria
- known constraints
- unacceptable outcomes
- whether the user wants advice only, a plan, or implementation

If the repository is empty or the project intent is unclear, ask clarifying questions before giving engineering advice.

### 2. Build Repo Coverage

Read `references/repo-coverage-gate.md`.

Map the repository before recommending:

- file tree and git status
- README, AGENTS, CONTEXT, docs, and status files when present
- package, build, test, deploy, env, schema, and migration config
- main entry points
- modules directly related to the decision
- callers, callees, tests, and data boundaries for those modules

Before advice, output a compact coverage note with what was read, why it is relevant, what remains unread, and confidence.

### 3. Use Coverage Fan-Out

Use subagents when available for medium or large repositories, cross-module decisions, architecture advice, refactors, migrations, security-sensitive work, or when the main context would crowd out important files.

Recommended lanes:

- `repo_mapper`: repository shape, docs, entry points, build/test/deploy commands
- `domain_scout`: relevant modules, call graph, data flow, ownership boundaries
- `test_scout`: related tests, test gaps, CI and verification commands
- `risk_scout`: schema, migrations, auth, permissions, env, state, deployment, data safety
- `history_scout`: relevant git history, TODOs, old design notes, prior constraints

Each subagent must return files inspected, evidence, uncertainties, unread areas, and impact on the decision. If subagents are unavailable, perform the lanes sequentially and disclose the limitation.

### 4. Build The System Model

Summarize how the relevant system currently works:

- core modules and responsibilities
- important data/control flow
- public APIs, schemas, or contracts
- runtime and deployment assumptions
- tests and validation surface
- fragile areas and unknowns

Ask the user to correct the model when the decision depends on product intent, hidden constraints, or ambiguous ownership.

### 5. Compare Options

Read `references/decision-rubric.md`.

Present two or three realistic options when possible. For each option, state:

- what changes
- why it fits or does not fit the current repo
- blast radius
- reversibility
- testability
- migration or data risk
- maintenance cost
- likely failure mode

Do not present a single option unless the repository evidence clearly rules out alternatives.

### 6. Recommend

Give a clear recommendation tied to evidence from files, tests, docs, or config. Separate:

- source-backed facts
- inferences
- assumptions
- open questions

If coverage is low, recommend the next investigation step instead of a final engineering direction.

### 7. Slice Implementation

Read `references/implementation-slicing.md`.

Turn the recommendation into small, verifiable steps:

- first safe slice
- validation for each slice
- rollback or stop condition
- files likely to change
- tests or checks to run
- decision points before broadening scope

## Output Rules

Use this structure for final advice:

1. Repo coverage note
2. Current system model
3. Options and tradeoffs
4. Recommendation
5. Implementation slices
6. Verification plan
7. Residual risks and unknowns

Keep recommendations direct. Do not bury the chosen path under generic best practices.
