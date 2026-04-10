---
name: workflows-do
description: Expert guidance for building with ai-workflows and workflows.do — event-driven AI orchestration, scheduled execution, and durable workflow patterns.
triggers:
  - ai-workflows
  - workflows.do
  - event-driven workflow
  - scheduled AI task
  - on() every()
  - workflow orchestration
---

# workflows.do Skill

Expert in `ai-workflows` and the [workflows.do](https://workflows.do) managed service. Helps design event-driven and scheduled AI workflows.

## Core Concepts

Workflows compose AI functions with triggers — events fire handlers, schedules run recurring jobs.

```typescript
import { AI, on, every } from 'ai-workflows'

// Define workflow with typed AI functions
const workflow = AI({
  analyzeDocument: {
    summary: 'string',
    keyPoints: ['string'],
    sentiment: 'positive | neutral | negative',
    actionItems: ['string'],
  },
  sendDigest: {
    sent: 'boolean',
    recipientCount: 'number',
  }
})

// Event-driven: fires when 'document-uploaded' event occurs
on('document-uploaded', async (event, context) => {
  const analysis = await context.ai.analyzeDocument({ text: event.data.content })
  return analysis
})

// Scheduled: runs every weekday at 9am
every('0 9 * * 1-5', async (event, context) => {
  return await context.ai.sendDigest({ date: new Date().toISOString() })
})
```

## Workflow Patterns

### Sequential Pipeline
```typescript
on('order-placed', async (event, ctx) => {
  const validated = await ctx.ai.validateOrder(event.data)
  const enriched = await ctx.ai.enrichWithCustomerData(validated)
  const routed = await ctx.ai.routeToFulfillment(enriched)
  return routed
})
```

### Fan-out (Parallel)
```typescript
on('content-submitted', async (event, ctx) => {
  const [safety, quality, seo] = await Promise.all([
    ctx.ai.checkSafety(event.data),
    ctx.ai.scoreQuality(event.data),
    ctx.ai.analyzeSeo(event.data),
  ])
  return { safety, quality, seo }
})
```

### Human-in-the-Loop Checkpoint
```typescript
on('high-value-lead', async (event, ctx) => {
  const score = await ctx.ai.scoreLead(event.data)
  if (score.confidence < 0.8) {
    // Pause for human review (workflows.do managed pause)
    return { status: 'pending-review', score }
  }
  return await ctx.ai.enrollInSequence(event.data)
})
```

## Common Event Types

| Event | When to use |
|-------|-------------|
| `document-uploaded` | File processing pipelines |
| `user-signed-up` | Onboarding workflows |
| `payment-completed` | Fulfillment triggers |
| `pr-opened` | Code review automation |
| `issue-created` | Support/task routing |
| `data-ready` | ETL completion signals |

## Scheduled Cron Patterns

```typescript
every('0 * * * *',    handler)  // hourly
every('0 9 * * *',    handler)  // daily at 9am
every('0 9 * * 1-5',  handler)  // weekdays at 9am
every('0 9 1 * *',    handler)  // monthly on 1st
every('*/15 * * * *', handler)  // every 15 minutes
```

## Best Practices

- Keep handler functions pure — side effects via `context.ai` only
- Return structured data from every handler for observability
- Use `Promise.all()` for independent parallel steps
- Define clear event schemas — treat events as API contracts
- Name events in past tense: `order-placed`, `document-processed`
- Plan for idempotency — events may be delivered more than once
