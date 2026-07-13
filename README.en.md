# Codex Engineering Skills

Language: English | [中文](./README.zh-CN.md)

![Anime-style Codex skills engineering workspace](./assets/codex-skills-hero-engineering.png)

Reusable Codex skills for stress-testing engineering plans, researching primary sources, reviewing repository-backed technical decisions, and establishing durable project settings.

This repository is intentionally engineering-focused. General idea-validation, decision, writing, frontend-design, and algorithmic-art skills live in [AojiLi/codex-general-skills](https://github.com/AojiLi/codex-general-skills).

## Operating Model

- Clarify the engineering question before implementation.
- Inspect relevant repository evidence before giving technical advice.
- Use subagents when repository size or context pressure makes independent coverage useful.
- Keep recommendations small, reversible, testable, and explicit about unknowns.
- Keep durable project facts in authoritative docs and load optional context only when needed.

## Skills

### Planning And Stress Testing

#### [grill-me](./skills/grill-me/SKILL.md)

Use it when you already have an engineering plan or design and want its hidden decisions challenged. It walks the decision tree one question at a time, gives a recommended answer with each question, and explores the repository itself when the answer is discoverable from code.

```text
Use $grill-me to stress-test this API migration plan: [describe the plan].
```

### Research And Engineering Review

#### [research](./skills/research/SKILL.md)

Use it when an engineering question depends on current documentation, APIs, specifications, source code, or other primary evidence. It delegates the reading to a background agent, traces important claims to first-party sources, and writes one cited Markdown report into the repository's existing research location.

```text
Use $research to investigate the current WebAuthn passkey APIs and save the findings in this repo.
```

#### [engineering-decision-review](./skills/engineering-decision-review/SKILL.md)

Use it for architecture, refactoring, module design, migrations, technical tradeoffs, risk review, or implementation strategy that depends on an existing repository. It maps the relevant repository surface, reports coverage and blind spots, uses targeted subagent lanes when useful, builds a current-system model, compares realistic options, recommends one path, and divides it into reversible slices with checks and stop conditions.

```text
Use $engineering-decision-review to decide whether this repository should split the billing module into a separate service.
```

### Project Setup

#### [codex-project-settings](./skills/codex-project-settings/SKILL.md)

Use it when starting long-term Codex work in a repository or repairing an existing setup. It inspects and classifies the repository, summarizes the evidence and blind spots, asks you to confirm its project understanding, then creates or safely merges the smallest useful setup: native `AGENTS.md` guidance, optional on-demand `CONTEXT.md`, and repo-local skills the project actually needs. When present, `CONTEXT.md` uses explicit routing and soft and hard size budgets.

```text
Use $codex-project-settings to initialize this repository for long-term Codex work.
```

## Install

Install all engineering skills:

```bash
npx skills@latest add AojiLi/codex-skills
```

Install one skill:

```bash
npx skills@latest add AojiLi/codex-skills --skill grill-me
npx skills@latest add AojiLi/codex-skills --skill research
npx skills@latest add AojiLi/codex-skills --skill engineering-decision-review
npx skills@latest add AojiLi/codex-skills --skill codex-project-settings
```

## Codex Project Settings Framework

The reusable project baseline is documented in [codex_agent_framework.md](./codex_agent_framework.md). Its selective context model is:

- `AGENTS.md`: natively discovered repository commands, rules, verification, and routing.
- `CONTEXT.md`: optional on-demand durable project facts and invariants.
- `.agents/skills/`: optional project-specific workflows.

## Structure

```text
codex-skills/
|-- README.md
|-- README.en.md
|-- README.zh-CN.md
|-- codex_agent_framework.md
`-- skills/
    |-- grill-me/
    |-- research/
    |-- engineering-decision-review/
    `-- codex-project-settings/
```

## Validation

Validate a skill with the bundled Codex validator:

```bash
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/<skill-name>
```
