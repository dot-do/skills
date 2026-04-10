---
name: workflows-do
description: Expert guidance for workflows.do — event-driven AI orchestration, on.Event.action() triggers, scheduled execution, agent loops, and durable workflow patterns.
---

# workflows.do

You are an expert in [workflows.do](https://workflows.do) — event-driven orchestration for the .do platform.

## When to Use

Activate when working with `workflows.do`, `on()`, `every()`, event triggers, or orchestrating multi-agent workflows.

## Event-Driven Workflows

```typescript
import { on } from 'workflows.do'
import { priya, ralph, tom, quinn, mark, sally } from 'agents.do'

on.Idea.captured(async idea => {
  const product = await priya`brainstorm ${idea}`
  const backlog = await priya.plan(product)

  for (const issue of backlog.ready) {
    const pr = await ralph`implement ${issue}`

    // Loop until approved
    do await ralph`update ${pr}`
    while (!await pr.approvedBy(quinn, tom, priya))

    await pr.merge()
  }

  await mark`document and launch ${product}`
  await sally`start outbound for ${product}`
})
```

## Event Syntax

Events follow the pattern `on.Noun.verb(handler)`:

```typescript
on.Idea.captured(handler)       // new idea submitted
on.PR.opened(handler)           // PR opened on GitHub
on.Issue.created(handler)       // GitHub issue created
on.Payment.completed(handler)   // payment processed
on.User.signedUp(handler)       // new user registered
on.Document.uploaded(handler)   // file uploaded
on.Sprint.started(handler)      // sprint kicked off
```

## Scheduled Execution

```typescript
import { every } from 'workflows.do'

every('0 9 * * 1-5', async () => {
  const report = await priya`generate weekly status report`
  await mark`send to stakeholders: ${report}`
})
```

```
every('0 * * * *',    fn)  // hourly
every('0 9 * * *',    fn)  // daily 9am
every('0 9 * * 1-5',  fn)  // weekdays 9am
every('*/15 * * * *', fn)  // every 15 min
```

## Workflow Patterns

```typescript
// Sequential pipeline
on.Order.placed(async (order, ctx) => {
  const validated = await ralph`validate ${order}`
  const enriched  = await priya`enrich with customer context: ${validated}`
  return await ralph`route to fulfillment: ${enriched}`
})

// Parallel fan-out
on.Content.submitted(async (content, ctx) => {
  const [safety, quality, seo] = await Promise.all([
    quinn`check safety of ${content}`,
    quinn`score quality of ${content}`,
    mark`analyze SEO of ${content}`,
  ])
  return { safety, quality, seo }
})

// Human checkpoint
on.Contract.received(async (contract) => {
  const review = await legal`review ${contract}`
  const approved = await ceo`approve: ${review}`
  if (approved) await sally`countersign ${contract}`
})
```

## Lower-Level API (ai-workflows)

```typescript
import { AI, on, every } from 'ai-workflows'

const workflow = AI({
  analyzeDocument: {
    summary: 'string',
    keyPoints: ['string'],
    actionItems: ['string'],
  }
})

on('document-uploaded', async (event, context) => {
  return await context.ai.analyzeDocument({ text: event.data.content })
})
```

## Best Practices

- Name events in `Noun.verb` past-tense form: `PR.opened`, `Idea.captured`
- Design handlers for idempotency — events may be delivered more than once
- Use `Promise.all()` for independent parallel steps
- Return structured data from every handler for observability
- Use `humans.do` for decisions requiring accountability (approvals, legal sign-offs)
