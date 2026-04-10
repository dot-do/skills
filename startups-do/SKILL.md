---
name: startups-do
description: startups.do and business-as-code — define entire autonomous startups in TypeScript with the Startup() DSL, teams, workflows, and platform services.
---

# startups.do

You are an expert in [startups.do](https://startups.do) — define and run autonomous startups entirely in code.

## When to Use

Activate when the user is defining a startup, business, or autonomous organization using the `.do` platform.

## Business-as-Code

```typescript
import { Startup } from 'startups.do'
import { engineering, product, sales, marketing } from 'teams.do'
import { dev, sales as salesWorkflow } from 'workflows.do'

export default Startup({
  name: 'Acme AI',
  teams: {
    engineering,
    product,
    sales,
    marketing,
  },
  workflows: {
    build: dev,
    sell:  salesWorkflow,
  },
  services: [
    'llm.do',
    'payments.do',
    'database.do',
    'org.ai',
  ],
})
```

That's a company. It builds products, sells them, and grows.

## Platform Services

```typescript
import { llm }      from 'llm.do'
import { payments } from 'payments.do'
import { db }       from 'database.do'
import { org }      from 'org.ai'
import { search }   from 'searches.do'

await llm`summarize this article`
await payments.charge(customer, amount)
await db.find({ collection: 'users', where: { active: true } })
await org.users.invite(email)
```

## Full Platform Reference

| Service | Import | Description |
|---------|--------|-------------|
| [agents.do](https://agents.do) | `agents.do` | Named AI agents |
| [teams.do](https://teams.do) | `teams.do` | Agent teams |
| [humans.do](https://humans.do) | `humans.do` | Human workers |
| [workflows.do](https://workflows.do) | `workflows.do` | Event-driven orchestration |
| [functions.do](https://functions.do) | `functions.do` | AI function invocation |
| [database.do](https://database.do) | `database.do` | AI-native data |
| [llm.do](https://llm.do) | `llm.do` | LLM inference |
| [payments.do](https://payments.do) | `payments.do` | Stripe Connect billing |
| [searches.do](https://searches.do) | `searches.do` | Semantic & vector search |
| [actions.do](https://actions.do) | `actions.do` | Tool calling & side effects |
| [triggers.do](https://triggers.do) | `triggers.do` | Webhooks, schedules, events |
| [integrations.do](https://integrations.do) | `integrations.do` | External service connectors |
| [analytics.do](https://analytics.do) | `analytics.do` | Metrics, traces, insights |
| [org.ai](https://org.ai) | `org.ai` | Identity, SSO, users, secrets |

## The Founder Patterns

```typescript
// Solo founder — get a team without hiring one
import { product, engineering, marketing } from 'teams.do'
const mvp  = await product`define the MVP`
const app  = await engineering`build ${mvp}`
await marketing`launch ${app}`

// Small team — AI does the work, humans decide
import { ceo } from 'humans.do'
const decision = await ceo`should we pivot to enterprise?`

// Growing startup — add humans without changing code
import { ralph } from 'agents.do'   // today: AI
// import { alice } from 'humans.do' // tomorrow: hire Alice, same interface
```

## Best Practices

- Define your startup in a single `startup.ts` — it's your company manifest
- Services are composable — start with 2-3, add more as you scale
- Humans and agents are interchangeable in the type system — design for both
- `org.ai` manages identity, secrets, and permissions — always start there
