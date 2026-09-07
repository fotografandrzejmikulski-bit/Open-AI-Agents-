# 27 — OmniCore Compound Reasoning & Self-Consistency Engine MAX

## Status
Architecture-ready research and orchestration project.

## Objective
Convert the supplied research on cached mega-prompts, self-consistency and compound AI into a governed reasoning substrate for OmniCore. The goal is not to make one model "think harder" indefinitely, but to allocate a bounded reasoning budget across multiple independent or specialized paths, aggregate evidence, detect disagreement and escalate only when the expected value of additional computation justifies it.

The supplied report argues for a system-centric architecture in which a capable but cheaper model can be embedded in a larger compound system using explicit context caching and batch self-consistency. fileciteturn238file1L8-L33 It also frames early-error propagation in single-shot inference as a structural reliability problem. fileciteturn238file1L37-L63

## Core principle

`reasoning depth = allocated resource`, not a fixed model property.

The engine therefore separates:

```text
TASK
  ↓
COMPLEXITY / CONSEQUENCE ESTIMATION
  ↓
REASONING BUDGET
  ↓
PARALLEL SOLVERS
  ↓
EVIDENCE / ANSWER NORMALIZATION
  ↓
AGREEMENT + CONTRADICTION ANALYSIS
  ↓
FINAL SYNTHESIS
  ↓
VERIFICATION / ESCALATION
```

## 1. Reasoning budget controller

Inputs:

- task complexity;
- uncertainty;
- consequence level;
- required precision;
- available latency budget;
- available compute budget;
- privacy constraints;
- model capability profile;
- prior evaluation performance.

Output:

```text
Budget {
  max_parallel_paths,
  max_tokens_per_path,
  max_wall_time,
  max_retries,
  escalation_policy
}
```

A simple policy can begin with deterministic thresholds and later be learned from evaluation data. The controller may increase computation only when uncertainty or disagreement remains materially high.

## 2. Cached context architecture

Large, stable domain context is treated as a reusable knowledge artifact rather than repeatedly rebuilt prompt text.

```text
DOMAIN PACK
├─ system constraints
├─ terminology
├─ examples
├─ source corpus references
├─ policy
└─ evaluation instructions
        ↓
VERSIONED CONTEXT CACHE
        ↓
N reasoning branches
```

Every cache has:

- content hash;
- provenance;
- policy version;
- model compatibility;
- expiry/invalidation rule;
- access scope.

No cached instruction may silently override current policy.

## 3. Self-consistency ensemble

The engine runs multiple bounded reasoning paths with controlled diversity:

```text
Path A — direct solver
Path B — decomposition solver
Path C — adversarial checker
Path D — retrieval-grounded solver
Path E — alternative-model solver
```

The aggregator compares structured outputs rather than blindly majority-voting free-form text.

Recommended intermediate schema:

```json
{
  "answer": "...",
  "claims": [],
  "evidence": [],
  "assumptions": [],
  "uncertainties": [],
  "confidence": 0.0,
  "failure_modes": []
}
```

## 4. Beyond naive majority vote

Condorcet-style aggregation is useful as a motivating intuition, but production decisions must account for correlated errors. fileciteturn238file1L19-L27

Therefore the aggregator tracks:

- model identity;
- prompt variant;
- retrieval set;
- tool path;
- evidence overlap;
- agreement clusters;
- contradiction graph.

Five agents that copied the same poisoned document do not constitute five independent confirmations.

## 5. Evidence graph

The reasoning engine attaches every substantive conclusion to an evidence graph:

```text
QUESTION
  ↓
CLAIM
  ├── SOURCE
  ├── RETRIEVAL
  ├── COMPUTATION
  ├── MODEL INFERENCE
  └── COUNTERARGUMENT
```

This integrates directly with Project 19's research-orchestration architecture and Project 25's evidence registry.

## 6. Disagreement-driven escalation

Escalation is triggered by measurable signals:

```text
IF high consequence AND disagreement > threshold
    → add adversarial solver

IF evidence conflict > threshold
    → expand retrieval

IF confidence low AND task budget remains
    → sample additional paths

IF uncertainty remains high
    → route to stronger model / human approval
```

This avoids spending maximum compute on every request.

## 7. Prompt compilation layer

Project 24 can compile the natural-language task into a structured reasoning program:

```text
Intent
  → constraints
  → context pack
  → solver graph
  → aggregation rule
  → verification rule
  → output contract
```

Prompt variants become executable artifacts rather than ad-hoc strings. This allows Project 20 to optimize them against frozen evaluation suites.

## 8. Security boundary

Compound reasoning increases attack surface because more model calls, retrieval paths and tools create more opportunities for indirect injection.

The engine therefore inherits Project 26's trust model:

```text
UNTRUSTED CONTENT
        ↓
NORMALIZATION / PROVENANCE
        ↓
MODEL CONTEXT
        ↓
STRUCTURED PLAN
        ↓
CAPABILITY BROKER
        ↓
SIDE EFFECT
```

Consensus does not grant authority. Three agents agreeing that a privileged action is appropriate still cannot bypass the capability broker.

## 9. Cost / latency governor

The engine maintains a live estimate:

```text
expected_value_of_more_reasoning
vs.
expected_cost_of_more_reasoning
```

Additional paths are launched only when the estimated improvement exceeds the configured threshold.

Tracked metrics:

- tokens per successful task;
- latency per successful task;
- accuracy / pass rate;
- disagreement rate;
- escalation rate;
- verification catch rate;
- cost per verified result.

The supplied report presents large potential savings from context caching and compound inference, but those figures are treated as source claims to be experimentally validated rather than repository-wide assumptions. fileciteturn238file1L19-L33

## 10. Evaluation protocol

Frozen benchmark tiers:

| Tier | Strategy | Purpose |
|---|---|---|
| T0 | single-shot baseline | establish reference |
| T1 | cached context | measure context reuse |
| T2 | 3-path ensemble | measure basic self-consistency |
| T3 | 5-path mixed solver | measure robustness |
| T4 | disagreement-triggered escalation | measure compute efficiency |
| T5 | adversarial + poisoned context | measure safety under compound execution |

Compare systems on:

`quality / latency / cost / safety / reproducibility`

## 11. Integration with OmniCore

```text
                         OMNICORE CONTROL PLANE
                                  │
                     +------------+-------------+
                     │                          │
               Policy / Authz              Reasoning Budget
                     │                          │
                     +------------+-------------+
                                  │
                       COMPOUND REASONING ENGINE
                                  │
             +--------------------+--------------------+
             │         │         │         │           │
           Solver A  Solver B  Solver C  Solver D   Solver E
             │         │         │         │           │
             +--------------------+--------------------+
                                  │
                           Aggregation Graph
                                  │
                        Verification / Evals
                                  │
                         Capability Broker
                                  │
                        Deterministic Executor
```

## 12. Definition of done

The engine is complete when:

1. reasoning budget is explicit and measurable;
2. stable context is versioned and reusable;
3. multiple solver paths can run concurrently;
4. aggregation detects correlated evidence and contradictions;
5. escalation is driven by measurable uncertainty;
6. additional computation is bounded by policy;
7. compound reasoning cannot bypass capability authorization;
8. every result is traceable to prompts, models, evidence and evaluation outcomes.

## Position in the portfolio

Project 27 becomes the **reasoning-performance substrate** connecting Projects 15, 16, 18, 19, 20, 24, 25 and 26. It turns the portfolio's doctrine of adaptive reasoning into an executable architecture with measurable compute allocation, ensemble verification and evidence-aware escalation.
