# Contributing to dot-do/skills

Thank you for your interest in contributing! This is a public skills library for Claude Code agents. Contributions of all kinds are welcome.

## Ways to Contribute

- **Add a new skill** — share a reusable capability module
- **Improve an existing skill** — fix errors, expand guidance, add examples
- **Report a bug** — open an issue if a skill behaves unexpectedly
- **Suggest a feature** — open a discussion or issue with your idea

---

## Adding a New Skill

### 1. File Naming Convention

Skills are markdown files with the `.skill.md` suffix:

```
<category>/<skill-name>.skill.md
```

Place your skill in the most appropriate category folder:

| Folder | Skills for… |
|--------|-------------|
| `identity/` | Agent soul, persona, identity definition |
| `agents/` | Agent authoring, orchestration, patterns |
| `memory/` | Memory management, context persistence |
| `tools/` | Utility tools, integrations |

If no category fits, propose a new one in your PR.

### 2. Skill File Structure

Every skill must include valid frontmatter and an H1 heading:

```md
---
name: my-skill
description: One-sentence description of what this skill does and when to use it.
triggers:
  - phrase that activates this skill
  - another trigger phrase
---

# My Skill Title

You are an expert in [domain]. When activated...

## Instructions
[Clear, actionable guidance]

## Examples
[Concrete examples]
```

**Frontmatter fields:**

| Field | Required | Description |
|-------|----------|-------------|
| `name` | Yes | Lowercase, hyphens only (`^[a-z0-9-]+$`) |
| `description` | Yes | When and why to use this skill (max 1024 chars) |
| `triggers` | Recommended | Keywords/phrases that activate the skill |

### 3. Quality Checklist

Before submitting, verify:

- [ ] Frontmatter is valid YAML
- [ ] `name` matches the filename (without `.skill.md`)
- [ ] Description clearly explains when to activate the skill
- [ ] H1 heading is the first line of content
- [ ] Instructions are actionable, not just descriptive
- [ ] Examples are concrete and realistic
- [ ] No sensitive data, credentials, or PII

### 4. Update the README

Add your skill to the appropriate table in [README.md](README.md).

---

## Pull Request Process

1. Fork the repository
2. Create a branch: `git checkout -b skill/my-skill-name`
3. Add your skill and update README
4. Open a PR with a clear title and description
5. A maintainer will review within a few days

---

## Reporting Issues

Use the issue templates:

- [Bug Report](.github/ISSUE_TEMPLATE/bug_report.md) — something is broken
- [Feature Request](.github/ISSUE_TEMPLATE/feature_request.md) — suggest a new skill or improvement

---

## Code of Conduct

This project follows the [Contributor Covenant](CODE_OF_CONDUCT.md). Be kind, be constructive.
