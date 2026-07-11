<a id="english"></a>

# Codex Skills

Language: English | [中文](#user-content-zh-cn)

![Anime-style Codex skills engineering workspace](./assets/codex-skills-hero-engineering.png)

Reusable Codex skills for thinking clearly, stress-testing plans, designing distinctive frontends, creating algorithmic art, preserving writing voice, making better decisions, reviewing engineering tradeoffs, and setting up repositories so Codex can work with them over time.

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
npx skills@latest add AojiLi/codex-skills --skill grill-me
npx skills@latest add AojiLi/codex-skills --skill frontend-design
npx skills@latest add AojiLi/codex-skills --skill algorithmic-art
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

### 6. Plans Need Pressure Before Execution

Some plans look reasonable until their hidden decision branches are questioned. [`grill-me`](./skills/grill-me/SKILL.md) interrogates a plan or design one question at a time, gives a recommended answer for each question, and explores the codebase instead of asking when the answer is discoverable.

### 7. Frontends Should Not Look Templated

AI-generated interfaces often converge on generic palettes, layout tropes, and copy. [`frontend-design`](./skills/frontend-design/SKILL.md) adds a design-lead workflow for distinctive visual direction, typography, layout, motion, copy, and self-critique before and during UI implementation.

### 8. Generative Art Needs A Real Algorithmic System

Code-based art can become shallow random decoration without a computational idea behind it. [`algorithmic-art`](./skills/algorithmic-art/SKILL.md) creates p5.js generative art from an algorithmic philosophy, seeded randomness, interactive parameters, and reusable viewer templates.

## Skills

See [skills/README.md](./skills/README.md) for the catalog.

### Planning

- **[idea-validator](./skills/idea-validator/SKILL.md)** - Clarify an idea, research it with independent lanes, challenge assumptions, and produce feasibility, value, and implementation conclusions.
- **[grill-me](./skills/grill-me/SKILL.md)** - Stress-test a plan or design through one-question-at-a-time interrogation with recommended answers.

### Frontend

- **[frontend-design](./skills/frontend-design/SKILL.md)** - Create distinctive, intentional frontend designs with subject-specific visual direction, typography, layout, motion, copy, and critique.

### Creative

- **[algorithmic-art](./skills/algorithmic-art/SKILL.md)** - Create seeded p5.js generative art with an algorithmic philosophy, interactive viewer, parameter controls, and reusable templates.

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
    |-- algorithmic-art/
    |-- README.md
    |-- codex-project-settings/
    |-- decision-advisor/
    |-- engineering-decision-review/
    |-- frontend-design/
    |-- grill-me/
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
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/grill-me
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/frontend-design
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/algorithmic-art
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/decision-advisor
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/voice-preserving-editor
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/engineering-decision-review
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/codex-project-settings
```

If the default Python environment does not have `PyYAML`, run validation from a temporary virtual environment with `PyYAML` installed.

---

<a id="zh-cn"></a>

# Codex Skills

语言版本：[English](#user-content-english) | 中文

![二次元风格 Codex skills 工程化工作台](./assets/codex-skills-hero-engineering.png)

这是一组可复用的 Codex skills，用于澄清想法、压力测试计划、设计更有辨识度的前端、创作 algorithmic art、保留写作声音、做决策、做更可靠的工程取舍，以及为项目建立长期可维护的 Codex 工作上下文。

这个仓库围绕一个很实际的问题：AI 可以产出远超人类舒适审核范围的代码、文字和计划。当输出面过大时，人的思考上下文会被挤占。你不再专注于项目的抽象结构，而是被迫进入大量低层级生成内容的审核。

对于运行速度、安全性、正确性、稳定性或安全边界非常重要的软件，AI 生成代码再由 AI 自审是不够可信的。即使审核过程会使用 AI，仍然需要有经验的技术人员做人工审核。审核本身会成为真实且很重的工程成本。

对个人和小团队来说，这种成本可能是致命的。在风险较低的项目里，把更多时间放在产品迭代上，往往比对每一段 AI 生成内容做重型人工审核更合理。在这种场景下，AI 生成和 AI 辅助自审是有必要的，但前提是工作必须被限制范围、带有上下文，并且容易被人检查。

## 核心工作模型

这个仓库试图让 AI 工作更小、更容易审核，也更少占用人的思维负担。

- **全局 idea 循环**：通过反复澄清和质疑，在实现之前判断一个 idea 是否值得做。
- **本地项目上下文**：把稳定的项目理解放在根目录文件里，避免 Codex 每次重新发现同样的上下文。
- **活跃上下文管理**：只把当前小方向放在实时上下文文件里，不把过去的小方向和当前方向混在一起。
- **给人看的状态**：维护一个短的状态文件，给人快速扫读，而不是给模型堆上下文。
- **按风险选择审核强度**：高风险系统需要更强的人工审核；低风险、快速迭代项目可以使用范围受控的 AI 自审。
- **可选工作流模块**：只在项目需要时添加 repo-local workflow skills，例如 builder/checker 或 reference validation。

## 本地项目设置

这个仓库推荐的 Codex 项目设置是：

- `AGENTS.md`：人写的偏好、仓库规则和路由说明；AI 可以帮助补细节，但这个文件必须保持对人可读。
- `CONTEXT.md`：稳定的项目上下文，围绕项目的主方向。主方向变化时开分支；多个方向同时推进时用 worktree。
- `ACTIVE_CONTEXT.md`：主方向下当前正在推进的小方向。需要持续更新，不保留旧小方向。
- `STATUS.md`：给人看的改动记录和项目状态快照。
- `.agents/skills/`：可选的 repo-local workflows，用于 builder/checker、reference validation、evaluation、release 等项目专属循环。

## 关键审核信号

用这些信号判断 AI 输出是否仍然可控：

- 输出体量：人是否能在不丢失主线的情况下审核它？
- 上下文覆盖：agent 在建议或改动前，是否检查了相关仓库范围？
- 风险等级：是否影响安全、数据完整性、资金、部署、正确性或性能？
- 审核负担：人是在审核关键决策，还是在对抗生成内容的体量？
- 迭代速度：这个流程是在推动产品前进，还是主要制造审核工作？
- 可逆性：改动是否可以切片、测试和回滚？

## 快速开始

安装整个仓库：

```bash
npx skills@latest add AojiLi/codex-skills
```

或者只安装某一个 skill：

```bash
npx skills@latest add AojiLi/codex-skills --skill idea-validator
npx skills@latest add AojiLi/codex-skills --skill grill-me
npx skills@latest add AojiLi/codex-skills --skill frontend-design
npx skills@latest add AojiLi/codex-skills --skill algorithmic-art
npx skills@latest add AojiLi/codex-skills --skill decision-advisor
npx skills@latest add AojiLi/codex-skills --skill voice-preserving-editor
npx skills@latest add AojiLi/codex-skills --skill engineering-decision-review
npx skills@latest add AojiLi/codex-skills --skill codex-project-settings
```

## 为什么需要这些 Skills

这些 skills 主要解决使用 coding agents 时反复出现的失败模式。

### 1. Idea 还不够清楚

Agent 很容易在 idea 还很模糊时就开始实现。[`idea-validator`](./skills/idea-validator/SKILL.md) 会先澄清问题，通过独立研究路线和 skeptic loop 挑战假设，最后给出可行性、价值和实现判断。

### 2. 决策问题需要明确推荐

宽泛决策很容易停留在模糊利弊分析。[`decision-advisor`](./skills/decision-advisor/SKILL.md) 会先确认决策背景、目标、选项、地区/司法辖区、约束和权重，再通过经济、战略、心理、风险、法律/监管和技术可行性视角分析，经过 critique loop 后给出清晰推荐、备选方案、行动计划和复盘信号。

### 3. Agent 太早给工程建议

Agent 经常只读几个文件，就开始提出架构或重构建议，仓库覆盖明显不足。[`engineering-decision-review`](./skills/engineering-decision-review/SKILL.md) 会明确仓库覆盖范围，在有用时使用 subagent fan-out，对方案做取舍比较，并把推荐路径切成小的可验证步骤。

### 4. 每个项目都需要稳定的 Codex 设置

如果每个仓库都从零开始，Codex 会不断重新学习上下文应该放在哪里、当前方向是什么、项目状态在哪里。[`codex-project-settings`](./skills/codex-project-settings/SKILL.md) 会在确认项目理解之后，设置或更新 `AGENTS.md`、`CONTEXT.md`、`ACTIVE_CONTEXT.md`、`STATUS.md` 和可选 repo-local skills。

### 5. 写作修改不应该变成通用 AI 腔

AI 很容易把个人表达改成过度平滑、没有作者味道的通用文本。[`voice-preserving-editor`](./skills/voice-preserving-editor/SKILL.md) 会在保留原意、节奏、语气、温度和个人风格的前提下，修改语法、表达、清晰度、流畅度、事实准确性和少量必要衔接内容。

### 6. 计划在执行前需要被追问

有些计划表面合理，但隐藏的决策分支没有被问清楚。[`grill-me`](./skills/grill-me/SKILL.md) 会一次只问一个问题来压力测试 plan/design，同时给出推荐回答；如果答案可以通过看代码库得到，就先看代码库而不是问用户。

### 7. 前端不应该长得像模板

AI 生成的界面很容易收敛到通用配色、通用布局和通用文案。[`frontend-design`](./skills/frontend-design/SKILL.md) 提供一个 design-lead workflow，用于在实现前和实现中建立有辨识度的视觉方向、字体、布局、动效、文案和自我 critique。

### 8. 生成艺术需要真正的算法系统

代码艺术如果没有计算思想，很容易变成浅层随机装饰。[`algorithmic-art`](./skills/algorithmic-art/SKILL.md) 会从 algorithmic philosophy 出发，用 p5.js、seeded randomness、交互参数和 viewer templates 创建可探索的 generative art。

## Skills

完整目录见 [skills/README.md](./skills/README.md)。

### Planning

- **[idea-validator](./skills/idea-validator/SKILL.md)** - 澄清 idea，通过独立研究路线和 skeptic loop 挑战假设，并产出可行性、价值和实现结论。
- **[grill-me](./skills/grill-me/SKILL.md)** - 通过一次一个问题的追问来压力测试 plan/design，并为每个问题给出推荐回答。

### Frontend

- **[frontend-design](./skills/frontend-design/SKILL.md)** - 通过贴合主题的视觉方向、字体、布局、动效、文案和 critique，创建更有辨识度的前端设计。

### Creative

- **[algorithmic-art](./skills/algorithmic-art/SKILL.md)** - 用 algorithmic philosophy、seeded p5.js、交互 viewer、参数控制和模板创建 generative art。

### Decision Support

- **[decision-advisor](./skills/decision-advisor/SKILL.md)** - 通过确认选项、权重、地区/司法辖区、六个分析视角和 critique loop，帮助做出清晰推荐和行动计划。

### Writing

- **[voice-preserving-editor](./skills/voice-preserving-editor/SKILL.md)** - 修改 prose、Markdown、文档、README、DOCX 或 Google Docs，同时保留作者原意、语气、温度和个人风格。

### Engineering

- **[engineering-decision-review](./skills/engineering-decision-review/SKILL.md)** - 通过显式仓库覆盖、subagent fan-out、取舍分析和实现切片来审核非平凡工程决策。

### Project Setup

- **[codex-project-settings](./skills/codex-project-settings/SKILL.md)** - 为仓库设置或更新 Codex project settings 和可选 repo-local workflows。

## Framework

- **[Codex Project Settings Framework](./codex_agent_framework.md)** - 用于 `AGENTS.md`、context 文件、可选 repo-local workflows 和 reference-backed project guidance 的可复用仓库结构。

framework 文档是长版参考。`codex-project-settings` skill 是把这个 framework 应用到真实仓库里的执行流程。

## 仓库结构

```text
.
|-- .gitignore
|-- assets/
|-- README.md
|-- README.en.md
|-- README.zh-CN.md
|-- codex_agent_framework.md
`-- skills/
    |-- algorithmic-art/
    |-- README.md
    |-- codex-project-settings/
    |-- decision-advisor/
    |-- engineering-decision-review/
    |-- frontend-design/
    |-- grill-me/
    |-- idea-validator/
    `-- voice-preserving-editor/
```

每个 skill 都是自包含的：

```text
skills/<skill-name>/
|-- SKILL.md
|-- agents/
|   `-- openai.yaml
`-- references/
```

## 验证

验证所有公开 skills：

```bash
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/idea-validator
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/grill-me
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/frontend-design
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/algorithmic-art
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/decision-advisor
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/voice-preserving-editor
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/engineering-decision-review
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/codex-project-settings
```

如果默认 Python 环境没有 `PyYAML`，可以创建临时 virtual environment，安装 `PyYAML` 后再运行验证。
