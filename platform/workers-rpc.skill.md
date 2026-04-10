---
name: workers-rpc
description: Expert guidance for dot-do/workers platform patterns — RPC wrapping, Durable Objects, promise pipelining, and the .do service architecture on Cloudflare Workers.
triggers:
  - dot-do workers
  - RPC wrapper
  - Durable Objects
  - promise pipelining
  - .do service
  - Cloudflare Workers
  - @dotdo/rpc
---

# workers / platform.do Skill

Expert in the `dot-do/workers` platform — Cloudflare Workers, Durable Objects, RPC wrapping, and the unified `.do` service architecture.

## Core Architecture

Every `.do` service is a Cloudflare Worker exposing a unified multi-transport RPC interface:

```
REST  /api/:method          → JSON HTTP
MCP   /mcp                  → JSON-RPC 2.0 (for Claude/AI tools)
WS    /ws                   → CapnWeb (promise pipelining)
```

## RPC Wrapper

Expose any TypeScript object as a full `.do` service:

```typescript
import { RPC } from '@dotdo/rpc'

const myService = {
  async processDocument(input: { text: string; format: string }) {
    return { summary: '...', wordCount: 42 }
  },
  async listDocuments(filter: { tag?: string }) {
    return [{ id: '1', title: 'Doc 1' }]
  },
}

// Expose as Worker with REST + MCP + WebSocket
export default RPC(myService, {
  name: 'my-service',
  description: 'Document processing service',
})
```

## Three Calling Styles

```typescript
// Style 1: Direct async/await
const result = await service.processDocument({ text: '...', format: 'md' })

// Style 2: Tagged template (natural language)
const result = await service`process this document: ${text}`

// Style 3: Template with named params
const fn = service`for {format} documents`
const result = await fn({ format: 'pdf', text: '...' })
```

## Durable Objects

Stateful compute with `@dotdo/do`:

```typescript
import { DOCore, CRUDMixin, EventsMixin } from '@dotdo/do'

class AgentDO extends EventsMixin(CRUDMixin(DOCore)) {
  async initialize(config: AgentConfig) {
    await this.storage.put('config', config)
  }

  async execute(input: unknown) {
    const config = await this.storage.get('config')
    const result = await this.process(input, config)
    await this.emit('executed', { input, result })
    return result
  }
}
```

**Available mixins:**

| Mixin | Adds |
|-------|------|
| `CRUDMixin` | `create`, `read`, `update`, `delete`, `list` |
| `EventsMixin` | `emit`, `on`, `off`, event history |
| `ThingsMixin` | Entity management with versioning |
| `EventSourcingMixin` | Append-only event log, projections |
| `ActionsMixin` | Typed action dispatch with validation |

## Promise Pipelining

Avoid round trips by chaining RPC calls without intermediate awaits:

```typescript
// ✅ Single round trip — pipeline executes server-side
const report = await priya
  .plan(sprint)
  .map(issue => ralph.implement(issue))
  .filter(impl => quinn.test(impl))
  .reduce(results => mark.summarize(results))

// ❌ Multiple round trips
const plan = await priya.plan(sprint)
const impls = await Promise.all(plan.map(i => ralph.implement(i)))
const tested = impls.filter(i => i.passing)
const report = await mark.summarize(tested)
```

## SDK Client Setup

```typescript
import { createClient } from 'rpc.do'

// Auto-detects transport (WebSocket → HTTP fallback)
const functions = createClient('https://functions.do')
const workflows = createClient('https://workflows.do')
const agents = createClient('https://agents.do')

// Credentials resolved from: DO_API_KEY → ORG_AI_TOKEN → env
```

## wrangler.toml Pattern

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

[vars]
SERVICE_NAME = "my-service"
```

## Monorepo Package Organization

```
workers/
├── packages/          # Shared libs (@dotdo/rpc, @dotdo/do, @dotdo/types)
├── workers/           # Deployed Cloudflare Workers
├── sdks/              # Client SDKs (agents.do, functions.do, etc.)
└── integrations/      # External connectors (Stripe, WorkOS, CF)
```

## Best Practices

- Use `RPC()` wrapper for new services — gets REST + MCP + WS for free
- Prefer pipeline chains over sequential awaits for multi-step agent calls
- Use DO mixins — don't re-implement CRUD/Events from scratch
- Store agent config in DO storage, not env vars — enables per-tenant config
- Always export `AgentDO` class alongside the default Worker export
