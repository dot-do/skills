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
# Install a skill into your Claude Code project
npx skills add dot-do/skills@functions-do
npx skills add dot-do/skills@workflows-do
npx skills add dot-do/skills@agents-do
npx skills add dot-do/skills@database-do
npx skills add dot-do/skills@evaluate-do
npx skills add dot-do/skills@workers-rpc
```

Or browse and install from the registry:

```bash
npx skills find "agent identity"
npx skills add <owner/repo@skill-name>
```

---

## Skills Index

### platform.do Services

Skills for the core managed services powering [platform.do](https://platform.do):

| Skill | Service | Description | Install |
|-------|---------|-------------|---------|
| [`functions-do`](platform/functions-do.skill.md) | [functions.do](https://functions.do) | Type-safe AI function invocation with schema generation, template literals, and provider routing | `npx skills add dot-do/skills@functions-do` |
| [`workflows-do`](platform/workflows-do.skill.md) | [workflows.do](https://workflows.do) | Event-driven AI orchestration, scheduled execution, fan-out patterns, and human-in-the-loop checkpoints | `npx skills add dot-do/skills@workflows-do` |
| [`agents-do`](platform/agents-do.skill.md) | [agents.do](https://agents.do) | Define, deploy, and orchestrate autonomous AI agents with triggers, actions, and observable execution | `npx skills add dot-do/skills@agents-do` |
| [`database-do`](platform/database-do.skill.md) | [database.do](https://database.do) | AI-native data modeling with Nouns/Things, Payload CMS collections, vector search, and AI generation | `npx skills add dot-do/skills@database-do` |
| [`evaluate-do`](platform/evaluate-do.skill.md) | evaluate.do | Systematic LLM benchmarking, parameter sweeps, and model comparison for agents | `npx skills add dot-do/skills@evaluate-do` |
| [`workers-rpc`](platform/workers-rpc.skill.md) | [platform.do](https://platform.do) | Cloudflare Workers RPC patterns, Durable Objects, promise pipelining, and .do service architecture | `npx skills add dot-do/skills@workers-rpc` |

### Identity & Soul

| Skill | Description | Install |
|-------|-------------|---------|
| [`soul`](identity/soul.skill.md) | Define agent soul, identity, and persona using the SOUL.md framework | `npx skills add dot-do/skills@soul` |

### Agent Authoring

| Skill | Description | Install |
|-------|-------------|---------|
| [`creating-agents`](agents/creating-agents.skill.md) | Expert guidance for creating Claude Code agents with proper structure and frontmatter | `npx skills add dot-do/skills@creating-agents` |
| [`mdx-injection`](agents/mdx-injection.skill.md) | Dynamic MDX template injection for customer/tenant-specific context | `npx skills add dot-do/skills@mdx-injection` |

---

## What is a Skill?

A skill is a markdown file with a frontmatter header that tells Claude Code when and how to activate it. Skills are composable — an agent can load multiple skills, and skills can reference each other.

```md
---
name: my-skill
description: What this skill does and when to activate it
triggers:
  - keyword that activates this skill
---

# My Skill

You are an expert in...
```

Skills are distributed via [skills.sh](https://skills.sh) and installed with `npx skills`. This repo is a public submodule of [dot-do/agents](https://github.com/dot-do/agents).

---

## Repository Structure

```
skills/
├── platform/              # platform.do service skills
│   ├── functions-do.skill.md
│   ├── workflows-do.skill.md
│   ├── agents-do.skill.md
│   ├── database-do.skill.md
│   ├── evaluate-do.skill.md
│   └── workers-rpc.skill.md
├── identity/              # Soul, identity, and persona skills
│   └── soul.skill.md
├── agents/                # Agent authoring and orchestration
│   ├── creating-agents.skill.md
│   └── mdx-injection.skill.md
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
├── SECURITY.md
└── LICENSE
```

---

## The .do Platform

This skills library is built for the [dot.do](https://dot.do) platform ecosystem:

| Service | Package | Description |
|---------|---------|-------------|
| [functions.do](https://functions.do) | `ai-functions` | Type-safe AI function invocation |
| [workflows.do](https://workflows.do) | `ai-workflows` | Event-driven AI orchestration |
| [agents.do](https://agents.do) | `autonomous-agents` | Autonomous agent runtime |
| [database.do](https://database.do) | `ai-database` | AI-native data layer |
| [platform.do](https://platform.do) | `dot-do/workers` | Cloudflare Workers runtime |

---

## Contributing

We welcome contributions! Please read [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on adding new skills, improving existing ones, and proposing features.

---

## License

MIT © [dot.do](https://dot.do) — see [LICENSE](LICENSE) for details.

---

<div align="center">

Made with ♥ by [dot.do](https://dot.do) · Part of the [dot-do](https://github.com/dot-do) ecosystem

</div>
