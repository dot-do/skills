# dot-do/skills

Public library of Claude Code skills for the dot.do agent ecosystem.

Skills are reusable, composable MDX modules that can be injected into any Claude Code agent via the `skills` frontmatter key or `npx skills add` command.

## Structure

```
skills/
├── identity/        # Soul, identity, and persona skills
├── memory/          # Memory management skills
├── agents/          # Agent orchestration skills
└── tools/           # Utility and tool skills
```

## Usage

```bash
npx skills add dot-do/skills@<skill-name>
```

## Publishing

This repo is a public submodule of [dot-do/agents](https://github.com/dot-do/agents).
