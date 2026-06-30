# Codex Skills

语言版本：[English](./README.md) | 中文

![二次元风格 Codex skills 工程化工作台](./assets/codex-skills-hero-engineering.png)

这是一组可复用的 Codex skills，用于澄清想法、保留写作声音、做决策、做更可靠的工程取舍，以及为项目建立长期可维护的 Codex 工作上下文。

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

## Skills

完整目录见 [skills/README.md](./skills/README.md)。

### Planning

- **[idea-validator](./skills/idea-validator/SKILL.md)** - 澄清 idea，通过独立研究路线和 skeptic loop 挑战假设，并产出可行性、价值和实现结论。

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
    |-- README.md
    |-- codex-project-settings/
    |-- decision-advisor/
    |-- engineering-decision-review/
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
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/decision-advisor
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/voice-preserving-editor
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/engineering-decision-review
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/codex-project-settings
```

如果默认 Python 环境没有 `PyYAML`，可以创建临时 virtual environment，安装 `PyYAML` 后再运行验证。
