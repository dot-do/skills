<div align="center">

# .do Agent Skills

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
```

---

## Skills Index

### platform.do Services

Skills for the core managed services powering [platform.do](https://platform.do):

| Skill | Service | Description |
|-------|---------|-------------|
| [`functions-do`](functions-do/SKILL.md) | [functions.do](https://functions.do) | Type-safe AI function invocation with schema generation, template literals, and provider routing |
| [`workflows-do`](workflows-do/SKILL.md) | [workflows.do](https://workflows.do) | Event-driven AI orchestration, scheduled execution, fan-out patterns, and human-in-the-loop checkpoints |
| [`agents-do`](agents-do/SKILL.md) | [agents.do](https://agents.do) | Define, deploy, and orchestrate autonomous AI agents with triggers, actions, and observable execution |
| [`database-do`](database-do/SKILL.md) | [database.do](https://database.do) | AI-native data modeling with Nouns/Things, Payload CMS collections, vector search, and AI generation |
| [`evaluate-do`](evaluate-do/SKILL.md) | evaluate.do | Systematic LLM benchmarking, parameter sweeps, and model comparison for agents |
| [`workers-rpc`](workers-rpc/SKILL.md) | [platform.do](https://platform.do) | Cloudflare Workers RPC patterns, Durable Objects, promise pipelining, and .do service architecture |

### Identity & Soul

| Skill | Description |
|-------|-------------|
| [`soul`](soul/SKILL.md) | Define agent soul, identity, and persona using the SOUL.md framework |

### Agent Authoring

| Skill | Description |
|-------|-------------|
| [`creating-agents`](creating-agents/SKILL.md) | Expert guidance for creating Claude Code agents with proper structure and frontmatter |
| [`mdx-injection`](mdx-injection/SKILL.md) | Dynamic MDX template injection for customer/tenant-specific context |

---

## Repository Structure

```
skills/
├── functions-do/          # functions.do — ai-functions
├── workflows-do/          # workflows.do — ai-workflows
├── agents-do/             # agents.do — autonomous-agents
├── database-do/           # database.do — ai-database
├── evaluate-do/           # evaluate.do — ai-experiments
├── workers-rpc/           # platform.do — @dotdo/rpc + Durable Objects
├── soul/                  # Agent soul & identity (SOUL.md framework)
├── creating-agents/       # Claude Code agent authoring
├── mdx-injection/         # Multi-tenant context injection
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

We welcome contributions! Please read [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on adding new skills, improving existing ones, and proposing features.

---

## License

MIT © [.do](https://platform.do) — see [LICENSE](LICENSE) for details.

---

<div align="center">

Made with ♥ by [.do](https://platform.do) · Part of the [dot-do](https://github.com/dot-do) ecosystem

</div>
