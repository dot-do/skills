---
name: agents-do
description: Expert guidance for autonomous-agents and agents.do — defining, deploying, and orchestrating autonomous AI agents with triggers, actions, and observable execution.
---

# agents.do

You are an expert in `autonomous-agents` and [agents.do](https://agents.do).

## When to Use

Activate this skill when working with `autonomous-agents`, `Agent()` factory, agent orchestration, or the agents.do managed service.

## Agent Definition

```typescript
import { Agent } from 'autonomous-agents'

const agent = Agent({
  name: 'ContentAgent',
  role: 'content-creator',
  objective: 'Draft, review, and publish content across channels',
  integrations: [
    { name: 'cms',   type: 'api',          endpoint: process.env.CMS_URL },
    { name: 'slack', type: 'notification', channel: '#content' },
  ],
  triggers: ['contentRequested', 'draftReviewed'],
  actions:  ['draftContent', 'reviewDraft', 'schedulePublication'],
  keyResults: [
    { key: 'draftsCompleted', target: 10,   unit: 'per week' },
    { key: 'publishedOnTime', target: 0.95, unit: 'rate' },
  ],
})

// Execute
await agent.execute({ type: 'contentRequested', data: { topic: 'AI' } })
await agent.do.draftContent({ topic: 'AI', audience: 'developers' })
```

## Named Platform Agents

| Agent | Role | Capabilities |
|-------|------|-------------|
| `Priya` | Product | Sprint planning, backlog, stakeholder comms |
| `Ralph` | Engineering | Code review, PR triage, architecture |
| `Tom` | Tech Lead | Cross-team coordination, technical direction |
| `Mark` | Marketing | Content strategy, campaigns |
| `Sally` | Sales | Lead scoring, sequences |
| `Quinn` | QA | Test planning, issue triage |
| `Rae` | Frontend | UI review, accessibility, component gen |

## Multi-Agent Orchestration

```typescript
import { agents } from 'agents.do'

// Delegate to named agent
const plan = await agents.priya`Create a sprint plan for ${features}`

// Pipeline
const reviewed = await agents.ralph`Review: ${prUrl}`
const approved = await agents.tom`Approve if score > 0.8: ${reviewed}`

// Parallel map
const results = await Promise.all(
  issues.map(issue => agents.ralph`Fix: ${issue}`)
)
```

## Best Practices

- One agent per role — no monolithic agents
- Always define `keyResults` — they drive autonomous behavior
- Use triggers (not polling) to wake agents
- Test configurations with `evaluate-do` before production
