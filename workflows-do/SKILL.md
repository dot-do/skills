---
name: workflows-do
description: Expert guidance for ai-workflows and workflows.do — event-driven AI orchestration, scheduled execution, and durable workflow patterns.
---

# workflows.do

You are an expert in `ai-workflows` and [workflows.do](https://workflows.do).

## When to Use

Activate this skill when working with `ai-workflows`, `on()`, `every()`, event-driven AI, or workflow orchestration.

## Core API

```typescript
import { AI, on, every } from 'ai-workflows'

const workflow = AI({
  analyzeDocument: {
    summary: 'string',
    keyPoints: ['string'],
    actionItems: ['string'],
  }
})

// Event-driven
on('document-uploaded', async (event, context) => {
  return await context.ai.analyzeDocument({ text: event.data.content })
})

// Scheduled
every('0 9 * * 1-5', async (event, context) => {
  return await context.ai.sendDigest({})
})
```

## Workflow Patterns

```typescript
// Sequential pipeline
on('order-placed', async (event, ctx) => {
  const validated = await ctx.ai.validateOrder(event.data)
  const enriched  = await ctx.ai.enrichWithCustomerData(validated)
  return await ctx.ai.routeToFulfillment(enriched)
})

// Parallel fan-out
on('content-submitted', async (event, ctx) => {
  const [safety, quality, seo] = await Promise.all([
    ctx.ai.checkSafety(event.data),
    ctx.ai.scoreQuality(event.data),
    ctx.ai.analyzeSeo(event.data),
  ])
  return { safety, quality, seo }
})
```

## Cron Reference

```
every('0 * * * *',    fn)  // hourly
every('0 9 * * *',    fn)  // daily 9am
every('0 9 * * 1-5',  fn)  // weekdays 9am
every('*/15 * * * *', fn)  // every 15 min
```

## Best Practices

- Name events in past tense: `order-placed`, `document-processed`
- Return structured data from every handler for observability
- Design handlers for idempotency — events may arrive more than once
- Use `Promise.all()` for independent parallel steps
