---
name: database-do
description: Expert guidance for building with ai-database and database.do — AI-native data modeling with Nouns/Things, Payload CMS collections, vector search, and workflow execution.
triggers:
  - ai-database
  - database.do
  - DB() factory
  - Noun Things
  - Payload CMS
  - vector search
  - ai-native database
---

# database.do Skill

Expert in `ai-database` and the [database.do](https://database.do) managed service. Helps design AI-native data models, collections, and generation workflows.

## Core Concepts

`ai-database` is built on Payload CMS and models data around **Nouns** (types) and **Things** (instances). AI can generate, enrich, and search Things automatically.

## Low-Level CRUD

```typescript
import { db } from 'ai-database'

// Find
const user = await db.findOne({
  collection: 'users',
  where: { email: { equals: 'alice@example.com' } }
})

const users = await db.find({
  collection: 'users',
  where: { role: { equals: 'admin' } },
  limit: 20,
  sort: '-createdAt',
})

// Create / Update / Delete
const newUser = await db.create({ collection: 'users', data: { email: 'bob@example.com' } })
await db.update({ collection: 'users', id: newUser.id, data: { role: 'admin' } })
await db.delete({ collection: 'users', id: newUser.id })

// Upsert / Get-or-create
const existing = await db.upsert({ collection: 'users', where: { email: 'carol@example.com' }, data: {...} })
const instance = await db.getOrCreate({ collection: 'products', where: { slug: 'widget' }, data: {...} })
```

## Typed Data Models with DB()

```typescript
import { DB } from 'ai-database'
import { z } from 'zod'

const Product = DB({
  id: 'product',
  schema: z.object({
    name: z.string(),
    slug: z.string(),
    description: z.string(),
    price: z.number(),
    tags: z.array(z.string()),
  }),
  generate: 'generateProductListing',  // AI function to auto-fill fields
  context: 'E-commerce product listing for a SaaS tools marketplace',
})

// Use like a typed ORM
const products = await Product.find()
const product = await Product.create({ name: 'Widget Pro', price: 49 })
```

## AI-Powered Generation

```typescript
import { ai } from 'ai-database'

// Generate structured data
const profile = await ai('Generate a user profile for ${email}', {
  function: 'generateProfile',
  model: 'claude-sonnet-4-6',
  output: 'Object',
  temperature: 0.7,
  maxTokens: 1000,
})

// Workflow with db + ai access
const workflowCode = `
  export default async (event, { ai, db }) => {
    const related = await db.things.findSimilar({ data: event.data })
    const enriched = await ai(\`Enrich this with context: \${JSON.stringify(related)}\`)
    await db.things.create({ data: enriched })
    return enriched
  }
`
```

## Core Collections

| Collection | Purpose |
|------------|---------|
| `nouns` | Data type definitions (like table schemas) |
| `things` | Data instances (rows with AI generation) |
| `functions` | AI function definitions |
| `workflows` | Multi-step execution code |
| `events` | Execution audit log |
| `generations` | AI completion records |
| `models` | AI model configurations |

## Database Support

Configure via `DATABASE_URI` environment variable:

```bash
DATABASE_URI=file:./data.db          # SQLite (default, development)
DATABASE_URI=libsql://db.turso.io    # Turso (serverless SQLite)
DATABASE_URI=mongodb://...           # MongoDB
DATABASE_URI=postgresql://...        # PostgreSQL
DATABASE_URI=postgres://...          # Vercel Postgres
```

## Vector Search

256-dimensional float32 embeddings with automatic indexing:

```typescript
// Store with embedding
await db.create({
  collection: 'things',
  data: { content: 'AI agents are...', embedding: Float32Array.from(vector) }
})

// Semantic search
const similar = await db.things.findSimilar({
  embedding: queryVector,
  limit: 10,
  threshold: 0.8,
})
```

## Best Practices

- Use `DB()` for domain models, `db` for system/cross-collection operations
- Set `generate` on Noun definitions to enable AI auto-fill
- Keep schemas Zod-validated — ai-database enforces types at write time
- Use `events` collection for audit trails — don't delete, only append
- Prefer `getOrCreate` over manual check-then-create for idempotency
