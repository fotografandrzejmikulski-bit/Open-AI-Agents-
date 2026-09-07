# 18 — Gemini 3 Max Cognitive Agent

## Status
Research → architecture-ready prototype.

## Objective
Build a multimodal, tool-using research/coding agent that allocates reasoning depth to task complexity, preserves explicit execution state around tool calls, uses code execution for verifiable computation, and routes consequential actions through policy and human approval.

## Source-derived principles
The supplied Gemini material describes thinking models, configurable thinking depth/budget, tool calling, thought signatures, multimodal processing, code execution and agentic development through Antigravity. fileciteturn219file0L28-L35 fileciteturn219file0L41-L70

The architecture adopts the useful engineering insight—reasoning is a resource—without treating hidden reasoning state as an application-level source of truth. Internal model state is opaque; application state is explicit and durable.

The material also describes programmatic visual analysis through Python/OpenCV/NumPy and high-resolution video analysis. fileciteturn217file2L91-L116

## Architecture

```text
USER INTENT
   ↓
TASK CLASSIFIER
   ├─ trivial → fast path
   ├─ analytical → deeper reasoning
   ├─ multimodal → visual/audio pipeline
   ├─ coding → sandbox + tests
   └─ consequential → approval path
   ↓
MODEL ROUTER
   ↓
REASONING POLICY
   ↓
AGENT LOOP
   ├─ plan
   ├─ tool call
   ├─ observe
   ├─ verify
   └─ continue / stop
   ↓
VERIFIER
   ↓
FINAL ARTIFACT + PROVENANCE
```

## State model

Never persist hidden chain-of-thought as application truth. Persist:

- task_id;
- conversation/session ID;
- task specification;
- tool-call IDs and normalized inputs/outputs;
- observations;
- hypotheses;
- evidence references;
- verification results;
- approval state;
- final result;
- model/provider/version metadata.

## Reasoning budget policy

```text
complexity = {simple, moderate, complex, frontier}
uncertainty = {low, medium, high}
consequence = {low, medium, high}

budget = policy(complexity, uncertainty, consequence)
```

Escalation rule:

`simple + low consequence → fast`

`complex or uncertain → deeper reasoning`

`high consequence → reasoning + external verification + approval`

The supplied source explicitly argues for dynamic selection of reasoning depth rather than using maximum reasoning on every request. fileciteturn216file6L253-L275

## Tool/state continuity

Tool calls are modeled as explicit state transitions:

`reasoning → tool_request → execution → observation → verification → continuation`

Any model-specific mechanism for continuity, including thought-signature-like metadata, is treated as opaque transport state rather than trusted business state. The source describes thought signatures as continuity metadata around multi-step tool use. fileciteturn216file6L276-L282

## Multimodal verification

For image/video tasks:

1. ingest original media;
2. identify measurable claims;
3. run deterministic analysis where possible;
4. have the model interpret results;
5. compare model interpretation with computed evidence;
6. attach provenance to every quantitative conclusion.

This avoids relying solely on visual intuition when a computational measurement is feasible.

## Code execution boundary

Generated code executes only inside a sandbox with explicit CPU, memory, duration, filesystem and network policy. Results return as typed artifacts. The agent may use computation to verify geometry, data extraction, charts or transformations, but generated code is never trusted solely because the model generated it.

## Security

Do not use this project to bypass content or safety controls. The supplied Gemini material contains references to safety-filter bypass and jailbreak techniques; these are reclassified here as adversarial test cases and regression inputs rather than implementation requirements. fileciteturn216file5L214-L223

Required defenses:

- prompt-injection detection;
- tool-argument validation;
- least-privilege capabilities;
- sandbox isolation;
- approval gates;
- provenance;
- adversarial regression suite;
- rate and cost limits.

## Evaluation

Benchmark dimensions:

| Dimension | Metric |
|---|---|
| Task success | pass@task |
| Reasoning efficiency | quality / inference cost |
| Tool reliability | successful tool transitions |
| Factuality | verified claim rate |
| Multimodal accuracy | measurement agreement |
| Safety | blocked unsafe transitions |
| Recovery | successful resume rate |
| Latency | p50/p95/p99 |

A/B-test reasoning policies against a fixed task set. Never optimize on a single benchmark.

## Integration targets

- OpenAI Agents SDK runtime;
- MCP capability layer;
- Google Gemini API adapter;
- sandbox execution;
- durable session/state store;
- evaluation harness;
- tracing/observability;
- optional Antigravity-style coding-agent workflow.

The supplied material also emphasizes MCP as a mechanism for connecting an agent to private databases, documentation and ticketing systems. fileciteturn217file5L214-L227

## Definition of done

The prototype is complete when the same task suite demonstrates that adaptive reasoning beats a fixed maximum-reasoning policy on the chosen quality/cost/latency frontier, while all consequential operations remain policy-controlled and auditable.
