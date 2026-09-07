# Project 38 — Sovereign Edge AI MAX

## Status
Architecture-ready sovereign execution program. This artifact consolidates the duplicate Project 38 edge-AI concepts into one canonical architecture. The redundant earlier variants remain preserved only for history; this file is the canonical Project 38 specification.

## Thesis
Build a provider-independent, local-first AI runtime that can operate under constrained hardware, imperfect connectivity and strict data-sovereignty requirements while retaining a controlled escalation path to edge and cloud resources.

## Canonical architecture

```text
                    OMNICORE CONTROL PLANE
                            ↓
                 MODEL-NEUTRAL CONTRACT
                            ↓
        ┌───────────────────┼───────────────────┐
        ↓                   ↓                   ↓
   DETERMINISTIC       LOCAL INFERENCE      EDGE INFERENCE
        ↓                   ↓                   ↓
      POLICY         MCP / CAPABILITIES      DEVICE APIs
        └───────────────────┼───────────────────┘
                            ↓
                     VERIFICATION GATE
                            ↓
                   OPTIONAL CLOUD ESCALATION
                            ↓
                   AUTHORITATIVE AUDIT
```

## Execution tiers

`T0 deterministic`

Schema validation, parsing, rules, caching and bounded local functions.

`T1 local CPU/GPU`

Quantized open-weight inference on owned hardware.

`T2 desktop/browser edge`

Local application/browser AI where supported, behind a capability wrapper.

`T3 mobile/on-prem edge`

Device NPU/GPU/CPU inference and private enterprise edge nodes.

`T4 cloud specialist`

Only when local/edge quality, latency, modality or capability requirements are not met and policy permits data egress.

## Inference contract

Every backend implements a common interface:

```text
capabilities()
health()
create_session()
generate()
stream()
structured_output()
tool_call()
usage()
cancel()
```

Provider-specific model IDs remain below the contract.

## Hardware-aware planner

Instead of guessing whether a device can run a model, the runtime probes:

```yaml
DeviceProfile:
  cpu:
  ram_gb:
  gpu:
  vram_gb:
  npu:
  storage_free_gb:
  thermal_state:
  battery_state:
  network_class:
  privacy_policy:
```

The planner computes a feasible execution profile and can reduce context, quantization level, concurrency or model size before falling back.

## Quantization and offloading

The supplied corpus describes GGUF quantization, CPU/GPU offloading and practical context ranges for constrained machines. These are treated as benchmark hypotheses rather than universal guarantees. fileciteturn69file6L258-L289

Benchmark matrix:

| Variable | Measurements |
|---|---|
| Quantization | quality / memory / throughput |
| Offload | CPU %, GPU %, latency |
| Context | usable length / degradation |
| Batch | throughput / thermal impact |
| Concurrency | p50/p95 / OOM rate |
| Power | Wh / successful task |

## Sovereign data plane

```text
LOCAL FILES
   ↓
CONTENT CLASSIFICATION
   ↓
LOCAL INDEX / VECTOR / EVIDENCE STORE
   ↓
MCP CAPABILITIES
   ↓
POLICY
```

Rclone-like multi-drive aggregation may be used, but the abstraction must preserve source identity, path provenance, freshness and authorization.

## Research stack

For internet-enabled research, the local stack may use a private search/retrieval layer plus MCP tools. External content is untrusted evidence and must carry:

`source + captured_at + content_hash + provenance + freshness + confidence`.

## Verification fabric

Generated code and consequential outputs pass through:

```text
GENERATE
 ↓
PARSE / TYPE CHECK
 ↓
STATIC ANALYSIS
 ↓
TEST / SANDBOX
 ↓
DOMAIN CONSTRAINTS
 ↓
POSTCONDITION / INVARIANT CHECK
 ↓
APPROVE / REJECT
```

## Multimodal extension

The runtime can route text, vision, audio and video requests to the best available local/edge backend. Multimodal observations remain evidence, never authorization.

## Privacy-preserving routing

The router evaluates:

`data_class × privacy_level × task_quality × latency × cost × device_capability × energy`

No automatic cloud export is allowed for data classes marked `local_only`.

## MCP boundary

MCP tools are capability primitives, not trust primitives:

```text
DISCOVER
 ↓
PROVENANCE
 ↓
ALLOWLIST
 ↓
AUTHORIZE
 ↓
CALL
 ↓
VALIDATE
 ↓
AUDIT
```

## Reliability

Offline-first operation must survive temporary network loss:

```text
CLOUD UNAVAILABLE
       ↓
EDGE
       ↓
LOCAL
       ↓
DETERMINISTIC FALLBACK
```

Tasks are checkpointed and resumable rather than replayed blindly.

## Security invariants

1. Local inference does not bypass policy.
2. Open or modified model weights do not constitute a safety boundary.
3. Model output never authorizes tool execution.
4. Secrets are excluded from model context whenever possible.
5. Cloud escalation requires an explicit egress decision.
6. Persistent state is separated from ephemeral context.
7. Tool results require validation before becoming trusted state.

## Evaluation program

### Quality
- task success;
- factuality/evidence coverage;
- structured-output validity.

### Performance
- TTFT;
- tokens/s;
- p50/p95 latency;
- peak RAM/VRAM;
- thermal throttling.

### Economics
- cost/task;
- Wh/task;
- local execution ratio;
- cloud escalation rate.

### Security
- policy violation rate;
- unauthorized tool-call rate;
- data-egress violations;
- secret exposure rate;
- recovery success rate.

## Roadmap

1. Reproducible local runner.
2. MCP capability fabric.
3. Hardware benchmark harness.
4. Verification and sandbox loop.
5. Multimodal edge adapters.
6. Adaptive local/edge/cloud routing.
7. Sovereign enterprise deployment profile.

## Definition of Done

Project 38 is complete when the same agent contract can execute locally, on edge hardware and through controlled cloud fallback without rewriting application logic, while privacy, provenance, verification and authorization remain invariant.
