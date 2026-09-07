# Project 37 — CogniSync Professional MAX

## Status
Portfolio project. Hackathon-derived foundation upgraded into a production-grade proactive work operating layer.

## Mission
Build a background-first professional agent that continuously converts fragmented work signals into verified decision support while preserving human agency. The target is not maximal autonomy; it is maximal **useful autonomy per unit of risk**.

## Core loop

```text
OBSERVE
  ↓
CONTEXT FUSION
  ↓
INTENT / PRIORITY INFERENCE
  ↓
PLAN
  ↓
PREPARE
  ↓
CONSEQUENCE + POLICY CHECK
  ↓
EXECUTE OR REQUEST APPROVAL
  ↓
AUTHORITATIVE CONFIRMATION
  ↓
AUDIT / LEARN
```

## System architecture

```text
MAIL / CALENDAR / FILES / CHAT / CRM / PROJECT DATA
                     ↓
              EVENT NORMALIZER
                     ↓
               EVIDENCE LEDGER
                     ↓
             CONTEXT COMPILER
                     ↓
             TASK / DECISION GRAPH
                     ↓
              AGENT REASONER
                     ↓
             CAPABILITY BROKER
              ↙      ↓       ↘
          DRAFT    SCHEDULE    ACTION
                     ↓
          POSTCONDITION CHECK
                     ↓
             AUDIT / TRACE
```

## Decision packets

For every material recommendation, produce a compact packet:

```yaml
DecisionPacket:
  objective:
  options:
  recommended_option:
  tradeoffs:
  evidence_refs:
  assumptions:
  uncertainty:
  expected_consequences:
  reversibility:
  approval_required:
```

The agent must distinguish **fact, inference, recommendation and pending action**.

## Proactivity governor

Proactivity is a bounded resource:

```yaml
ProactivityPolicy:
  urgency_threshold:
  interruption_budget:
  notification_budget:
  confidence_threshold:
  consequence_threshold:
  quiet_hours:
  escalation_policy:
```

The system optimizes interruption quality rather than message volume.

## Memory architecture

Separate:

`ephemeral_context → working memory → durable user memory → organizational knowledge → audit ledger`

Memory writes require provenance and policy evaluation. The model cannot promote arbitrary conversational content into trusted durable memory.

## Capability contract

```yaml
Capability:
  id:
  version:
  inputs:
  outputs:
  side_effects:
  authorization:
  reversibility:
  quota:
  cost_model:
  verification:
  provenance:
```

## Consequence-aware execution

```text
LOW CONSEQUENCE
→ auto-execute when reversible + policy-safe

MEDIUM CONSEQUENCE
→ prepare + summarize + approval or bounded rule

HIGH / IRREVERSIBLE
→ explicit approval + execution + confirmation
```

## Evidence and grounding

All important conclusions retain source references, timestamps and freshness. Conflicting evidence is surfaced rather than silently averaged.

## Adaptive model routing

CogniSync delegates by task profile rather than brand:

`fast classification → low-cost model`
`complex synthesis → reasoning model`
`vision/audio → multimodal specialist`
`private work → local/edge model when policy permits`
`high-consequence output → verifier / multi-model check`

## Failure and recovery

Failure classes:

- stale context;
- connector outage;
- authorization denial;
- ambiguous intent;
- tool failure;
- postcondition failure;
- duplicate side effect;
- budget exhaustion;
- evaluator disagreement.

Each class has an explicit retry, compensate, escalate or stop policy.

## Observability

Every run correlates:

`session_id + turn_id + model_id + capability_id + policy_version + evidence_refs + artifact_id + latency + cost + final_state_version`

## Security invariants

1. Model output is never authorization.
2. Secrets remain outside model context whenever possible.
3. External completion is reported only after connector confirmation.
4. Stale turns cannot overwrite newer state.
5. Unknown side effects fail closed.
6. Durable memory requires provenance.
7. User intent, authorization and capability remain separate.

## Evaluation

### Productivity
- time saved per approved outcome;
- unnecessary interruption rate;
- decision latency reduction;
- completion reliability.

### Quality
- recommendation precision;
- evidence coverage;
- stale-context rate;
- hallucination/unsupported-claim rate.

### Safety
- unauthorized-action rate;
- duplicate-side-effect rate;
- secret-exposure rate;
- policy-bypass rate;
- approval-skipping rate.

### Economics
- cost per successful workflow;
- human minutes saved;
- connector invocation efficiency.

## Roadmap

### Phase 1 — verified assistant
Daily brief, blockers, drafts, decision packets and audit trail.

### Phase 2 — governed action
MCP/API connectors, durable memory, notifications, confirmation semantics.

### Phase 3 — adaptive specialist network
Bounded specialist agents, model routing, multi-model verification.

### Phase 4 — vertical operating packs
Creative professionals, consultants, small teams and other knowledge-work verticals.

## Definition of Done

CogniSync is complete when proactive behavior, capability execution, evidence, memory, approval and audit operate as one reproducible control loop, with measurable utility and measurable restraint.
