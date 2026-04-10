---
name: headlessly
description: headless.ly — SaaS built for agents, not humans. Typed digital objects with verb lifecycle, cross-domain events, and agent-native APIs.
---

# headlessly

You are an expert in [headless.ly](https://headless.ly) — the composable business operating system where every business entity is a typed Digital Object with a verb conjugation lifecycle, event-sourced history, and an agent-native API surface.

## When to Use

Activate when building on the headless.ly platform — defining business entities with `Noun()`, subscribing to cross-domain events, querying with time travel, or integrating headless.ly into the startups.studio control plane.

## The Core Idea: SaaS Built for Agents, Not Humans

headless.ly rebuilds every major SaaS category — CRM, billing, project management, analytics, EHR, inventory, and 40+ more — as typed, event-driven APIs designed for AI agents to operate autonomously. Your agent doesn't need a dashboard. It needs `CRM.Headless.ly/api/contacts`.

The `.do` domain carries a triple meaning:
- **Take Action** — verbs do things to objects
- **Durable Objects** — Cloudflare state primitives, one per tenant
- **Digital Objects** — typed, versioned, event-sourced entities

## Digital Objects: The `Noun()` DSL

Every entity is defined with `Noun()` from the `digital-objects` package — zero dependencies, zero codegen, full TypeScript inference via const generics:

```typescript
import { Noun } from 'digital-objects'

export const Contact = Noun('Contact', {
  name:    'string!',
  email:   'string?#',              // optional, indexed
  stage:   'Lead | Qualified | Customer | Churned | Partner',
  company: '-> Company.contacts',  // forward graph edge
  deals:   '<- Deal.contact[]',    // reverse graph edge
  qualify: 'Qualified',            // custom verb → typed event
  capture: 'Captured',
})
```

## Verb Lifecycle (Conjugation System)

Every verb gets a full conjugation automatically:

```typescript
// Imperative — execute
await contact.qualify()

// BEFORE hook — validate or reject
Contact.qualifying(async (contact, ctx) => {
  if (!contact.email) throw new Error('Email required before qualifying')
})

// AFTER hook — react, trigger side effects
Contact.qualified(async (contact, ctx) => {
  await ctx.Campaign.create({ name: `Onboard ${contact.name}`, type: 'Email' })
})

// Attribution — who/what triggered it
contact.qualifiedBy  // → User or Agent record
```

Opt out of mutations to declare immutability:
```typescript
export const Event = Noun('Event', {
  kind:    'string!',
  payload: 'json',
  update:  null,  // immutable — no updates, no deletes allowed
})
```

## The 35 Core Entities Across 9 Domains

| Domain | Package | Key Entities |
|--------|---------|-------------|
| CRM | `@headlessly/crm` | Organization, Contact, Lead, Deal, Activity, Pipeline |
| Billing | `@headlessly/billing` | Customer, Product, Plan, Price, Subscription, Invoice, Payment |
| Projects | `@headlessly/projects` | Project, Issue, Comment |
| Content | `@headlessly/content` | Content, Asset, Site |
| Support | `@headlessly/support` | Ticket |
| Analytics | `@headlessly/analytics` | Event, Metric, Funnel, Goal |
| Marketing | `@headlessly/marketing` | Campaign, Segment, Form |
| Experiments | `@headlessly/experiments` | Experiment, FeatureFlag |
| Platform | `@headlessly/platform` | Workflow, Integration, Agent |

## Three SDK Import Styles

```typescript
// Universal context — access everything through $
import { $ } from '@headlessly/sdk'
await $.Contact.find({ stage: 'Lead' })

// Domain packages — explicit, tree-shakeable
import { Contact, Deal } from '@headlessly/crm'
import { Subscription }  from '@headlessly/billing'

// Domain namespaces — grouped access
import { crm, billing } from '@headlessly/sdk'
await crm.Contact.find({ stage: 'Qualified' })
```

## Cross-Domain Event Automation

Wire business logic across domains without tight coupling:

```typescript
Deal.closed(async (deal, $) => {
  await $.Subscription.create({ plan: 'pro', customer: deal.contact })
  await $.Campaign.create({ name: `Onboard ${deal.name}`, type: 'Email' })
  await $.Ticket.create({ subject: `Welcome ${deal.name}`, requester: deal.contact })
})
```

## Time Travel Queries

Every entity has a full immutable event log:

```typescript
// Query state as of a past timestamp
const leads = await $.Contact.find(
  { stage: 'Lead' },
  { asOf: '2026-01-15T10:00:00Z' }
)

// Roll back a specific record
await $.Contact.rollback('contact_fX9bL5nRd', { to: '2026-02-06T15:00:00Z' })
```

## Promise Pipelining (One Round-Trip)

Via `rpc.do` — single network round-trip for chained operations:

```typescript
const deals = await $.Contact
  .find({ stage: 'Qualified' })
  .map(contact => contact.deals)
  .filter(deal => deal.stage === 'Open')
```

## Multi-Tenant URL Architecture

```
CRM.Headless.ly/api/contacts       → REST API
CRM.Headless.ly/mcp                → MCP tools surface  
CRM.Headless.ly/openapi            → OpenAPI spec
Healthcare.Headless.ly/crm         → same data, industry-specific defaults
headless.ly/~my-startup/Contact    → tenant-scoped
```

## Entity IDs

All IDs use sqids format: `contact_fX9bL5nRd`, `deal_k7TmPvQx`, `org_aQ4wMnZ`

## Stack

- **Runtime**: Cloudflare Workers + Durable Objects (one DO per tenant, near user)
- **Database**: ParqueDB (`@dotdo/db`) — hybrid relational-document-graph on Apache Parquet
- **Transport**: `rpc.do` with cap'n proto promise pipelining
- **MCP**: Three tools — `search`, `fetch`, `do` (runs arbitrary TypeScript via `ai-evaluate`)
- **Auth**: `oauth.do` — SSO, API keys, multi-tenant isolation
- **Integrations**: Stripe, Composio, Zapier, Slack, Discord, Apollo, BrowserBase, AWS SES
