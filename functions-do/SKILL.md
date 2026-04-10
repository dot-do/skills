---
name: functions-do
description: Expert guidance for ai-functions and functions.do — type-safe AI function invocation, schema generation, template literals, and provider routing.
---

# functions.do

You are an expert in `ai-functions` and [functions.do](https://functions.do).

## When to Use

Activate this skill when the user is working with `ai-functions`, `functions.do`, `AI()` factory, typed AI schemas, or template literal prompts.

## Three Invocation Styles

```typescript
import { ai, AI, list } from 'ai-functions'

// 1. Ad-hoc template literal
const summary = await ai`Summarize: ${article}`

// 2. Typed factory with schema
const myAI = AI({
  classifyIntent: {
    category: 'string',
    confidence: 'number',
    reasoning: 'string',
  }
})
const result = await myAI.classifyIntent({ text: userMessage })

// 3. List generation
for await (const item of list`List 10 use cases for ${topic}`) {
  console.log(item)
}
```

## Schema Design

```typescript
const contentAI = AI({
  generateBlogPost: {
    title: 'string',
    slug: 'string',
    sections: ['string'],        // array
    tags: ['string'],
    sentiment: 'positive | neutral | negative',  // union
    readingTimeMinutes: 'number',
  }
})
```

## Built-in Domain Functions

`extract` · `is` · `say` · `research` · `scrape` · `code` · `mdx` · `plan` · `scope` · `workflow` · `ui` · `image` · `markdown`

## Configuration

```typescript
const result = await myAI.generate({
  topic: 'AI agents',
  model: 'claude-sonnet-4-6',
  temperature: 0.7,
  maxTokens: 2000,
  system: 'You are a technical writer...',
})
```

## Best Practices

- Group related functions into a single `AI()` instance per domain
- Use `list()` for streaming UX, `AI()` for structured data, `ai\`\`` for one-offs
- Narrow types with union strings: `'draft | published | archived'`
- Test with `evaluate-do` skill before production
