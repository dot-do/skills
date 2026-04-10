---
name: workers-rpc
description: Expert guidance for dot-do/workers platform patterns — RPC wrapping, Durable Objects, promise pipelining, and the .do service architecture on Cloudflare Workers.
---

# workers / platform.do

You are an expert in the `dot-do/workers` platform runtime on Cloudflare Workers.

## When to Use

Activate this skill when working with `@dotdo/rpc`, Durable Objects, `.do` service architecture, or Cloudflare Workers deployments.

## RPC Wrapper

Expose any TypeScript object as a full `.do` service (REST + MCP + WebSocket):

```typescript
import { RPC } from '@dotdo/rpc'

export default RPC({
  async processDocument(input: { text: string }) {
    return { summary: '...', wordCount: 42 }
  },
  async listDocuments(filter: { tag?: string }) {
    return [{ id: '1', title: 'Doc 1' }]
  },
}, { name: 'my-service' })
```

## Three Calling Styles

```typescript
// Direct
const result = await service.processDocument({ text: '...' })

// Tagged template (natural language)
const result = await service`process this document: ${text}`

// Template with named params
const fn = service`for {format} documents`
const result = await fn({ format: 'pdf', text: '...' })
```

## Durable Objects

```typescript
import { DOCore, CRUDMixin, EventsMixin } from '@dotdo/do'

class AgentDO extends EventsMixin(CRUDMixin(DOCore)) {
  async execute(input: unknown) {
    const config = await this.storage.get('config')
    const result = await this.process(input, config)
    await this.emit('executed', { input, result })
    return result
  }
}
```

**Mixins:** `CRUDMixin` · `EventsMixin` · `ThingsMixin` · `EventSourcingMixin` · `ActionsMixin`

## Promise Pipelining

```typescript
// ✅ Single round trip
const report = await priya
  .plan(sprint)
  .map(issue => ralph.implement(issue))
  .filter(impl => quinn.test(impl))

// ❌ Multiple round trips
const plan  = await priya.plan(sprint)
const impls = await Promise.all(plan.map(i => ralph.implement(i)))
```

## wrangler.toml

```toml
name = "my-service"
main = "src/index.ts"
compatibility_date = "2025-01-01"

[[durable_objects.bindings]]
name = "MY_DO"
class_name = "MyDO"

[[migrations]]
tag = "v1"
new_classes = ["MyDO"]
```

## Best Practices

- Use `RPC()` for new services — gets REST + MCP + WS for free
- Use DO mixins — don't re-implement CRUD/Events from scratch
- Store agent config in DO storage, not env vars (enables per-tenant config)
- Prefer pipeline chains over sequential awaits for multi-agent calls
