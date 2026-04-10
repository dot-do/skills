<div align="center">

# skills

**The open agent skills ecosystem for Claude Code**

[![skills.sh](https://img.shields.io/badge/skills.sh-registry-8b5cf6?style=flat-square)](https://skills.sh)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue?style=flat-square)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen?style=flat-square)](CONTRIBUTING.md)
[![Contributor Covenant](https://img.shields.io/badge/Contributor%20Covenant-2.1-4baaaa?style=flat-square)](CODE_OF_CONDUCT.md)

Skills are reusable, composable markdown modules that extend Claude Code agents with new capabilities — soul & identity, dynamic context injection, agent authoring patterns, and more.

[Browse Skills](#skills-index) · [Quick Start](#quick-start) · [Publish a Skill](CONTRIBUTING.md) · [Report a Bug](https://github.com/dot-do/skills/issues/new?template=bug_report.md)

</div>

---

## Quick Start

```bash
# Install a skill into your Claude Code project
npx skills add dot-do/skills@soul
npx skills add dot-do/skills@creating-agents
npx skills add dot-do/skills@mdx-injection
```

Or browse and install from the registry:

```bash
npx skills find "agent identity"
npx skills add <owner/repo@skill-name>
```

---

## Skills Index

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
├── identity/             # Soul, identity, and persona skills
│   └── soul.skill.md
├── agents/               # Agent authoring and orchestration
│   ├── creating-agents.skill.md
│   └── mdx-injection.skill.md
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
├── SECURITY.md
└── LICENSE
```

---

## Contributing

We welcome contributions! Please read [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on:

- Adding new skills
- Improving existing skills
- Reporting issues
- Proposing features

---

## License

MIT © [dot.do](https://dot.do) — see [LICENSE](LICENSE) for details.

---

<div align="center">

Made with ♥ by [dot.do](https://dot.do) · Part of the [dot-do](https://github.com/dot-do) ecosystem

</div>
