---
name: mdx-injection
description: Patterns for dynamic MDX template injection for customer/tenant-specific context in agents. Use when building multi-tenant agent systems.
triggers:
  - dynamic context injection
  - tenant-specific agent
  - MDX template
  - customer context
---

# MDX Dynamic Injection Skill

Expert in dynamic context injection using MDX templates for multi-tenant agent systems.

## Pattern: Layered Context Injection

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

import { TenantContext } from '@dot-do/context'

<TenantContext
  name="{tenantName}"
  industry="{industry}"
  tone="{preferredTone}"
  knowledgeBase="{kbUrl}"
/>

# {agentName} — {tenantName} Configuration

You are {agentName}, configured specifically for {tenantName}.

## Tenant Context
- Industry: {industry}
- Preferred tone: {preferredTone}
- Key priorities: {priorities}

{customInstructions}
```

## Injection Points

| Variable | Source | When to inject |
|----------|--------|---------------|
| `{tenantName}` | DB / env | Every session |
| `{industry}` | Tenant profile | Every session |
| `{preferredTone}` | Tenant prefs | Every session |
| `{customInstructions}` | Tenant config | Every session |
| `{sessionContext}` | Recent history | Per-conversation |
| `{userProfile}` | User record | Per-user |

## Implementation Notes

- Keep base soul stable — only inject what's truly tenant-specific
- Use frontmatter for structured metadata, body for instructions
- Version your templates so tenant configs can pin to a version
- Test injection with a mock tenant before deploying
