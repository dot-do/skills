---
name: evaluate-do
description: Expert guidance for ai-experiments — systematic LLM benchmarking, parameter sweeps, experiment result analysis, and model comparison for agents.do workflows.
triggers:
  - ai-experiments
  - Experiment()
  - evaluate agents
  - benchmark models
  - LLM evaluation
  - model comparison
---

# evaluate.do Skill

Expert in `ai-experiments` for systematic AI evaluation — parameter sweeps, model comparisons, and benchmark reporting before production deployment.

## Core Concepts

`Experiment()` runs a cartesian product of parameters (models × temperatures × inputs) and records all results with timing metrics.

```typescript
import { Experiment, cartesian } from 'ai-experiments'

// Run 8 combinations: 2 models × 4 temperatures
const results = await Experiment('sentiment-classifier', {
  models: ['gpt-4o', 'gpt-4o-mini'],
  temperature: [0, 0.3, 0.7, 1.0],
  prompt: ({ input }) => [`Classify the sentiment of: "${input}"`],
  inputs: ['The product is amazing!', 'This is broken and useless.'],
})

console.log(results)
// {
//   name: 'sentiment-classifier',
//   results: [{ params: { model, temperature, input }, output: '...' }, ...],
//   totalTime: 4200,
//   timestamp: '2026-04-10T...'
// }
```

## Experiment Config Reference

```typescript
{
  models: string | string[],          // model(s) to test
  temperature?: number | number[],    // temperature(s) — default [0]
  seed?: number | number[],           // seeds for reproducibility
  prompt: (params) => [string, ...],  // prompt template function
  inputs: any[] | (() => Promise<any[]>),  // test inputs (static or dynamic)
  schema?: object,                    // JSON schema for structured output
  expectedOutputs?: any[],            // for pass/fail validation
}
```

## Vitest Integration

```typescript
import { createRunner } from 'ai-experiments'
import { describe, it } from 'vitest'

const runner = createRunner({ outputDir: '.ai/experiments' })

describe('Agent classification', () => {
  it('classifies intents correctly', runner.run({
    name: 'intent-classifier',
    models: ['claude-sonnet-4-6', 'gpt-4o'],
    temperature: [0, 0.3],
    prompt: ({ input }) => [`Classify intent: "${input}"`],
    inputs: ['Book a flight', 'Cancel my subscription', 'Talk to support'],
    expectedOutputs: ['travel', 'cancellation', 'support'],
  }))
})
```

Results are saved to `.ai/experiments/<name>/` as markdown reports.

## Cartesian Product Utility

```typescript
import { cartesian } from 'ai-experiments'

// Generate all combinations manually
const combos = cartesian({
  model: ['gpt-4o', 'claude-sonnet-4-6'],
  temperature: [0, 0.7],
  systemPrompt: ['concise', 'detailed'],
})
// → 8 combinations
```

## Evaluation Workflow

1. **Define experiment** — choose models, temperatures, inputs
2. **Run experiment** — `Experiment()` executes all combinations
3. **Review results** — markdown report in `.ai/experiments/`
4. **Choose winner** — select best model+temperature for production
5. **Deploy** — configure chosen params in `ai-functions` or `agents.do`

## Best Practices

- Always run experiments before changing model or temperature in production
- Use `seed` for reproducibility when comparing runs
- Test with real representative inputs, not toy examples
- Compare cost vs. quality tradeoffs (smaller models at low temp often match)
- Save experiment results in version control for regression detection
- Run nightly experiments on critical agent paths via `ai-workflows` `every()`
