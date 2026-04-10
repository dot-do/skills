---
name: workers-do
description: The high-level .do platform SDK — named agent imports, tagged template calls, remote pipeline map(), and the full workers.do developer experience.
---

# workers.do

You are an expert in the [workers.do](https://workers.do) platform SDK — the highest-level interface for building with autonomous agents, teams, and workflows.

## When to Use

Activate when the user is writing code that imports from `agents.do`, `teams.do`, `workflows.do`, `humans.do`, `workers.do`, or `startups.do`.

## The Basics

```typescript
import { priya, ralph, tom, mark } from 'agents.do'

priya`plan the Q1 roadmap`
ralph`build the authentication system`
tom`review the architecture`
mark`write the launch announcement`
```

No method names. No parameters. Just say what you want — in plain language.

## Named Agents

```typescript
import { priya, ralph, tom, mark, quinn, rae, sally } from 'agents.do'

// Each agent is a tagged template function
const spec   = await priya`spec out user authentication`
const code   = await ralph`build ${spec}`
const review = await tom`review ${code}`
const tests  = await quinn`test ${review} thoroughly`
const docs   = await mark`document ${review}`
```

Each agent has a real GitHub identity (`@priya-pdm`, `@ralph-do`, etc.) — when Tom reviews your PR, you'll see `@tom-do` commenting.

## Pipelines

Chain agents without multiple round trips:

```typescript
// Pipeline a sprint end-to-end
const sprint = await priya`plan the sprint`
  .map(issue => ralph`build ${issue}`)
  .map(code  => tom`review ${code}`)
```

The `.map()` isn't JavaScript's — it's a remote operation. The callback is recorded, not executed. The server receives the entire pipeline and executes it in one pass.

## Teams

```typescript
import { product, engineering, marketing } from 'teams.do'

const mvp  = await product`define the MVP`
const app  = await engineering`build ${mvp}`
await marketing`launch ${app}`
```

`teams.do` groups agents by function. `product` = Priya + stakeholder coordination. `engineering` = Ralph + Tom + Quinn. `marketing` = Mark.

## Humans in the Loop

Humans use the *exact same syntax* as agents:

```typescript
import { legal, ceo } from 'humans.do'

const contract = await legal`review this agreement`
const approved = await ceo`approve the partnership`
```

Messages route to Slack, email, or wherever your human is. The workflow pauses and resumes when they respond — same API, no special handling needed.

## Event-Driven Workflows

```typescript
import { on } from 'workflows.do'
import { priya, ralph, tom, quinn, mark, sally } from 'agents.do'

on.Idea.captured(async idea => {
  const product = await priya`brainstorm ${idea}`
  const backlog = await priya.plan(product)

  for (const issue of backlog.ready) {
    const pr = await ralph`implement ${issue}`

    do await ralph`update ${pr}`
    while (!await pr.approvedBy(quinn, tom, priya))

    await pr.merge()
  }

  await mark`document and launch ${product}`
  await sally`start outbound for ${product}`
})
```

Real development workflows. Event-driven. PR-based. Agents and humans in the same loop.

## Business-as-Code

```typescript
import { Startup } from 'startups.do'
import { engineering, product, sales } from 'teams.do'
import { dev, sales as salesWorkflow } from 'workflows.do'

export default Startup({
  name: 'Acme AI',
  teams:     { engineering, product, sales },
  workflows: { build: dev, sell: salesWorkflow },
  services:  ['llm.do', 'payments.do', 'org.ai'],
})
```

That's a company. It builds products, sells them, and grows.

## Install

```bash
npm install agents.do
```

## The Named Agents

| Agent | Role | Tagline |
|-------|------|---------|
| `priya` | Product | Specs, roadmaps, priorities |
| `ralph` | Engineering | Ship iteratively |
| `tom` | Tech Lead | Architecture, code review |
| `rae` | Frontend | React, UI, accessibility |
| `mark` | Marketing | Copy, content, launches |
| `sally` | Sales | Outreach, demos, closing |
| `quinn` | QA | Testing, edge cases, quality |

## Best Practices

- Use tagged templates for natural language tasks — avoid `.method()` calls when possible
- Keep pipelines declarative — let the server optimize execution order
- Use `humans.do` for decisions that require judgment or accountability
- Import from `teams.do` when you want team-level coordination, `agents.do` for individual agents
