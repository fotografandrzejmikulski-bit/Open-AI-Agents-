# 20 — Adaptive Prompt Lab

## Status
Research → architecture-ready prototype.

## Objective
Turn prompt engineering into an experimentally measured optimization loop. Generate prompt variants from task requirements, constraints and examples; run them against a fixed evaluation set; compare quality, factuality, robustness, latency and cost; then promote only reproducible winners.

## Source-derived principles
The supplied prompt-engineering material defines the useful core as the combination of structural precision, cognitive framing and iterative evaluation. It also discusses few-shot example ordering, CoT-style decomposition, meta-prompting and constraint-based prompting. fileciteturn219file1L17-L31 fileciteturn214file6L249-L280

The system therefore treats a prompt as a versioned artifact with tests, not as a static paragraph.

## Architecture

```text
TASK SPEC
  ↓
PROMPT SCHEMA
  ↓
VARIANT GENERATOR
  ├─ structural variants
  ├─ example variants
  ├─ constraint variants
  ├─ reasoning-policy variants
  └─ output-schema variants
  ↓
EVALUATION MATRIX
  ↓
STATISTICAL COMPARISON
  ↓
ROBUSTNESS TESTS
  ↓
PROMOTION / REJECTION
```

## Prompt schema

Every prompt version contains:

- objective;
- role/context only where useful;
- constraints;
- required evidence;
- task decomposition;
- output schema;
- failure behavior;
- examples, if demonstrated to help;
- evaluation hooks;
- version metadata.

## Variant generation

Generate controlled deltas rather than uncontrolled rewrites:

`baseline → one change → benchmark → retain/reject`

This makes causal attribution possible.

## Example ordering experiment

When using few-shot examples, evaluate multiple orderings and permutations. The supplied material claims that example order can materially affect accuracy; treat this as an empirical variable to test, not as a universal constant. fileciteturn214file6L276-L280

## Constraint engine

Constraint-based prompting may include:

- lexical restrictions;
- output-length bounds;
- required sections;
- forbidden unsupported claims;
- schema validation;
- source citation requirements;
- explicit uncertainty labels.

Constraints must reduce ambiguity without creating unnecessary prompt complexity.

## Meta-prompting

A separate optimizer may propose improved prompts, but promotion is gated by the same objective benchmark used for human-written prompts. The optimizer never evaluates itself using only its own judgment.

## Evaluation

```text
quality score
factuality score
format-validity
instruction adherence
robustness under perturbation
latency
cost
safety
```

Use paired tasks and regression suites. Keep a frozen holdout set to prevent overfitting to the optimization benchmark.

## Robustness suite

Test:

- paraphrases;
- reordered inputs;
- irrelevant context;
- missing fields;
- contradictory evidence;
- long-context noise;
- adversarial instructions embedded in source material.

## Security

Prompt optimization must never be used to bypass safety systems. Materials discussing jailbreaks are useful as adversarial test categories, not as recipes for removing controls.

## Definition of done

The lab is successful when it can show, on a held-out evaluation set, that a promoted prompt improves the target metric without unacceptable degradation in safety, factuality, latency or cost.
