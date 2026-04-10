---
name: evaluate-do
description: Expert guidance for ai-experiments — LLM benchmarking, parameter sweeps, model comparison, and pre-production evaluation of agents and functions.
---

# evaluate.do

You are an expert in `ai-experiments` for systematic AI evaluation.

## When to Use

Activate this skill when benchmarking models, running parameter sweeps, comparing LLM outputs, or evaluating agents before production.

## Core API

```typescript
import { Experiment, cartesian } from 'ai-experiments'

// Runs 8 combinations: 2 models × 4 temperatures
const results = await Experiment('sentiment-test', {
  models: ['claude-sonnet-4-6', 'gpt-4o'],
  temperature: [0, 0.3, 0.7, 1.0],
  prompt: ({ input }) => [`Classify sentiment: "${input}"`],
  inputs: ['Amazing product!', 'Completely broken.'],
})
// Results saved to .ai/experiments/sentiment-test/
```

## Config Reference

| Field | Type | Description |
|-------|------|-------------|
| `models` | `string \| string[]` | Model(s) to test |
| `temperature` | `number \| number[]` | Temperature sweep |
| `seed` | `number \| number[]` | For reproducibility |
| `prompt` | `(params) => string[]` | Prompt template |
| `inputs` | `any[] \| async fn` | Test inputs |
| `schema` | `object` | JSON schema for structured output |
| `expectedOutputs` | `any[]` | For pass/fail validation |

## Vitest Integration

```typescript
import { createRunner } from 'ai-experiments'

const runner = createRunner({ outputDir: '.ai/experiments' })

it('classifies intents', runner.run({
  name: 'intent-classifier',
  models: ['claude-sonnet-4-6'],
  temperature: [0, 0.3],
  prompt: ({ input }) => [`Classify intent: "${input}"`],
  inputs: ['Book a flight', 'Cancel subscription'],
}))
```

## Evaluation Workflow

1. Define experiment — models, temperatures, representative inputs
2. Run — `Experiment()` executes all combinations
3. Review — markdown report in `.ai/experiments/<name>/`
4. Choose winner — best model + temperature for production
5. Deploy — configure chosen params in `ai-functions` or `agents.do`

## Best Practices

- Use `seed` for reproducibility when comparing runs
- Test with real inputs, not toy examples
- Run nightly experiments on critical paths via `workflows-do` `every()`
- Commit experiment results to version control for regression detection
