<a id="english"></a>

# Codex Engineering Skills

Language: English | [中文](#user-content-zh-cn)

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

<a id="zh-cn"></a>

# Codex Engineering Skills

语言版本：[English](#user-content-english) | 中文

![二次元风格 Codex skills 工程化工作台](./assets/codex-skills-hero-engineering.png)

这是一组工程专用的 Codex skills，用于验证软件 idea、压力测试工程计划、调研一手资料、基于仓库证据审核技术决策，以及建立长期可维护的项目设置。

这个仓库现在只关注工程工作流。通用决策、文字编辑、前端设计和算法艺术 skills 已移动到 [AojiLi/codex-general-skills](https://github.com/AojiLi/codex-general-skills)。

## 工作模型

- 在实现前先澄清 idea 或工程问题。
- 在给出技术建议前检查相关仓库证据。
- 当仓库较大或主上下文压力较高时，使用 subagents 做独立覆盖。
- 推荐路径保持小、可逆、可测试，并明确披露未知部分。
- 把稳定项目事实、当前工作方向和给人看的状态分开存放，并限制长度。

## Skills

### 规划与验证

- **[idea-validator](./skills/idea-validator/SKILL.md)** - 澄清软件或产品 idea，通过独立研究和 skeptic loops，输出可行性、价值、差异化、MVP、实现和验证结论。
- **[grill-me](./skills/grill-me/SKILL.md)** - 按决策分支持续追问工程计划或设计，直到假设和取舍被明确。

### 调研与工程审核

- **[research](./skills/research/SKILL.md)** - 把调研交给后台 agent，追溯高可信一手资料，并把带引用的结果保存到仓库。
- **[engineering-decision-review](./skills/engineering-decision-review/SKILL.md)** - 通过显式仓库覆盖、有证据的取舍和小型可验证实现切片来审核非平凡工程决策。

### 项目设置

- **[codex-project-settings](./skills/codex-project-settings/SKILL.md)** - 在明确仓库覆盖后建立或更新 Codex 项目设置、有界项目记忆和可选 repo-local workflows。

## 安装

安装全部工程 skills：

```bash
npx skills@latest add AojiLi/codex-skills
```

安装单个 skill：

```bash
npx skills@latest add AojiLi/codex-skills --skill idea-validator
npx skills@latest add AojiLi/codex-skills --skill grill-me
npx skills@latest add AojiLi/codex-skills --skill research
npx skills@latest add AojiLi/codex-skills --skill engineering-decision-review
npx skills@latest add AojiLi/codex-skills --skill codex-project-settings
```

## Codex Project Settings Framework

可复用项目基线位于 [codex_agent_framework.md](./codex_agent_framework.md)。默认的项目记忆模型是：

- `AGENTS.md`：仓库入口规则和路由。
- `CONTEXT.md`：有界的稳定项目事实和约束。
- `ACTIVE_CONTEXT.md`：只保留一个当前方向，方向变化时整体覆盖。
- `STATUS.md`：有界的、给人看的项目状态快照和最近重要变化。
- `.agents/skills/`：可选的项目专用工作流。

## 目录结构

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

## 验证

使用 Codex 自带 validator 检查 skill：

```bash
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/<skill-name>
```
