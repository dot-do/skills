---
name: agents-do
description: Expert guidance for agents.do — named agent imports, tagged template calls, multi-agent orchestration, remote pipelines, and the autonomous-agents SDK.
---

# agents.do

You are an expert in [agents.do](https://agents.do) — the .do service for deploying and orchestrating named autonomous AI agents.

## When to Use

Activate when working with `agents.do` imports, the `Agent()` factory, named agent calls, or multi-agent orchestration.

## The SDK — Named Imports

```typescript
import { priya, ralph, tom, mark, quinn, rae, sally } from 'agents.do'

// Natural language — just say what you want
const spec   = await priya`spec out user authentication`
const code   = await ralph`build ${spec}`
const review = await tom`review ${code}`
const tests  = await quinn`test ${review} thoroughly`
```

Each agent has a real GitHub identity. When Tom reviews your PR, you'll see `@tom-do` commenting.

## Pipeline with Remote .map()

```typescript
const sprint = await priya`plan the sprint`
  .map(issue => ralph`build ${issue}`)
  .map(code  => tom`review ${code}`)
```

The `.map()` is a **remote operation** — not JavaScript's Array.map. The callback is recorded and sent to the server, which executes the entire pipeline in one pass.

## Named Agents

| Import | Agent | Role | Tagline |
|--------|-------|------|---------|
| `priya` | Priya | Product | Specs, roadmaps, priorities |
| `ralph` | Ralph | Engineering | Ship iteratively |
| `tom` | Tom | Tech Lead | Architecture, code review |
| `rae` | Rae | Frontend | React, UI, accessibility |
| `mark` | Mark | Marketing | Copy, content, launches |
| `sally` | Sally | Sales | Outreach, demos, closing |
| `quinn` | Quinn | QA | Testing, edge cases, quality |

## Lower-Level: Agent() Factory

For custom agents not in the named roster:

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
  triggers:   ['contentRequested', 'draftReviewed'],
  actions:    ['draftContent', 'reviewDraft', 'schedulePublication'],
  keyResults: [
    { key: 'draftsCompleted', target: 10,   unit: 'per week' },
    { key: 'publishedOnTime', target: 0.95, unit: 'rate' },
  ],
})

await agent.execute({ type: 'contentRequested', data: { topic: 'AI agents' } })
await agent.do.draftContent({ topic: 'AI agents', audience: 'developers' })
```

## Multi-Agent Orchestration

```typescript
// Sequential handoff
const spec     = await priya`spec out ${feature}`
const code     = await ralph`build ${spec}`
const reviewed = await tom`review ${code}`

// Parallel
const [safety, quality] = await Promise.all([
  quinn`check security of ${code}`,
  tom`review architecture of ${code}`,
])

// Event-driven loop
import { on } from 'workflows.do'

on.PR.opened(async pr => {
  const review = await tom`review ${pr}`
  if (review.approved) await pr.merge()
  else await ralph`address feedback: ${review}`
})
```

## Best Practices

- Use named imports (`priya`, `ralph`) for platform agents — they have real identity and history
- Use `Agent()` factory for custom/tenant-specific agents
- Keep pipeline chains declarative — `.map()` is more efficient than sequential awaits
- Always define `keyResults` on custom agents — they drive autonomous behavior
