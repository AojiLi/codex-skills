# Codex Engineering Skills

Language: English | [中文](./README.zh-CN.md)

![Anime-style Codex skills engineering workspace](./assets/codex-skills-hero-engineering.png)

Reusable Codex skills for validating software ideas, stress-testing engineering plans, researching primary sources, reviewing repository-backed technical decisions, and establishing durable project settings.

This repository is intentionally engineering-focused. General decision, writing, frontend-design, and algorithmic-art skills live in [AojiLi/codex-general-skills](https://github.com/AojiLi/codex-general-skills).

## Operating Model

- Clarify the idea or engineering question before implementation.
- Inspect relevant repository evidence before giving technical advice.
- Use subagents when repository size or context pressure makes independent coverage useful.
- Keep recommendations small, reversible, testable, and explicit about unknowns.
- Store durable project facts, the current workstream, and human-facing status in separate bounded files.

## Skills

### Planning And Validation

- **[idea-validator](./skills/idea-validator/SKILL.md)** - Clarify a software or product idea, run independent research and skeptic loops, and produce feasibility, value, differentiation, MVP, implementation, and validation conclusions.
- **[grill-me](./skills/grill-me/SKILL.md)** - Interrogate an engineering plan or design one decision branch at a time until the assumptions and tradeoffs are explicit.

### Research And Engineering Review

- **[research](./skills/research/SKILL.md)** - Delegate research to a background agent, trace claims to high-trust primary sources, and save the cited findings in the repository.
- **[engineering-decision-review](./skills/engineering-decision-review/SKILL.md)** - Review non-trivial engineering decisions with explicit repository coverage, evidence-backed tradeoffs, and small verifiable implementation slices.

### Project Setup

- **[codex-project-settings](./skills/codex-project-settings/SKILL.md)** - Set up or update repository-level Codex settings with explicit repository coverage, bounded project memory, and optional repo-local workflows.

## Install

Install all engineering skills:

```bash
npx skills@latest add AojiLi/codex-skills
```

Install one skill:

```bash
npx skills@latest add AojiLi/codex-skills --skill idea-validator
npx skills@latest add AojiLi/codex-skills --skill grill-me
npx skills@latest add AojiLi/codex-skills --skill research
npx skills@latest add AojiLi/codex-skills --skill engineering-decision-review
npx skills@latest add AojiLi/codex-skills --skill codex-project-settings
```

## Codex Project Settings Framework

The reusable project baseline is documented in [codex_agent_framework.md](./codex_agent_framework.md). Its default project memory model is:

- `AGENTS.md`: repository entry rules and routing.
- `CONTEXT.md`: bounded durable project facts and invariants.
- `ACTIVE_CONTEXT.md`: one current direction, overwritten when the direction changes.
- `STATUS.md`: a bounded human-facing project snapshot with recent material changes.
- `.agents/skills/`: optional project-specific workflows.

## Structure

```text
codex-skills/
|-- README.md
|-- README.en.md
|-- README.zh-CN.md
|-- codex_agent_framework.md
`-- skills/
    |-- idea-validator/
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
