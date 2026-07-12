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

#### [idea-validator](./skills/idea-validator/SKILL.md)

Use it before implementation when a software idea, product concept, research direction, or architecture thought is still incomplete. It clarifies the problem, user, solution, timing, success criteria, constraints, and unknowns one question at a time. After you confirm the brief, it asks whether to use five independent research subagents or run the same lanes sequentially, synthesizes the evidence, automatically runs up to five skeptic rounds, and returns feasibility, value, differentiation, MVP, implementation, validation, risk, and next-step conclusions.

```text
Use $idea-validator to evaluate this idea before I build it: [describe the idea].
```

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

Use it when starting long-term Codex work in a repository or repairing an existing setup. It inspects and classifies the repository, summarizes the evidence and blind spots, asks you to confirm its project understanding, then creates or safely merges `AGENTS.md`, `CONTEXT.md`, `ACTIVE_CONTEXT.md`, `STATUS.md`, and only the repo-local skills the project actually needs. The project-memory files use explicit soft and hard size budgets.

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

#### [idea-validator](./skills/idea-validator/SKILL.md)

适合在实现之前分析仍不完整的软件 idea、产品概念、研究方向或架构想法。它会一次问一个问题，澄清问题、用户、方案、时机、成功标准、约束和未知项。你确认 brief 后，它会询问使用五个独立 research subagents，还是在主 agent 中顺序执行相同研究路线；随后由主 agent 汇总证据，自动运行最多五轮 skeptic loop，最后给出可行性、价值、差异化、MVP、实现、验证、风险和下一步结论。

```text
使用 $idea-validator 在我开始实现前分析这个 idea：[描述 idea]。
```

#### [grill-me](./skills/grill-me/SKILL.md)

适合已经有工程计划或设计，但希望把隐藏决策和假设问清楚的场景。它会沿着决策树一次问一个问题，每个问题都会附带推荐回答；如果答案可以从代码得到，它会先检查仓库而不是反问用户。

```text
使用 $grill-me 压力测试这个 API 迁移计划：[描述计划]。
```

### 调研与工程审核

#### [research](./skills/research/SKILL.md)

适合需要核对当前文档、API、规范、源码或其他一手证据的工程问题。它会把阅读工作交给后台 agent，把重要结论追溯到官方文档、源码、spec 或 first-party API，并在仓库原有的调研位置保存一份带引用的 Markdown 报告。

```text
使用 $research 调研当前 WebAuthn passkey API，并把结果保存到这个仓库。
```

#### [engineering-decision-review](./skills/engineering-decision-review/SKILL.md)

适合依赖现有仓库的架构、重构、模块设计、迁移、技术取舍、风险审核或实现策略问题。它会检查相关仓库范围，披露已读内容和 blind spots，在有必要时使用定向 subagent lanes，建立当前系统模型，比较真实可行的选项，推荐一条路径，并把它拆成带验证和停止条件的可逆步骤。

```text
使用 $engineering-decision-review 判断这个仓库是否应该把 billing 模块拆成独立服务。
```

### 项目设置

#### [codex-project-settings](./skills/codex-project-settings/SKILL.md)

适合开始长期 Codex 项目工作，或者修复已有项目设置。它会检查并分类仓库，说明证据和 blind spots，让你确认它对项目的理解，然后创建或安全合并 `AGENTS.md`、`CONTEXT.md`、`ACTIVE_CONTEXT.md`、`STATUS.md`，并且只添加项目真正需要的 repo-local skills。三个项目记忆文件都有明确的目标值和硬上限。

```text
使用 $codex-project-settings 为这个仓库建立长期 Codex 项目设置。
```

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
