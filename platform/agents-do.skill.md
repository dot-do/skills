---
name: agents-do
description: Expert guidance for building with autonomous-agents and agents.do — defining, deploying, and orchestrating autonomous AI agents with triggers, actions, and observable execution.
triggers:
  - autonomous-agents
  - agents.do
  - Agent() factory
  - autonomous agent
  - agent orchestration
  - digital worker
---

# agents.do Skill

Expert in `autonomous-agents` and the [agents.do](https://agents.do) managed service. Helps design, configure, and orchestrate autonomous AI agents.

## Core Concepts

Agents are defined with a configuration object specifying their role, objective, integrations, triggers, and actions. The `Agent()` factory returns an executable agent instance.

```typescript
import { Agent } from 'autonomous-agents'

const agent = Agent({
  name: 'ContentAgent',
  role: 'content-creator',
  objective: 'Draft, review, and publish content across channels',
  
  integrations: [
    { name: 'cms', type: 'api', endpoint: process.env.CMS_URL },
    { name: 'slack', type: 'notification', channel: '#content' },
  ],
  
  triggers: ['contentRequested', 'draftReviewed', 'publishScheduled'],
  
  actions: [
    'draftContent',
    'reviewDraft',
    'schedulePublication',
    'notifyStakeholders',
  ],
  
  keyResults: [
    { key: 'draftsCompleted', target: 10, unit: 'per week' },
    { key: 'publishedOnTime', target: 0.95, unit: 'rate' },
  ],
})
```

## Execution Patterns

```typescript
// Direct execution
const result = await agent.execute({
  type: 'contentRequested',
  data: { topic: 'AI agents', format: 'blog-post', wordCount: 1500 }
})

// Dynamic action invocation
await agent.do.draftContent({ topic: 'AI agents', audience: 'developers' })
await agent.do.notifyStakeholders({ message: 'Draft ready for review' })

// Event handler (auto-generated from triggers)
agent.onContentRequested(async (event) => {
  return await agent.do.draftContent(event.data)
})
```

## Agent Configuration Reference

| Field | Type | Description |
|-------|------|-------------|
| `name` | string | Agent identifier (PascalCase) |
| `role` | string | Functional role slug (kebab-case) |
| `objective` | string | Primary mission statement |
| `integrations` | array | External services the agent can call |
| `triggers` | string[] | Events that wake the agent |
| `actions` | string[] | Actions the agent can take |
| `keyResults` | array | OKR-style success metrics |
| `searches` | array | Search providers available to agent |

## Named dot.do Agents

Pre-built agents in the platform ecosystem:

| Agent | Role | Key capabilities |
|-------|------|-----------------|
| `Priya` | Product | Sprint planning, backlog grooming, stakeholder comms |
| `Ralph` | Engineering | Code review, PR triage, architecture decisions |
| `Tom` | Tech Lead | Cross-team coordination, technical direction |
| `Mark` | Marketing | Content strategy, campaign planning |
| `Sally` | Sales | Lead scoring, sequence management |
| `Quinn` | QA | Test planning, issue triage, regression analysis |
| `Rae` | Frontend | UI review, accessibility, component generation |

## Multi-Agent Orchestration

```typescript
import { agents } from 'agents.do'

// Delegate to a named agent
const plan = await agents.priya`Create a sprint plan for ${features}`

// Pipeline across agents
const reviewed = await agents.ralph`Review this PR: ${prUrl}`
const approved = await agents.tom`Approve if quality score > 0.8: ${reviewed}`

// Distributed map
const results = await Promise.all(
  issues.map(issue => agents.ralph`Fix this issue: ${issue}`)
)
```

## Observability

Every `execute()` call records:
- Timestamp and duration
- Input/output snapshots
- Action invocations
- Integration calls
- Key result updates

Access via `agent.history` or the agents.do dashboard.

## Best Practices

- One agent per role — don't build monolithic agents
- Define `keyResults` for every agent — success metrics drive behavior
- Use triggers (not polling) to wake agents
- Log action inputs/outputs — observability is non-negotiable
- Test with `ai-experiments` before production deployment
