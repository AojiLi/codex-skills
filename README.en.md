# Codex Skills

Language: English | [中文](./README.zh-CN.md)

![Anime-style Codex skills engineering workspace](./assets/codex-skills-hero-engineering.png)

Reusable Codex skills for thinking clearly, preserving writing voice, making better decisions, reviewing engineering tradeoffs, and setting up repositories so Codex can work with them over time.

This repository is built around one practical problem: AI can produce more code, text, and plans than a human can comfortably audit. When the output surface gets too large, the user's own reasoning gets crowded out. Instead of thinking about the abstract shape of the project, the user is forced into low-level review of too much generated material.

For software where runtime speed, safety, correctness, stability, or security matter deeply, AI-generated code plus AI self-review is not enough. Experienced technical review remains necessary, even when that review is assisted by AI. The review burden becomes a real engineering cost.

For individuals and small teams, that cost can be fatal. In lower-risk projects, it is often better to spend more time on product iteration than on heavyweight human review of every AI-generated detail. In that setting, AI generation and AI-assisted self-review are useful, but only if the work is kept scoped, contextualized, and easy to inspect.

## Core Operating Model

This repo tries to make AI work smaller, more reviewable, and less mentally expensive.

- **Global idea loop**: use repeated clarification and skepticism to decide whether an idea is worth doing before implementation starts.
- **Local project context**: keep durable project understanding in root-level files so Codex does not rediscover the same context every session.
- **Active context management**: keep only the current narrow direction in a live context file, instead of mixing old directions with the current one.
- **Human-readable status**: keep a short status file for the human reviewer, not for the model.
- **Risk-sensitive review**: use stronger human review for high-risk systems; use scoped AI review for lower-risk, fast-iteration work.
- **Optional workflow modules**: add repo-local workflow skills such as builder/checker or reference validation only when the project needs them.

## Local Project Settings

The Codex project setup this repository promotes is:

- `AGENTS.md`: human-written preferences, repository rules, and routing instructions; AI may help fill details, but this file should stay readable to the user.
- `CONTEXT.md`: durable project context, centered on the project's main direction. If the main direction changes, use a branch; if multiple directions must progress at once, use worktrees.
- `ACTIVE_CONTEXT.md`: the current narrow direction inside the broader project direction. Update it constantly and do not preserve old narrow directions there.
- `STATUS.md`: a human-facing change record and project snapshot.
- `.agents/skills/`: optional repo-local workflows for project-specific loops such as builder/checker, reference validation, evaluation, or release.

## Key Review Signals

Use these signals to decide whether AI output is staying manageable:

- output size: can a human review it without losing the main idea?
- context coverage: did the agent inspect the relevant repository surface before advising or editing?
- risk level: does this affect security, data integrity, money, deployment, correctness, or performance?
- review burden: is the human reviewing meaningful decisions or just fighting generated volume?
- iteration speed: is the process helping the product move, or mostly creating review work?
- reversibility: can the change be sliced, tested, and rolled back?

## Quickstart

Install the full repository:

```bash
npx skills@latest add AojiLi/codex-skills
```

Or install only one skill:

```bash
npx skills@latest add AojiLi/codex-skills --skill idea-validator
npx skills@latest add AojiLi/codex-skills --skill decision-advisor
npx skills@latest add AojiLi/codex-skills --skill voice-preserving-editor
npx skills@latest add AojiLi/codex-skills --skill engineering-decision-review
npx skills@latest add AojiLi/codex-skills --skill codex-project-settings
```

## Why These Skills Exist

These skills address repeated failure modes when working with coding agents.

### 1. The Idea Is Not Clear Enough

Agents can implement too early when the underlying idea is still vague. [`idea-validator`](./skills/idea-validator/SKILL.md) forces clarification, independent research lanes, skeptic loops, and a final feasibility judgment before implementation.

### 2. The Decision Needs A Clear Recommendation

Broad decisions can drift into vague pros and cons without a confirmed decision frame, options, weights, jurisdiction, and risk model. [`decision-advisor`](./skills/decision-advisor/SKILL.md) clarifies the decision, runs economics, strategy, psychology, risk management, legal/regulatory, and technical-feasibility lenses, critiques each lens, and returns a clear recommendation with an action plan and review signals.

### 3. The Agent Gives Engineering Advice Too Early

Agents often read a few files and then make architecture or refactoring recommendations without enough repository coverage. [`engineering-decision-review`](./skills/engineering-decision-review/SKILL.md) makes repository coverage explicit, uses subagent fan-out when useful, compares options, and turns the chosen path into small implementation slices.

### 4. Every Project Needs A Stable Codex Setup

Starting each repository from scratch makes Codex relearn where context, current direction, and project status should live. [`codex-project-settings`](./skills/codex-project-settings/SKILL.md) sets up or updates `AGENTS.md`, `CONTEXT.md`, `ACTIVE_CONTEXT.md`, `STATUS.md`, and optional repo-local skills after confirming the project understanding.

### 5. Writing Should Not Become Generic AI Prose

AI editing can over-polish personal writing until it no longer sounds like the author. [`voice-preserving-editor`](./skills/voice-preserving-editor/SKILL.md) improves grammar, clarity, flow, accuracy, and missing connective text while preserving the user's meaning, rhythm, tone, warmth, and personal style.

## Skills

See [skills/README.md](./skills/README.md) for the catalog.

### Planning

- **[idea-validator](./skills/idea-validator/SKILL.md)** - Clarify an idea, research it with independent lanes, challenge assumptions, and produce feasibility, value, and implementation conclusions.

### Decision Support

- **[decision-advisor](./skills/decision-advisor/SKILL.md)** - Analyze decisions through clarified options, weights, jurisdiction, six-lens research, critique loops, and a clear recommendation.

### Writing

- **[voice-preserving-editor](./skills/voice-preserving-editor/SKILL.md)** - Edit prose, Markdown, docs, READMEs, DOCX, or Google Docs while preserving the author's meaning, tone, warmth, and personal style.

### Engineering

- **[engineering-decision-review](./skills/engineering-decision-review/SKILL.md)** - Review non-trivial engineering decisions with explicit repo coverage, subagent fan-out, tradeoff analysis, and implementation slices.

### Project Setup

- **[codex-project-settings](./skills/codex-project-settings/SKILL.md)** - Set up or update a repository with Codex project settings and optional repo-local workflows.

## Framework

- **[Codex Project Settings Framework](./codex_agent_framework.md)** - A reusable repository structure for `AGENTS.md`, context files, optional repo-local workflows, and reference-backed project guidance.

The framework document is the long-form reference. The `codex-project-settings` skill is the executable workflow for applying that framework to a real repository.

## Repository Layout

```text
.
|-- .gitignore
|-- assets/
|-- README.md
|-- README.en.md
|-- README.zh-CN.md
|-- codex_agent_framework.md
`-- skills/
    |-- README.md
    |-- codex-project-settings/
    |-- decision-advisor/
    |-- engineering-decision-review/
    |-- idea-validator/
    `-- voice-preserving-editor/
```

Each skill is self-contained:

```text
skills/<skill-name>/
|-- SKILL.md
|-- agents/
|   `-- openai.yaml
`-- references/
```

## Validate

Validate all public skills:

```bash
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/idea-validator
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/decision-advisor
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/voice-preserving-editor
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/engineering-decision-review
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/codex-project-settings
```

If the default Python environment does not have `PyYAML`, run validation from a temporary virtual environment with `PyYAML` installed.
