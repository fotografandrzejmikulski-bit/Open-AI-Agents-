# 17 — Adaptive Model Router

## Objective
Create a cross-provider routing layer that chooses the least expensive / lowest-latency model capable of satisfying an evaluated quality threshold, with escalation when uncertainty or verification failure rises.

## Source-derived basis
The supplied Gemini and Google AI materials explicitly separate fast and reasoning-oriented models and recommend dynamic selection of reasoning depth based on task complexity. fileciteturn216file6L253-L275 fileciteturn216file4L173-L183

## Architecture

```text
Request
  ↓
Task Classifier
  ↓
Policy Engine
  ├── latency target
  ├── quality target
  ├── modality
  ├── privacy boundary
  ├── budget
  └── consequence level
  ↓
Model Router
  ├── local model
  ├── fast cloud model
  ├── reasoning model
  └── specialist model
  ↓
Verifier
  ├── schema
  ├── tests
  ├── evidence
  └── confidence
  ↓
Escalate / Finalize
```

## Routing policy
1. Classify the task.
2. Select a candidate model satisfying privacy and capability constraints.
3. Allocate a bounded reasoning budget.
4. Verify the result.
5. Escalate only when the quality gate fails or uncertainty exceeds policy.
6. Record routing decisions for later optimization.

## Interfaces
All providers implement a common adapter:
`generate`, `stream`, `tool_call`, `structured_output`, `usage`, `cancel`.

## Metrics
Track quality per task class, cost/request, latency p50/p95, escalation rate, tool error rate, failure recovery and user correction rate.

## Safety
Routing never bypasses safety controls. Provider-specific configuration remains explicit and auditable.
