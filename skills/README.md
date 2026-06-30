# Skills Catalog

This directory contains reusable Codex skills. Skills are kept flat under `skills/<skill-name>/` so install commands can stay simple and stable.

Each public skill should include:

- `SKILL.md`
- `agents/openai.yaml`
- `references/` when the workflow needs detailed rubrics or templates

## Planning

- **[idea-validator](./idea-validator/SKILL.md)** - Clarify a vague idea, run independent research lanes, challenge assumptions, and produce feasibility, value, differentiation, MVP, implementation, and validation conclusions.

## Decision Support

- **[decision-advisor](./decision-advisor/SKILL.md)** - Analyze decisions through a confirmed decision frame, candidate options, jurisdiction, constraints, weight framework, six-lens research, critique loops, recommendation, action plan, and review signals.

## Writing

- **[voice-preserving-editor](./voice-preserving-editor/SKILL.md)** - Edit, polish, correct, complete, or insert prose while preserving the author's meaning, tone, warmth, rhythm, and personal style.

## Engineering

- **[engineering-decision-review](./engineering-decision-review/SKILL.md)** - Prevent premature engineering advice by requiring relevant repository coverage, subagent fan-out when useful, explicit tradeoffs, and small verifiable implementation slices.

## Project Setup

- **[codex-project-settings](./codex-project-settings/SKILL.md)** - Initialize or update a repository with Codex project settings: `AGENTS.md`, `CONTEXT.md`, `ACTIVE_CONTEXT.md`, `STATUS.md`, and optional repo-local workflow or reference skills.
