# Codex Engineering Skills

语言版本：[English](./README.md) | 中文

![二次元风格 Codex skills 工程化工作台](./assets/codex-skills-hero-engineering.png)

这是一组工程专用的 Codex skills，用于压力测试工程计划、调研一手资料、基于仓库证据审核技术决策，以及建立长期可维护的项目设置。

这个仓库现在只关注工程工作流。通用 idea 验证、决策、文字编辑、前端设计和算法艺术 skills 已移动到 [AojiLi/codex-general-skills](https://github.com/AojiLi/codex-general-skills)。

## 工作模型

- 在实现前先澄清工程问题。
- 在给出技术建议前检查相关仓库证据。
- 当仓库较大或主上下文压力较高时，使用 subagents 做独立覆盖。
- 推荐路径保持小、可逆、可测试，并明确披露未知部分。
- 把稳定项目事实放在权威文档中，只在需要时读取可选上下文。

## Skills

### 规划与压力测试

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

适合开始长期 Codex 项目工作，或者修复已有项目设置。它会检查并分类仓库，说明证据和 blind spots，让你确认它对项目的理解，然后建立最小够用的设置：Codex 原生发现的 `AGENTS.md`、确有需要时才创建的 `CONTEXT.md`，以及项目专用 skills。`CONTEXT.md` 存在时采用明确的读取路由、目标值和硬上限。

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
npx skills@latest add AojiLi/codex-skills --skill grill-me
npx skills@latest add AojiLi/codex-skills --skill research
npx skills@latest add AojiLi/codex-skills --skill engineering-decision-review
npx skills@latest add AojiLi/codex-skills --skill codex-project-settings
```

## Codex Project Settings Framework

可复用项目基线位于 [codex_agent_framework.md](./codex_agent_framework.md)。它采用选择式上下文模型：

- `AGENTS.md`：Codex 原生发现的仓库命令、规则、验证要求和路由。
- `CONTEXT.md`：可选、按需读取的稳定项目事实和约束。
- `.agents/skills/`：可选的项目专用工作流。

## 目录结构

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

## 验证

使用 Codex 自带 validator 检查 skill：

```bash
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/<skill-name>
```
