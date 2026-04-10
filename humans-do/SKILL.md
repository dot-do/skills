---
name: humans-do
description: humans.do — bring human workers into .do workflows with the same syntax as AI agents. Slack/email routing, workflow pause/resume, and human approval patterns.
---

# humans.do

You are an expert in [humans.do](https://humans.do) — the .do service for integrating human workers into autonomous workflows using the same syntax as AI agents.

## When to Use

Activate when the user needs human approval, review, or input inside a `.do` workflow.

## The Key Insight

Humans use the *exact same tagged template syntax* as AI agents. No special handling, no callbacks, no webhooks to configure manually.

```typescript
import { priya, ralph } from 'agents.do'
import { legal, ceo, designer } from 'humans.do'

// AI agent
const spec = await priya`define the feature spec`

// Human worker — identical syntax, workflow pauses until they respond
const approved = await ceo`approve this spec: ${spec}`

// Back to AI
const code = await ralph`build ${approved}`
```

## Routing

Messages automatically route to wherever the human is:

```typescript
import { slack, email, sms } from 'humans.do/channels'

// Route to specific channels
await legal.via(slack)`review this contract`
await ceo.via(email)`approve the $50k spend`
```

Default routing is configured per-human in `org.ai`.

## Approval Patterns

```typescript
// Simple approval gate
const approved = await ceo`approve the partnership with ${partner}`
if (!approved) return

// Multi-approver (all must approve)
await pr.approvedBy(quinn, tom, priya)

// First-responder (any one approves)
await legal`sign off on ${contract}`
```

## Timeout & Escalation

```typescript
import { withTimeout, escalate } from 'humans.do'

// Escalate if no response in 4 hours
const review = await withTimeout(
  legal`review ${contract}`,
  { hours: 4, escalateTo: ceo }
)
```

## Best Practices

- Use `humans.do` for decisions with accountability or legal weight
- Keep human tasks atomic — one clear question, one expected response
- Set timeouts on human steps — workflows shouldn't block indefinitely
- `org.ai` is where you configure who each role maps to and their routing preferences
