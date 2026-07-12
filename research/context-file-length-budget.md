# Length Budgets for Repository Memory Files

_Research current as of 2026-07-13._

## Recommendation

No reviewed source defines `CONTEXT.md`, `ACTIVE_CONTEXT.md`, or `STATUS.md`, and none prescribes an exact word count for them. The numbers below are therefore a **recommended policy inferred from adjacent first-party guidance and long-context research**, not vendor limits.

| File | Soft budget | Hard budget | Retention objective |
| --- | ---: | ---: | --- |
| `CONTEXT.md` | 1,000 words (about 1,330 tokens) | 1,500 words (about 2,000 tokens) | Durable project map and invariants only |
| `ACTIVE_CONTEXT.md` | 300 words (about 400 tokens) | 500 words (about 670 tokens) | One current direction; overwrite, never accumulate |
| `STATUS.md` | 500 words (about 670 tokens) | 800 words (about 1,070 tokens) | Current human snapshot plus a bounded recent-change window |
| **Combined** | **1,800 words (about 2,400 tokens)** | **2,800 words (about 3,740 tokens)** | Applies when a harness loads all three together |

Treat the soft budget as a warning: prune during the next substantive update. Treat the hard budget as a stop: do not append until stale or detailed material is removed, rewritten, or moved to a linked source-of-truth document. Token estimates use OpenAI's English rule of thumb that one token is about three-quarters of a word; actual tokenization varies by model and content. [OpenAI's token-counting guidance](https://help.openai.com/en/articles/4936856-what-are-tokens-and-how-to-count-them)

## What the sources explicitly support

- Codex concatenates discovered `AGENTS.md` guidance until `project_doc_max_bytes`, 32 KiB by default. That is a loader ceiling for the recognized instruction chain, **not** a recommended size and **not** an automatic limit on these three custom files. [OpenAI Codex documentation](https://learn.chatgpt.com/docs/agent-configuration/agents-md)
- OpenAI reports that one large `AGENTS.md` crowded out task and code context, became stale, and was hard to verify. Its internal project instead uses a roughly 100-line `AGENTS.md` as a map to deeper repository documentation, with progressive disclosure and automated stale-doc cleanup. This is a first-party case study, not a universal threshold. [OpenAI, "Harness engineering"](https://openai.com/index/harness-engineering/)
- Anthropic explicitly recommends targeting fewer than 200 lines per `CLAUDE.md`; it says longer files consume more context and reduce adherence, and notes that splitting content into imports does not save context because imports still load at launch. It also recommends periodically removing outdated or conflicting instructions. [Claude Code memory documentation](https://code.claude.com/docs/en/memory)
- Anthropic's broader principle is to find the smallest set of high-signal tokens that produces the desired behavior. It recommends file-based notes for project state and just-in-time retrieval rather than retaining everything in the live context. [Anthropic, "Effective context engineering for AI agents"](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
- For cross-session coding, Anthropic found that a progress artifact plus Git history helped a fresh agent understand recent work; the source does not specify how long that artifact should be. [Anthropic, "Effective harnesses for long-running agents"](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)
- Long context capacity is not the same as reliable use. The 2024 *Lost in the Middle* experiments found positional degradation and diminishing gains from additional retrieved documents. [Liu et al., TACL 2024](https://aclanthology.org/2024.tacl-1.9/) Newer evidence narrows that conclusion: Google reports strong position-independent simple fact retrieval for Gemini 2.5 Flash, while its current long-context guidance still warns that multi-item retrieval varies widely and recommends omitting unneeded tokens. [Google Research](https://research.google/pubs/retrieval-quality-at-context-limit/), [Gemini long-context documentation](https://ai.google.dev/gemini-api/docs/long-context)

Together, these sources justify a conservative relevance budget and progressive disclosure. They do **not** justify deriving a file limit from a model's maximum context window or claiming a universal performance cliff at a particular token count.

## Why these inferred budgets

`CONTEXT.md` receives the largest allocation because a stable project map may need purpose, architecture boundaries, non-obvious commands, constraints, and invariants. The 1,500-word hard cap is a conservative inferred ceiling that can generally remain under Anthropic's adjacent under-200-line guidance when written as terse Markdown; line density varies, so this is not an exact equivalence. `ACTIVE_CONTEXT.md` is deliberately much smaller because it represents one narrow workstream, not a plan archive. `STATUS.md` gets a middle-sized allocation so a human can scan current state, risks, and a few recent changes without reading project history.

The combined soft cap keeps routine repository memory near 2,400 tokens, leaving the overwhelming majority of the context window for the task, code, tool output, and selectively loaded documentation. The hard caps are governance thresholds, not claims about model capacity. Repositories with measured task-level evaluations may tighten or relax them, but a larger model window alone is not evidence that more always-loaded memory improves outcomes.

## Retention rules

### `CONTEXT.md`

- Keep project purpose, stable terminology, architecture and ownership maps, canonical commands, durable constraints, invariants, and links to authoritative docs.
- Promote a fact only when it is expected to survive multiple tasks or at least one release cycle, or when agents repeatedly need the same non-obvious fact.
- Replace obsolete facts in place; do not retain their chronology here. Put rationale and history in ADRs, design docs, changelogs, or Git.
- Move detailed subsystem explanations, runbooks, schemas, and large command catalogs to scoped documents. Retain a one-sentence summary and link.
- Review after material architecture or tooling changes and at least quarterly. At the soft cap, remove duplication first; at the hard cap, split by source-of-truth domain before adding content.

### `ACTIVE_CONTEXT.md`

- Keep exactly one current goal, success condition, scope boundary, live decisions, blockers, verification state, and next step.
- Rewrite the file when the goal or phase changes. Delete completed steps, resolved blockers, rejected options, and previous directions immediately; Git already preserves the old text.
- Do not use dated append-only entries. Put multi-phase execution detail in a separate active plan and link it.
- When no work is active, reduce the file to an explicit idle state and next intended decision, preferably under 100 words.

### `STATUS.md`

- Put the one-sentence state, last-updated date, current milestone, next step, risks, blockers, and recent material changes at the top-level scan path.
- Keep at most seven recent material changes. Normally keep only the last 30 days, but allow older entries when a slow-moving project needs them to explain the current state. This rolling window is a proposed retention rule, not a source-prescribed number.
- Summarize outcomes, not activity logs. Move older history to Git, release notes, a changelog, or completed plans; link those sources rather than duplicating them.
- Update the current snapshot in place when state changes. Do not append a new paragraph that restates an older snapshot.

## Loading and enforcement

Use `AGENTS.md` as a router: read `CONTEXT.md` for orientation or durable project facts, `ACTIVE_CONTEXT.md` for the current workstream, and `STATUS.md` for progress, handoff, or onboarding questions. Prefer links that an agent can follow just in time over unconditional imports. This follows OpenAI's map-plus-progressive-disclosure pattern and Anthropic's warning that imported instruction files still consume launch context. [OpenAI](https://openai.com/index/harness-engineering/), [Anthropic](https://code.claude.com/docs/en/memory)

For English prose, word counts are a simple audit proxy: warn above soft caps and fail above hard caps, with a reviewed override for generated or unusually terse content. For Chinese and other languages without reliable whitespace-delimited words, enforce an approximate token budget instead; if a tokenizer is unavailable, use a project-calibrated character limit. Line count is only a secondary guard because one line can contain arbitrarily dense text. Separately test representative coding tasks for instruction adherence, retrieval of key facts, stale-fact errors, and startup token cost. Those evaluations, not these baseline numbers, should determine any project-specific exception.
