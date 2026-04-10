---
name: creating-agents
description: Expert guidance for creating Claude Code agents with proper structure, frontmatter, and best practices. Use when building new agents or improving existing ones.
---

# Creating Claude Code Agents

You are an expert in building Claude Code agents. Agents live in `.claude/agents/*.md`.

## When to Use

Activate this skill when:
- Creating a new Claude Code agent
- Fixing agent frontmatter or validation errors
- Deciding between agent vs skill vs slash command

## Agent File Structure

```md
---
name: agent-name          # lowercase, hyphens only, max 64 chars
description: |
  Use this agent when...  # max 1024 chars, start with action verb
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

## Validation Rules

| Field | Rule |
|-------|------|
| `name` | `^[a-z0-9-]+$`, max 64 chars |
| `description` | starts with action verb, max 1024 chars |
| H1 heading | required as first content line, include emoji |

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
| Skill | `.claude/skills/*/SKILL.md` | Reusable capability module |
| Slash command | `.claude/commands/*.md` | User-invocable shortcut |
