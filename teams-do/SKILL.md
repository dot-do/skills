---
name: teams-do
description: teams.do — coordinate groups of agents as functional teams (product, engineering, marketing, sales). Team-level imports and cross-team workflow patterns.
---

# teams.do

You are an expert in [teams.do](https://teams.do) — group agents into functional teams for higher-level coordination.

## When to Use

Activate when the user wants to coordinate multiple agents as a team rather than orchestrating individuals.

## Core Usage

```typescript
import { product, engineering, marketing, sales } from 'teams.do'

// Team-level calls — the team coordinates internally
const mvp  = await product`define the MVP for ${idea}`
const app  = await engineering`build ${mvp}`
await marketing`launch ${app}`
await sales`start outreach for ${app}`
```

## Team Composition

| Team | Agents | Responsibility |
|------|--------|---------------|
| `product` | Priya | Specs, roadmaps, priorities, stakeholder coordination |
| `engineering` | Ralph, Tom, Quinn | Build, architecture, testing, code review |
| `marketing` | Mark | Copy, content, launches, brand |
| `sales` | Sally | Outreach, demos, pipeline, closing |
| `design` | Rae | UI, frontend, accessibility, components |

## Individual vs Team

```typescript
import { ralph, tom, quinn } from 'agents.do'   // individuals
import { engineering } from 'teams.do'           // team

// Individual — direct control
const code = await ralph`implement ${spec}`
const review = await tom`review ${code}`

// Team — let the team coordinate
const shipped = await engineering`implement, review, and test ${spec}`
```

Use individuals when you need predictable, sequential handoffs. Use teams when you want the group to self-organize.

## Custom Teams

```typescript
import { Startup } from 'startups.do'
import { engineering, product } from 'teams.do'

// Teams are composable
export default Startup({
  name: 'MyStartup',
  teams: {
    core: { ...engineering, ...product },
    growth: { ...sales, ...marketing },
  }
})
```

## Best Practices

- Prefer team-level calls for strategic work (`product\`plan Q2\``)
- Use individual agents for precise, sequential workflows
- Teams self-coordinate — don't micromanage the internal handoffs
