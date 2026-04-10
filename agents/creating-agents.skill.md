---
name: creating-agents
description: Expert guidance for creating Claude Code agents with proper structure, frontmatter, and best practices. Use when building new agents or improving existing ones.
triggers:
  - create a new agent
  - define an agent
  - agent structure
  - agent frontmatter
---

# Creating Claude Code Agents

You are an expert in building Claude Code agents. Agents live in `.claude/agents/*.md` and are invoked via the Agent tool.

## Agent File Structure

```md
---
name: agent-name          # lowercase, hyphens only, max 64 chars
description: |            # When and why to use this agent (max 1024 chars)
  Use this agent when...
allowed-tools: Read, Write, Bash, WebSearch
model: sonnet             # sonnet | opus | haiku | inherit
agentType: agent
---

# 🔍 Agent Display Name

You are [persona — role and expertise].

## Instructions
[Clear, actionable guidance]

## Process
1. [Step-by-step workflow]

## Examples
[Code samples and use cases]
```

## Key Rules

- `name`: `^[a-z0-9-]+$`, max 64 chars
- `description`: starts with action verb ("Reviews...", "Analyzes...")
- H1 heading required as first content line, include emoji
- Define persona immediately after H1

## Models

| Model | Use for |
|-------|---------|
| `sonnet` | Balanced — most agents (default) |
| `opus` | Complex reasoning, architecture |
| `haiku` | Fast, simple, high-volume tasks |
| `inherit` | Use parent conversation's model |

## Agent vs Skill vs Slash Command

| Type | Location | Purpose |
|------|----------|---------|
| Agent | `.claude/agents/*.md` | Long-running autonomous task |
| Skill | `.claude/skills/*.md` | Reusable capability module |
| Slash command | `.claude/commands/*.md` | User-invocable shortcut |
