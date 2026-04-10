---
name: startups-do
description: startups.do + Startups.Studio — define entire AI-generated startups as code, or operate them through the multi-surface control plane (CLI, API, SDK, MCP, web).
---

# startups.do + Startups.Studio

You are an expert in [startups.do](https://startups.do) and [Startups.Studio](https://startups.studio) — the platform for building startups as structured Business-as-Code objects, operated by a default team of AI agents across every surface.

## When to Use

Activate when the user is defining a startup, operating a business via the platform, running a Foundation Sprint, generating startup ideas from a Thesis, or working with the Startups.Studio control plane.

## Business-as-Code

A startup is a structured system, not scattered SaaS state. Define it in TypeScript:

```typescript
import { Startup } from 'startups.do'
import { engineering, product, sales, marketing } from 'teams.do'
import { dev, sell } from 'workflows.do'

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
    sell,
  },
  services: [
    'llm.do',
    'payments.do',
    'database.do',
    'org.ai',
  ],
})
```

That's a company. It builds products, sells them, and grows — operated by AI agents using the same `agents.do` SDK.

## The Default Agent Team

Every new startup created via Startups.Studio ships with a core team of named AI agents pre-configured as `agents` records:

| Agent | Role | Domain |
|-------|------|--------|
| [Priya](https://priya.do) | Product Manager | product |
| [Ralph](https://ralph.do) | Implementation Specialist | engineering |
| [Tom](https://tom.do) | Tech Lead / TypeScript Architect | engineering |
| [Rae](https://rae.do) | Frontend / React Lead | frontend |
| [Mark](https://mark.do) | Marketing Lead | marketing |
| [Sally](https://sally.do) | Sales Lead | sales |
| [Quinn](https://quinn.do) | QA Lead | qa |

Agents and human roles are interchangeable in the type system — swap in a human with zero code changes:

```typescript
import { priya } from 'agents.do'   // AI agent today
// import { sarah } from 'humans.do'  // hire Sarah tomorrow, same interface
```

## The Multi-Surface Control Plane

Startups.Studio exposes one shared data model across five surfaces:

| Surface | Use it when |
|---------|------------|
| CLI | Terminal-first workflows — `startups.studio discover customer` |
| API | Direct HTTP integration — native Payload REST + `/api/register` |
| SDK | TypeScript code — typed collection clients |
| MCP | Agent clients — discoverable tools over the entire collection model |
| Web apps | Human visibility — admin, docs, marketing, ops |

All surfaces read/write the same records. Move between them without rebuilding state.

## Collection Families (50+ Collections)

**Identity & Workspace:** `studios`, `startups`, `domains`, `users`, `templates`

**Discovery & Strategy:** `ideas`, `hypotheses`, `experiments`, `lean-canvases`, `story-brands`, `business-models`, `competitors`, `differentiators`, `approaches`, `theses`, `advantages`

**Model & Execution:** `nouns`, `verbs`, `things`, `functions`, `workflows`, `actions`, `tasks`, `routines`, `documents`, `events`

**Agents & Operations:** `agents`, `goals`, `projects`, `approvals`, `sandboxes`, `browsers`

**Commercial:** `customers`, `contacts`, `leads`, `deals`, `accounts`, `campaigns`, `products`, `services`, `subscriptions`, `budgets`, `cost-events`, `revenue-events`

**Data & Integrations:** `sources`, `resources`, `integrations`, `chats`, `messages`

## Agents Collection Schema

Every agent in a startup — AI or human — is a typed record:

```typescript
{
  name: 'Priya',
  startup: { id: 'startup_abc123' },
  role: 'Product Manager',
  objective: 'Define what gets built and in what order',
  agentType: 'ai',           // 'ai' | 'human'
  adapterType: 'claude-code', // claude-code | agent-sdk | openclaw | cursor | gemini | human
  capabilities: ['product-planning', 'sprint-management', 'stakeholder-communication'],
  budgetMonthlyCents: 5000,
}
```

## Foundation Sprint — Codified

Startups.Studio runs Jake Knapp's Foundation Sprint as CLI commands, producing a `Founding Hypothesis`:

> *If we help [customer] solve [problem] with [approach], they will choose it over [competitors] because our solution is [differentiation].*

```bash
startups.studio discover customer    # → ICPs collection
startups.studio discover problem     # → Ideas collection
startups.studio discover advantages  # → Advantages collection
startups.studio discover competitors # → Competitors collection
startups.studio define hypothesis    # → Hypotheses collection
```

An AI agent can run the entire 2-day sprint in minutes. A human can work through it interactively.

## Thesis-Driven Startup Factory

Define a strategic Thesis and the platform generates startup ideas at scale:

```typescript
// 1. Define your thesis
startups.studio theses create --json '{
  "statement": "AI agents can replace professional services costing $50–200/hr",
  "domains": ["onet", "naics"],
  "filters": {
    "onet": { "minMedianWage": 50, "automationProbability": ">0.6" },
    "naics": { "sectors": ["54", "52"] }
  }
}'

// 2. Generate ideas (fan-out workflow)
// ~800 occupations × ~200 filtered industries = ~160,000 evaluations
// Each scored on TAM, feasibility, differentiation

// 3. Foundation Sprint on top ideas
// 4. Build, launch, measure
```

**Reference data powering generation:**
| Collection | Source | Size |
|-----------|--------|------|
| Industries | NAICS | 1,012 codes |
| Occupations | SOC/ONET | 867 codes |
| Processes | APQC | ~1,500 codes |
| Products/Services | UNSPSC | ~70,000 codes |

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

| Service | Description |
|---------|-------------|
| `agents.do` | Named AI agents — Priya, Ralph, Tom, Rae, Mark, Sally, Quinn |
| `teams.do` | Functional agent teams |
| `humans.do` | Human workers — same syntax as AI agents |
| `workflows.do` | Event-driven orchestration |
| `functions.do` | AI function invocation |
| `database.do` | AI-native data layer |
| `llm.do` | LLM inference |
| `payments.do` | Stripe Connect billing |
| `searches.do` | Semantic & vector search |
| `actions.do` | Tool calling & side effects |
| `triggers.do` | Webhooks, schedules, events |
| `integrations.do` | External service connectors |
| `analytics.do` | Metrics, traces, insights |
| `org.ai` | Identity, SSO, users, secrets |

## Bootstrapping a New Startup

```bash
# From idea to working startup
npx create-startups "AI-powered legal contract review for SMBs"

# What it does:
# 1. Registers org + startup in Startups.Studio
# 2. Provisions headless.ly entities (35 core + startup-specific)
# 3. Configures default agent team (Priya, Ralph, Tom, Rae, Mark, Sally, Quinn)
# 4. Runs Foundation Sprint (ICP, problem, advantages, competitors, hypothesis)
# 5. Returns CLI access + API keys + MCP endpoint
```

## Best Practices

- Every startup is one shared model — CLI, API, SDK, MCP, and web all read/write the same records
- Start with the `create-startups` CLI for fastest path from idea to first authenticated request
- Agents and humans are interchangeable — design interfaces for both from day one
- `org.ai` manages identity and secrets — always provision it first
- Use the `agents` collection to define your team — both AI and human roles — before building workflows
