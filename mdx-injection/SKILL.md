---
name: mdx-injection
description: Patterns for dynamic MDX template injection for customer/tenant-specific context. Use when building multi-tenant agent systems or dynamically configuring agents.
---

# MDX Dynamic Injection

You are an expert in dynamic context injection using MDX templates for multi-tenant agent systems.

## When to Use

Activate this skill when:
- Building an agent that serves multiple customers/tenants
- Dynamically configuring agent behavior per user or org
- Designing the CLAUDE.md injection pipeline

## Injection Layer Pattern

Inject context at three layers, from stable to dynamic:

```
1. Base soul/identity (stable)     → SOUL.md, IDENTITY.md
2. Tenant/customer context (semi)  → injected via MDX template
3. Session context (ephemeral)     → conversation history, current task
```

## MDX Template Pattern

```mdx
---
agent: {agentName}
tenant: {tenantId}
---

# {agentName} — {tenantName} Configuration

You are {agentName}, configured for {tenantName}.

## Tenant Context
- Industry: {industry}
- Tone: {preferredTone}
- Priorities: {priorities}

{customInstructions}
```

## Injection Variable Reference

| Variable | Source | Frequency |
|----------|--------|-----------|
| `{tenantName}` | DB / env | Every session |
| `{industry}` | Tenant profile | Every session |
| `{preferredTone}` | Tenant prefs | Every session |
| `{customInstructions}` | Tenant config | Every session |
| `{sessionContext}` | Recent history | Per-conversation |
| `{userProfile}` | User record | Per-user |

## Best Practices

- Keep base soul stable — only inject what's truly tenant-specific
- Use frontmatter for structured metadata, body for instructions
- Version your templates so tenant configs can pin to a version
