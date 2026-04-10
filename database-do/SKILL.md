---
name: database-do
description: Expert guidance for ai-database and database.do — AI-native data modeling, Payload CMS collections, Nouns/Things pattern, vector search, and workflow execution.
---

# database.do

You are an expert in `ai-database` and [database.do](https://database.do).

## When to Use

Activate this skill when working with `ai-database`, `DB()`, Payload CMS collections, Nouns/Things data modeling, or the database.do service.

## Low-Level CRUD

```typescript
import { db } from 'ai-database'

const user   = await db.findOne({ collection: 'users', where: { email: { equals: 'alice@example.com' } } })
const users  = await db.find({ collection: 'users', limit: 20, sort: '-createdAt' })
const newRec = await db.create({ collection: 'users', data: { email: 'bob@example.com' } })
await db.update({ collection: 'users', id: newRec.id, data: { role: 'admin' } })
await db.delete({ collection: 'users', id: newRec.id })
const rec    = await db.getOrCreate({ collection: 'products', where: { slug: 'widget' }, data: {...} })
```

## Typed Models with DB()

```typescript
import { DB } from 'ai-database'
import { z } from 'zod'

const Product = DB({
  id: 'product',
  schema: z.object({
    name: z.string(),
    slug: z.string(),
    price: z.number(),
    tags: z.array(z.string()),
  }),
  generate: 'generateProductListing',  // AI auto-fill function
  context: 'E-commerce product for a SaaS marketplace',
})

const products = await Product.find()
const product  = await Product.create({ name: 'Widget Pro', price: 49 })
```

## Database Configuration

```bash
DATABASE_URI=file:./data.db          # SQLite (dev)
DATABASE_URI=libsql://db.turso.io    # Turso serverless
DATABASE_URI=mongodb://...           # MongoDB
DATABASE_URI=postgresql://...        # PostgreSQL
```

## Core Collections

`nouns` · `things` · `functions` · `workflows` · `events` · `generations` · `models`

## Best Practices

- Use `DB()` for domain models, `db` for cross-collection operations
- Set `generate` on Noun definitions to enable AI auto-fill
- Use `getOrCreate` over manual check-then-create for idempotency
- Treat `events` as an append-only audit log — never delete
