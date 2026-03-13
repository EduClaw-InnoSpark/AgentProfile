# AgentProfile

> **一句话创建 Agent。**
>
> 一个用于定义 AI Agent 配置的开源规范。用一句话描述你的需求，Agent 构造器将自动生成完整、结构化的 AgentProfile。

[English](./README.md)

## 什么是 AgentProfile？

AgentProfile 是一个基于 JSON 的开放标准，用于描述 AI Agent。它提供了一个统一的格式来定义 Agent 的身份、能力、行为规范和工具集 —— 所有这些都可以从一句自然语言指令自动生成。

```
"一个处理 SaaS 产品客户支持的 Agent" → AgentProfile → 可直接使用的 Agent
```

## 工作流程

```
┌─────────────────────────────────────────────────────────┐
│                      一句话指令                           │
│               "Python 项目代码审查助手"                    │
└────────────────────────┬────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────┐
│                    Agent 构造器                            │
│  • 生成名称、描述和详细信息                                 │
│  • 从工具仓库中匹配适配的工具                               │
│  • 从技能仓库中匹配适配的技能                               │
└────────────────────────┬────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────┐
│                      AgentProfile                         │
│  { name, description, details, skills, tools, ... }      │
└────────────────────────┬────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────┐
│                     Agent 工作空间                         │
│  即刻可用，直接与用户交互                                   │
└─────────────────────────────────────────────────────────┘
```

## Profile 模板（Spec v1.0）

AgentProfile 是一个 JSON 文件，结构如下：

```jsonc
{
  // 必填：简洁的名称，体现 Agent 的核心角色
  "name": "Python 代码审查助手",

  // 必填：一句话描述 Agent 的定位与功能
  "description": "专注于 Python 代码审查的 AI 助手，提供风格检查、缺陷检测和性能优化建议。",

  // 必填：Markdown 格式的行为规范（章节结构自由）
  "details": "## 角色定位\n\n...\n\n## 核心维度\n\n...",

  // 可选：Agent 模板类型（默认 "default"）
  "agent_template": "default",

  // 可选：Agent 可调用的工具名称
  "tools": [],

  // 可选：要加载的技能目录名
  "skills": ["python-lint", "security-scan"],

  // 可选：子 Agent 名称（每项引用另一个 AgentProfile）
  "subagents": []
}
```

### 字段说明

| 字段 | 类型 | 是否必填 | 说明 |
|------|------|----------|------|
| `name` | `string` | 是 | 简洁的名称，反映 Agent 的角色 |
| `description` | `string` | 是 | 一句话概括 Agent 的角色和能力 |
| `details` | `string` | 是 | Markdown 格式的行为规范（参见下方） |
| `agent_template` | `string` | 否 | 运行时模板类型，默认为 `"default"`。参见[兼容运行时](#兼容运行时) |
| `tools` | `string[]` | 否 | 从工具仓库中匹配的工具标识符 |
| `skills` | `string[]` | 否 | 从技能仓库中匹配的技能模块 |
| `subagents` | `string[]` | 否 | 用于任务委派的子 Agent 名称，每项引用另一个 AgentProfile 的 `name` |

### Details 格式

`details` 字段必须是 Markdown 格式的字符串，章节结构不做限制 — 可根据 Agent 的领域自由组织内容。你也可以将多个源文件的内容（如 `AGENTS.md`、`IDENTITY.md`、`SOUL.md`）拼接为一个 Markdown 字符串。以下是一些常用的章节模式供参考：

#### 角色定位

定义 Agent 的身份、语气和行为理念。

```markdown
## 角色定位

作为[领域][功能]助手，以[风格]的方式帮助用户[核心目标]。
注重[关键原则]。
```

#### 核心维度

Agent 关注点的结构化分解，使用表格或列表格式。

```markdown
## 核心维度

| 维度 | 关注要点 |
|------|----------|
| 维度1 | 具体要点说明 |
| 维度2 | 具体要点说明 |
```

#### 标准规范

质量标准和参考依据。

```markdown
## 标准规范

- 遵循[行业标准 / 最佳实践]
- [评价标准]
- [反馈方式]
```

#### 输出格式

定义 Agent 响应的结构。

```markdown
## 输出格式

1. **步骤一标题**：说明
2. **步骤二标题**：说明
3. **步骤三标题**：说明
```

## 兼容运行时

AgentProfile 与运行时无关。以下运行时已知兼容：

| 运行时 | 仓库 |
|--------|------|
| OpenClaw | [github.com/openclaw/openclaw](https://github.com/openclaw/openclaw) |
| OpenCode | [github.com/anomalyco/opencode](https://github.com/anomalyco/opencode) |
| Codex | [github.com/openai/codex](https://github.com/openai/codex) |
| Claude Code | [github.com/anthropics/claude-code](https://github.com/anthropics/claude-code) |
| OpenBunny | [github.com/fairyshine/OpenBunny](https://github.com/fairyshine/OpenBunny) |

## 快速开始

### 生成 Profile

用一句话描述你的场景：

```
一个处理账单咨询的客户支持 Agent
```

Agent 构造器将自动生成完整的 AgentProfile，包括：
- 合适的 Agent 名称
- 清晰的描述
- 详细的行为规范
- 从工具仓库中匹配的工具
- 从技能仓库中匹配的技能

## 示例

查看 [`examples/`](./examples/) 目录获取不同场景的示例 Profile。

## 贡献

欢迎参与贡献！你可以：

1. **提交新的 Profile 示例** — 分享不同场景下的有效 Agent Profile
2. **改进规范** — 提出对 Profile 格式的补充或改进建议
3. **构建集成** — 创建能够消费或生成 AgentProfile 文档的工具

## 许可证

MIT
