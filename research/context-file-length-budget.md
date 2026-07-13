# Length Budget for Optional Repository Context

_Research current as of 2026-07-13._

## Recommendation

No reviewed source defines `CONTEXT.md` or prescribes an exact word count for it. The numbers below are therefore a **recommended policy inferred from adjacent first-party guidance and long-context research**, not vendor limits.

| File | Soft budget | Hard budget | Retention objective |
| --- | ---: | ---: | --- |
| `CONTEXT.md` | 1,000 words (about 1,330 tokens) | 1,500 words (about 2,000 tokens) | Durable project map and invariants only |

Treat the soft budget as a warning: prune during the next substantive update. Treat the hard budget as a stop: do not append until stale or detailed material is removed, rewritten, or moved to a linked source-of-truth document. Token estimates use OpenAI's English rule of thumb that one token is about three-quarters of a word; actual tokenization varies by model and content. [OpenAI's token-counting guidance](https://help.openai.com/en/articles/4936856-what-are-tokens-and-how-to-count-them)

## What the sources explicitly support

- Codex concatenates discovered `AGENTS.md` guidance until `project_doc_max_bytes`, 32 KiB by default. That is a loader ceiling for the recognized instruction chain, **not** a recommended size and **not** an automatic limit on `CONTEXT.md`. [OpenAI Codex documentation](https://learn.chatgpt.com/docs/agent-configuration/agents-md)
- OpenAI reports that one large `AGENTS.md` crowded out task and code context, became stale, and was hard to verify. Its internal project instead uses a roughly 100-line `AGENTS.md` as a map to deeper repository documentation, with progressive disclosure and automated stale-doc cleanup. This is a first-party case study, not a universal threshold. [OpenAI, "Harness engineering"](https://openai.com/index/harness-engineering/)
- Anthropic explicitly recommends targeting fewer than 200 lines per `CLAUDE.md`; it says longer files consume more context and reduce adherence, and notes that splitting content into imports does not save context because imports still load at launch. It also recommends periodically removing outdated or conflicting instructions. [Claude Code memory documentation](https://code.claude.com/docs/en/memory)
- Anthropic's broader principle is to find the smallest set of high-signal tokens that produces the desired behavior and retrieve supporting material just in time instead of retaining everything in live context. [Anthropic, "Effective context engineering for AI agents"](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
- Long context capacity is not the same as reliable use. The 2024 *Lost in the Middle* experiments found positional degradation and diminishing gains from additional retrieved documents. [Liu et al., TACL 2024](https://aclanthology.org/2024.tacl-1.9/) Newer evidence narrows that conclusion: Google reports strong position-independent simple fact retrieval for Gemini 2.5 Flash, while its current long-context guidance still warns that multi-item retrieval varies widely and recommends omitting unneeded tokens. [Google Research](https://research.google/pubs/retrieval-quality-at-context-limit/), [Gemini long-context documentation](https://ai.google.dev/gemini-api/docs/long-context)

Together, these sources justify a conservative relevance budget and progressive disclosure. They do **not** justify deriving a file limit from a model's maximum context window or claiming a universal performance cliff at a particular token count.

## Why this inferred budget

A stable project map may need purpose, architecture boundaries, non-obvious commands, constraints, and invariants. The 1,500-word hard cap is a conservative inferred ceiling that can generally remain under Anthropic's adjacent under-200-line guidance when written as terse Markdown; line density varies, so this is not an exact equivalence. The budget is a governance threshold, not a claim about model capacity. Repositories with measured task-level evaluations may tighten or relax it, but a larger model window alone is not evidence that more context improves outcomes.

## Retention rules

- Keep project purpose, stable terminology, architecture and ownership maps, canonical commands, durable constraints, invariants, and links to authoritative docs.
- Promote a fact only when it is expected to survive multiple tasks or at least one release cycle, or when agents repeatedly need the same non-obvious fact.
- Replace obsolete facts in place; do not retain their chronology here. Put rationale and history in ADRs, design docs, changelogs, or Git.
- Move detailed subsystem explanations, runbooks, schemas, and large command catalogs to scoped documents. Retain a one-sentence summary and link.
- Review after material architecture or tooling changes and at least quarterly. At the soft cap, remove duplication first; at the hard cap, split by source-of-truth domain before adding content.

## Loading and enforcement

Use `AGENTS.md` as a selective router: read `CONTEXT.md` only for durable project facts that are not already clear from authoritative documentation. Keep current work in the current task, plan, issue, or other project source of truth; keep project history and status in Git, issues, changelogs, releases, or the existing project-management system. Prefer links that an agent can follow just in time over unconditional imports. [OpenAI](https://openai.com/index/harness-engineering/), [Anthropic](https://code.claude.com/docs/en/memory)

For English prose, word counts are a simple audit proxy: warn above the soft cap and fail above the hard cap, with a reviewed override for generated or unusually terse content. For Chinese and other languages without reliable whitespace-delimited words, enforce an approximate token budget instead; if a tokenizer is unavailable, use a project-calibrated character limit. Line count is only a secondary guard because one line can contain arbitrarily dense text. Separately test representative coding tasks for instruction adherence, retrieval of key facts, stale-fact errors, and startup token cost. Those evaluations, not this baseline number, should determine any project-specific exception.
