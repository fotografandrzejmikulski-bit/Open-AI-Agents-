# 04 — AI-NATIVE OPERATING SYSTEM

## Status
**Engineering Specification Baseline — Runtime Research Track**

## Mission
Prototype the practical portion of the Cognitive Stack thesis as a controlled runtime architecture in which learned components optimize scheduling, adapter generation and multimodal interaction while deterministic runtime primitives remain authoritative.

## Core invariant
**AI proposes; deterministic runtime decides.**

No learned model, generated adapter or perceptual interface may directly grant itself kernel, device, credential, deployment or persistence authority.

## Runtime constitution

System lifecycle:

`INITIALIZING → ACTIVE → DEGRADED → MAINTENANCE → EMERGENCY`

Each transition is governed by deterministic predicates, watchdogs and explicit recovery actions.

```text
AI / ML proposals
       ↓
policy + capability gate
       ↓
deterministic runtime controller
       ↓
authoritative state transition
       ↓
telemetry / audit
```

A model explanation is never considered evidence that a transition is safe.

## Planes

```text
CONTROL PLANE
  policy · scheduler · lifecycle · admission

EXECUTION PLANE
  processes · services · drivers · device adapters

DATA PLANE
  telemetry · artifacts · SemanticFS references

INTERACTION PLANE
  text · speech · vision · accessibility · PUI
```

## 1. Neural Process Scheduling

### Inputs
- CPU/GPU utilization;
- queue depth;
- memory pressure;
- latency target;
- process class/priority;
- I/O wait;
- power/thermal state;
- historical scheduler outcomes.

### Control loop

```text
telemetry
→ feature window
→ model proposal
→ policy filter
→ deterministic scheduler
→ authoritative observation
→ feedback/eval
```

The model emits a bounded recommendation, not an executable scheduler operation.

```ts
type SchedulingProposal = {
  proposalId: string;
  modelVersion: string;
  targetProcess: string;
  recommendedClass: string;
  priorityDelta: number;
  confidence: number;
  featureHash: string;
};
```

### Hard constraints

The policy gate must reject proposals causing:

- starvation beyond configured bounds;
- unauthorized priority escalation;
- resource quota violation;
- thermal envelope violation;
- fairness degradation beyond threshold;
- unsafe process isolation changes.

## 2. AI Foundry adapter pipeline

Generated adapters are ordinary untrusted artifacts until verified.

```text
hardware specification
→ capability schema
→ generated adapter candidate
→ compile/static analysis
→ interface/contract tests
→ sandbox execution
→ benchmark
→ signature/provenance record
→ registry
→ explicit promotion
```

### Stable device interface

```ts
interface DeviceAdapter {
  manifest(): CapabilityManifest;
  probe(): Promise<DeviceHealth>;
  prepare(op: DeviceOperation): Promise<PreparedOperation>;
  execute(op: PreparedOperation): Promise<DeviceResult>;
  cancel(op: PreparedOperation): Promise<CancelReceipt>;
  rollback?(checkpoint: CheckpointRef): Promise<RollbackReceipt>;
}
```

Generated code cannot be promoted solely because compilation succeeds. Promotion requires test evidence and a reproducible artifact hash.

## 3. Perceptual User Interface

PUI normalizes heterogeneous signals into explicit intents.

```ts
type Intent = {
  intentId: string;
  action: string;
  target?: string;
  confidence?: number;
  evidenceRefs: string[];
  source: 'text' | 'voice' | 'vision' | 'gesture' | 'accessibility';
};
```

PUI must preserve uncertainty. A low-confidence recognition must not silently become a destructive action.

High-impact intents require additional confirmation and capability authorization.

## 4. Authorization boundary

Authorization considers:

`actor + intent + capability + target resource + runtime state + policy version + risk`.

Semantic similarity, model confidence and user-interface recognition are not authorization primitives.

## 5. Learned component lifecycle

Every learned component follows:

`PROPOSED → VALIDATED → CANARY → ACTIVE → DEGRADED/QUARANTINED → RETIRED`.

Required metadata:

- model/component version;
- training/evaluation dataset reference;
- policy version;
- artifact checksum;
- performance baseline;
- known limitations;
- rollback target.

## 6. Failure containment

```text
DETECT
  ↓
ISOLATE COMPONENT
  ↓
SNAPSHOT / CHECKPOINT
  ↓
RESTORE LAST VERIFIED STATE
  ↓
DETERMINISTIC HEALTH CHECK
  ↓
TEST
  ↓
STAGED REACTIVATION
```

Recovery must not depend on the failing model cooperating or generating a correct repair.

## 7. SemanticFS boundary

`semantic retrieval != authorization`.

Semantic retrieval may produce candidate resources; authorization independently evaluates whether a resource can be read, modified, executed or exported.

## 8. Resource governance

The runtime requires bounded budgets for:

- CPU;
- GPU;
- memory;
- I/O;
- network egress;
- energy where measurable;
- model inference count;
- scheduler overhead.

A learned policy cannot increase its own budget.

## 9. Reliability requirements

The MVP must define and measure SLOs for:

- scheduling decision latency;
- p95/p99 process latency;
- control-loop overhead;
- recovery time;
- false intervention rate;
- fairness deviation;
- dropped/failed control events;
- PUI intent error rates.

Mean throughput alone is insufficient for acceptance.

## 10. Security

- least-privilege model/runtime identities;
- no production credentials in training or benchmark fixtures;
- restricted egress for generated components;
- kernel boundary protected from model-controlled code;
- signed/versioned promoted artifacts;
- tamper-evident audit records;
- explicit data-residency controls for telemetry;
- adversarial testing of PUI and model-controlled inputs.

## 11. Observability

Every model-driven proposal and consequential decision records:

`proposalId · modelVersion · policyVersion · featureHash · runtimeState · decision · reasonCodes · resultingState`.

Telemetry must separately distinguish:

- model proposal quality;
- policy rejection;
- deterministic execution result;
- post-action outcome.

This prevents success attribution to the model when the actual safety boundary was the deterministic controller.

## 12. Test strategy

### Unit
State machine, policy predicates, scheduler constraints, capability checks, PUI normalization and rollback logic.

### Property-based
- forbidden transitions never occur;
- policy gates never authorize out-of-budget actions;
- recovery converges to a known safe state;
- repeated identical inputs do not create nondeterministic authorization results.

### Integration
Telemetry → model proposal → policy gate → scheduler/runtime → telemetry.

### Performance
Compare static baseline vs AI-assisted policy using versioned workloads and confidence intervals for measured deltas.

### Chaos / fault injection
Inject stale telemetry, model timeout, corrupted model artifact, runaway process, thermal pressure, device loss and transport delay.

### Security
Prompt/model injection, capability confusion, malicious adapter artifact, untrusted telemetry and PUI spoofing.

## 13. MVP delivery sequence

1. Linux user-space telemetry collector.
2. Synthetic workload generator.
3. Scheduler recommender.
4. Deterministic policy gate.
5. Checkpoint/rollback mechanism.
6. Trace and audit recorder.
7. Benchmark harness.
8. Dashboard comparing baseline vs AI-assisted scheduling.
9. Generated-adapter sandbox prototype.
10. PUI intent schema and authorization adapter.

Kernel changes remain a later research step after the user-space control loop demonstrates measurable benefit without compromising safety.

## 14. Definition of Done

**Implementation Ready** requires executable contracts for scheduling proposals, lifecycle states, device adapters, intents, resource budgets, authorization, rollback and telemetry. Advancement toward production requires reproducible benchmark evidence, fault-injection results, security review, operational runbooks and independently verified deployment behavior.

## Long-term integration

The project may integrate with the repository's substrate abstraction, verification/security fabric and runtime assurance projects through typed contracts. It must not duplicate portfolio governance or replace higher-level agent orchestration.
