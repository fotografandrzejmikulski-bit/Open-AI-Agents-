# 16 — Prompt Laboratory & Evaluation Engine

## Objective
Build a laboratory for generating, varying, testing and versioning prompts as executable behavioral configurations rather than static text.

## Source-derived basis
The supplied prompt-engineering material frames a strong prompt as a combination of structural precision, cognitive framing and iterative evaluation, and discusses in-context learning, chain-based reasoning, meta-prompting and constraint-based prompting. fileciteturn213file1L7-L31 fileciteturn214file6L249-L285

## Architecture

```text
Prompt Spec
   ↓
Variant Generator
   ├── role / objective
   ├── constraints
   ├── examples
   ├── output schema
   └── reasoning policy
   ↓
Execution Matrix
   ├── models
   ├── temperatures / budgets
   ├── context sizes
   └── tool configurations
   ↓
Evaluator
   ├── correctness
   ├── consistency
   ├── citation/provenance
   ├── latency/cost
   └── safety
   ↓
Selector
   ↓
Versioned Prompt Artifact
```

## Variable prompting
Prompts should be represented as structured templates with explicit variables and constraints. Generate families of variants instead of one “magic prompt”. Maintain an experiment record for each variant.

## Evaluation loop
`generate → run → score → analyze failures → mutate → rerun → select → freeze`.

Do not optimize for benchmark scores alone. Include adversarial, edge-case and regression suites.

## Prompt contract
```json
{
  "prompt_id": "string",
  "version": "string",
  "objective": "string",
  "variables": {},
  "constraints": [],
  "examples": [],
  "output_schema": {},
  "evaluation_suite": "string"
}
```

## Safety
Constraint engineering must not be used to hide instructions from users, evade model safeguards or induce covert behavioral influence. Security evaluation may test for hidden directives and prompt injection, but the laboratory is a defensive optimization system.

## Acceptance criteria
A prompt version becomes production-ready only when it beats the current baseline across the predefined evaluation suite without unacceptable increases in cost, latency, hallucination or safety risk.
