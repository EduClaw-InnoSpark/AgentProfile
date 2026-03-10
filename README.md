# AgentProfile

> **Create Agent with One Sentence.**
>
> An open-source specification for defining AI agent profiles. Describe what you want in one sentence, and the Agent Generator will produce a complete, structured AgentProfile.

[中文版](./README_zh.md)

## What is AgentProfile?

AgentProfile is a JSON-based open standard for describing AI agents. It provides a unified format to capture an agent's identity, capabilities, behavioral specifications, and toolset — all generated from a single natural language instruction.

```
"A customer support agent for SaaS products" → AgentProfile JSON → Ready-to-use Agent
```

## Workflow

```
┌─────────────────────────────────────────────────────────┐
│                   One Sentence Instruction                │
│          "A code review assistant for Python projects"    │
└────────────────────────┬────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────┐
│                     Agent Generator                      │
│  • Generate name, description and details                │
│  • Match relevant tools from tool repository             │
│  • Match relevant skills from skill repository           │
└────────────────────────┬────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────┐
│                    AgentProfile JSON                      │
│  { name, description, details, skills, tools, ... }      │
└────────────────────────┬────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────┐
│                     Agent Workspace                       │
│  Ready to interact with users                            │
└─────────────────────────────────────────────────────────┘
```

## Profile Template (Spec v1.0)

An AgentProfile is a JSON file with the following structure:

```jsonc
{
  // Required: concise name capturing the agent's core role
  "name": "Python Code Review Assistant",

  // Required: one-sentence description of the agent's purpose
  "description": "An AI assistant focused on Python code review, providing style checks, bug detection, and performance optimization suggestions.",

  // Required: detailed Markdown spec (see Details Format below)
  "details": "## Role\n\n...\n\n## Core Dimensions\n\n...\n\n## Standards\n\n...\n\n## Output Format\n\n...",

  // Optional: agent template type (default: "default")
  "agent_template": "default",

  // Optional: tool names the agent can invoke
  "tools": [],

  // Optional: skill directory names to load
  "skills": ["python-lint", "security-scan"],

  // Optional: sub-agent names for delegation
  "subagents": []
}
```

### Field Reference

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `name` | `string` | Yes | Concise name reflecting the agent's role |
| `description` | `string` | Yes | One-sentence summary of the agent's role and capabilities |
| `details` | `string` | Yes | Markdown-formatted behavioral specification (see below) |
| `agent_template` | `string` | No | Template type, defaults to `"default"` |
| `tools` | `string[]` | No | List of tool identifiers from the tool repository |
| `skills` | `string[]` | No | Skill modules from the skill repository |
| `subagents` | `string[]` | No | Sub-agents for task delegation |

### Details Format

The `details` field must be a Markdown string containing these sections:

#### 1. Role

Define the agent's identity, tone, and behavioral philosophy.

```markdown
## Role

As a [domain] [function] assistant, use a [style] approach to help users [core goal].
Focus on [key principle].
```

#### 2. Core Dimensions

Structured breakdown of what the agent focuses on. Use a table or list format.

```markdown
## Core Dimensions

| Dimension | Focus Points |
|-----------|-------------|
| Dimension 1 | Specific focus description |
| Dimension 2 | Specific focus description |
```

#### 3. Standards

Quality criteria and reference standards.

```markdown
## Standards

- Follow [industry standard / best practice]
- [Evaluation criteria]
- [Feedback methodology]
```

#### 4. Output Format

Define the structure of the agent's responses.

```markdown
## Output Format

1. **Step 1 Title**: Description
2. **Step 2 Title**: Description
3. **Step 3 Title**: Description
```

## Quick Start

### Generate a Profile

Describe your scenario in one sentence:

```
A customer support agent that handles billing inquiries
```

The Agent Generator will automatically produce a complete AgentProfile including:
- An appropriate agent name
- A clear description
- Detailed behavioral specifications
- Matched tools from the tool repository
- Matched skills from the skill repository

## Examples

See the [`examples/`](./examples/) directory for sample profiles covering various scenarios.

## Contributing

We welcome contributions! You can:

1. **Submit new profile examples** — share effective agent profiles for different scenarios
2. **Improve the spec** — propose additions or refinements to the profile format
3. **Build integrations** — create tools that consume or generate AgentProfile JSON

## License

MIT
