---
name: functions-do
description: Expert guidance for building with ai-functions and functions.do — type-safe AI function invocation, schema generation, template literals, and provider routing.
triggers:
  - ai-functions
  - functions.do
  - AI() factory
  - typed AI function
  - generateObject
  - ai template literal
---

# functions.do Skill

Expert in `ai-functions` and the [functions.do](https://functions.do) managed service. Helps design, generate, and debug type-safe AI functions.

## Core Concepts

`ai-functions` transforms unpredictable LLM outputs into reliable, typed components using schema validation and template literals.

**Three invocation styles:**

```typescript
import { ai, AI, list } from 'ai-functions'

// 1. Template literal — ad-hoc generation
const summary = await ai`Summarize this article: ${article}`

// 2. Typed factory — schema-validated generation
const myAI = AI({
  classifyIntent: {
    category: 'string',
    confidence: 'number',
    reasoning: 'string',
  }
})
const result = await myAI.classifyIntent({ text: userMessage })

// 3. List generation — arrays or async iteration
for await (const item of list`List 10 use cases for ${topic}`) {
  console.log(item)
}
```

## Schema Design

Schemas use plain TypeScript object notation (no Zod required at call site):

```typescript
const contentAI = AI({
  generateBlogPost: {
    title: 'string',
    slug: 'string',
    excerpt: 'string',
    sections: ['string'],        // array of strings
    tags: ['string'],
    readingTimeMinutes: 'number',
    seoScore: 'number',
  },
  extractKeyPoints: {
    points: ['string'],
    sentiment: 'positive | neutral | negative',
    confidence: 'number',
  }
})
```

## Built-in Domain Functions

Pre-built helpers for common tasks:

| Function | Description |
|----------|-------------|
| `extract` | Extract structured data from text |
| `is` | Boolean classification |
| `say` | Conversational response generation |
| `research` | Multi-step research synthesis |
| `scrape` | Web content extraction |
| `code` | Code generation |
| `mdx` | MDX document generation |
| `plan` | Strategic planning |
| `scope` | Requirements scoping |
| `workflow` | Workflow definition generation |
| `ui` | UI component generation |

## Configuration

```typescript
const result = await myAI.generateContent({
  topic: 'AI agents',
  model: 'claude-opus-4-6',     // override model
  temperature: 0.7,              // creativity
  maxTokens: 2000,               // response length
  system: 'You are a technical writer...',  // system prompt
})
```

## Environment Setup

```bash
# .env
AI_GATEWAY=https://gateway.ai.cloudflare.com/v1/...  # optional, auto-detected
ANTHROPIC_API_KEY=...
OPENAI_API_KEY=...
```

## Best Practices

- Define schemas once, reuse across the app — create an `ai/` directory
- Use `list()` for streaming UX, `AI()` for structured data, `ai\`\`` for one-offs
- Narrow schema types with union strings: `'draft | published | archived'`
- Group related functions into a single `AI()` instance per domain
- Test functions with `ai-experiments` before production
