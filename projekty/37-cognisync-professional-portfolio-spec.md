# Project 37 — CogniSync Professional MAX

## Status
Portfolio project. Hackathon-derived foundation upgraded into a production-grade proactive work operating layer.

## Mission
Build a background-first professional agent that continuously converts fragmented work signals into **verified decision support and bounded action**, preserving human judgment where consequences are material.

The objective is not maximal autonomy. It is:

`MAX useful autonomy per unit of risk`

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

## 1. Work Graph

Work is represented as structured state instead of only a chat transcript:

```yaml
WorkNode:
  id:
  type: task|decision|meeting|message|document|deadline|risk|blocker|artifact
  source:
  owner:
  timestamp:
  status:
  priority:
  provenance:

WorkEdge:
  from:
  to:
  relation: blocks|depends_on|derived_from|contradicts|resolves|mentioned_in
  confidence:
  provenance:
```

This lets the agent reason over dependencies, deadlines and consequences while preserving source lineage.

## 2. Decision packets

For every material recommendation:

```yaml
DecisionPacket:
  objective:
  current_state:
  options:
  recommended_option:
  tradeoffs:
  evidence_refs:
  assumptions:
  uncertainty:
  expected_consequences:
  reversibility:
  approval_required:
  next_verification:
```

The agent must distinguish **fact, inference, recommendation, prepared action and verified outcome**.

## 3. Proactivity Governor

Proactivity is a bounded resource:

```yaml
ProactivityPolicy:
  urgency_threshold:
  confidence_threshold:
  consequence_threshold:
  interruption_budget:
  notification_budget:
  quiet_hours:
  batching_policy:
  escalation_policy:
```

Decision function:

`value × confidence × urgency × consequence × reversibility − interruption_cost`

The system optimizes interruption quality, not message volume.

## 4. Memory architecture

```text
EPHEMERAL CONTEXT
       ↓
WORKING MEMORY
       ↓
DURABLE USER MEMORY
       ↓
ORGANIZATIONAL KNOWLEDGE
       ↓
AUDIT / PROVENANCE LEDGER
```

Durable writes require provenance, scope and policy evaluation. Arbitrary model output cannot silently become trusted memory.

## 5. Evidence / grounding

Every important conclusion retains:

`source → observation → inference → recommendation`

with:

`timestamp + freshness + confidence + provenance`.

Conflicting evidence is surfaced rather than silently averaged.

## 6. Capability contract

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

Capability is not authorization. The Capability Broker remains the only gateway to consequential external effects.

## 7. Consequence-aware execution

```text
LOW CONSEQUENCE
→ auto-execute only when reversible + policy-safe

MEDIUM CONSEQUENCE
→ prepare + summarize + bounded approval/rule

HIGH / IRREVERSIBLE
→ explicit approval + execution + authoritative confirmation
```

Completion is never inferred only from a connector response; the system reads back authoritative state and verifies the postcondition.

## 8. Adaptive model routing

Routing is task-driven:

```text
FAST CLASSIFICATION
      ↓
LOW-COST WORKER
      ↓ uncertainty / complexity
STRONGER REASONER
      ↓ disagreement / consequence
MULTI-SOLVER / VERIFIER
      ↓ unresolved high consequence
HUMAN DECISION GATE
```

Profile dimensions:

`quality + latency + privacy + cost + consequence + capability + freshness`.

## 9. Professional workflow packs

Initial vertical packs:

- creative professional;
- consultant;
- project delivery;
- research coordination;
- small business/team.

Each pack is a versioned Skill with explicit capabilities, provenance and evaluation criteria.

## 10. Grand-Challenge bridge

CogniSync is the human-facing operational layer for Project 48:

```text
GRAND CHALLENGE / BUSINESS PROBLEM
          ↓
RESEARCH / EVIDENCE
          ↓
DECISION PACKET
          ↓
EXPERIMENT / ACTION PLAN
          ↓
TEAM COORDINATION
          ↓
MEASURED RESULT
```

It converts research into bounded organizational work without claiming that unresolved science has been solved.

## 11. Influence and agency protection

The agent does not optimize user behavior through hidden pressure. Recommendations expose assumptions, trade-offs, reversibility and alternatives.

Integration:

```text
RECOMMENDATION
      ↓
AGENCY CHECK
      ↓
DISCLOSURE / REVERSIBILITY
      ↓
USER DECISION
```

Project 43 supplies defensive influence-risk analysis.

## 12. Notification policy

Notifications are typed:

`INFO | FYI | WARNING | DECISION | ACTION_REQUEST | CRITICAL`

Every class has explicit thresholds and batching rules.

## 13. Stale-turn / stale-state protection

```yaml
Run:
  run_id:
  state_version:
  authority_epoch:
  started_at:
  expires_at:
  status: active|superseded|cancelled|completed|failed
```

A stale run cannot authoritatively overwrite newer state. Before resumption, the agent re-reads current state and revalidates authorization.

## 14. Failure and recovery

Failure classes:

- stale context/state;
- connector outage;
- authorization denial;
- ambiguous intent;
- tool failure;
- postcondition failure;
- duplicate-side-effect risk;
- budget exhaustion;
- evaluator disagreement.

Each maps to:

`RETRY | COMPENSATE | ESCALATE | STOP | REPLAN`.

## 15. Observability

Every run correlates:

```text
session_id
turn_id
model_id
actual_runtime_id
capability_id
policy_version
evidence_refs
artifact_id
state_version
latency
cost
outcome
```

Actual execution identity, not requested aliases, determines metering.

## 16. Evaluation

### Productivity
- time saved per verified outcome;
- decision latency reduction;
- blocker detection precision;
- unnecessary interruption rate.

### Quality / epistemics
- recommendation precision;
- evidence coverage;
- stale-context rate;
- unsupported-claim rate;
- contradiction surfacing.

### Safety
- unauthorized-action rate;
- duplicate-side-effect rate;
- secret-exposure rate;
- approval-skipping rate;
- policy-bypass rate.

### Economics
- cost per successful workflow;
- human review minutes per outcome;
- connector efficiency;
- cloud escalation ratio.

## 17. Definition of Done

- work graph;
- evidence/provenance ledger;
- decision packets;
- proactivity governor;
- durable checkpointed state;
- capability-brokered connectors;
- authoritative outcome confirmation;
- stale-turn protection;
- adaptive routing;
- notification policy;
- agency/influence guard;
- versioned workflow packs;
- grand-challenge integration;
- measurable utility, safety and cost evaluation.

## Position in portfolio

Project 37 is the human-facing professional operating layer above the evidence, reasoning, trust, routing, sovereign-runtime and grand-challenge subsystems. It converts them into bounded professional workflows while preserving human control over consequential decisions.
