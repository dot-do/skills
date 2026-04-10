<div align="center">

# skills

**The open agent skills ecosystem for Claude Code**

[![skills.sh](https://img.shields.io/badge/skills.sh-registry-8b5cf6?style=flat-square)](https://skills.sh)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue?style=flat-square)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen?style=flat-square)](CONTRIBUTING.md)
[![Contributor Covenant](https://img.shields.io/badge/Contributor%20Covenant-2.1-4baaaa?style=flat-square)](CODE_OF_CONDUCT.md)

Skills are reusable, composable markdown modules that extend Claude Code agents with new capabilities — soul & identity, dynamic context injection, agent authoring patterns, and the full [platform.do](https://platform.do) SDK ecosystem.

[Browse Skills](#skills-index) · [Quick Start](#quick-start) · [Publish a Skill](CONTRIBUTING.md) · [Report a Bug](https://github.com/dot-do/skills/issues/new?template=bug_report.md)

</div>

---

## Quick Start

```bash
npx skills add dot-do/skills@functions-do
npx skills add dot-do/skills@workflows-do
npx skills add dot-do/skills@agents-do
npx skills add dot-do/skills@database-do
npx skills add dot-do/skills@evaluate-do
npx skills add dot-do/skills@workers-rpc
npx skills add dot-do/skills@soul
npx skills add dot-do/skills@creating-agents
```

---

## Skills Index

### platform.do Services

| Skill | Service | Description |
|-------|---------|-------------|
| [`functions-do`](functions-do/SKILL.md) | [functions.do](https://functions.do) | Type-safe AI function invocation — `AI()` factory, schema design, template literals, provider routing |
| [`workflows-do`](workflows-do/SKILL.md) | [workflows.do](https://workflows.do) | Event-driven orchestration — `on()`, `every()`, sequential/parallel/HITL patterns |
| [`agents-do`](agents-do/SKILL.md) | [agents.do](https://agents.do) | Autonomous agents — `Agent()` config, named agents, multi-agent pipelines |
| [`database-do`](database-do/SKILL.md) | [database.do](https://database.do) | AI-native data — `DB()` models, Nouns/Things, vector search, AI generation |
| [`evaluate-do`](evaluate-do/SKILL.md) | evaluate.do | LLM benchmarking — `Experiment()`, parameter sweeps, model comparison |
| [`workers-rpc`](workers-rpc/SKILL.md) | [platform.do](https://platform.do) | Cloudflare Workers — `RPC()` wrapper, Durable Objects, promise pipelining |

### Identity & Soul

| Skill | Description |
|-------|-------------|
| [`soul`](soul/SKILL.md) | Define agent soul, identity, and persona using the SOUL.md framework |

### Agent Authoring

| Skill | Description |
|-------|-------------|
| [`creating-agents`](creating-agents/SKILL.md) | Create Claude Code agents with correct structure, frontmatter, and validation rules |
| [`mdx-injection`](mdx-injection/SKILL.md) | Dynamic MDX template injection for multi-tenant agent configuration |

---

## What is a Skill?

A skill is a directory containing a `SKILL.md` file. Claude Code loads skills into the agent's context, activating the capability described inside.

```
my-skill/
└── SKILL.md    ← frontmatter + instructions
```

```md
---
name: my-skill
description: What this skill does and when Claude should activate it
---

# My Skill

You are an expert in...
```

Install with `npx skills`, publish via [skills.sh](https://skills.sh). This repo is a public submodule of [dot-do/agents](https://github.com/dot-do/agents).

---

## Repository Structure

```
skills/
├── functions-do/        # functions.do — ai-functions
├── workflows-do/        # workflows.do — ai-workflows
├── agents-do/           # agents.do — autonomous-agents
├── database-do/         # database.do — ai-database
├── evaluate-do/         # evaluate.do — ai-experiments
├── workers-rpc/         # platform.do — @dotdo/rpc + Durable Objects
├── soul/                # Agent soul & identity (SOUL.md framework)
├── creating-agents/     # Claude Code agent authoring
├── mdx-injection/       # Multi-tenant context injection
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
├── SECURITY.md
└── LICENSE
```

---

## The .do Platform

| Service | Package | Description |
|---------|---------|-------------|
| [functions.do](https://functions.do) | `ai-functions` | Type-safe AI function invocation |
| [workflows.do](https://workflows.do) | `ai-workflows` | Event-driven AI orchestration |
| [agents.do](https://agents.do) | `autonomous-agents` | Autonomous agent runtime |
| [database.do](https://database.do) | `ai-database` | AI-native data layer |
| [platform.do](https://platform.do) | `dot-do/workers` | Cloudflare Workers runtime |

---

## Contributing

Read [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on adding skills, improving existing ones, and proposing features.

---

## License

MIT © [.do](https://platform.do) — see [LICENSE](LICENSE) for details.

---

<div align="center">

Made with ♥ by [.do](https://platform.do) · Part of the [dot-do](https://github.com/dot-do) ecosystem

</div>
