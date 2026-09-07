# Project 38 — Sovereign Edge AI MAX

## Status
Architecture-ready sovereign execution program. This artifact is the canonical Project 38 specification. Historical duplicate Project 38 variants are retained only as archived lineage artifacts.

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

`T0 deterministic → T1 local CPU/GPU → T2 desktop/browser edge → T3 mobile/on-prem edge → T4 cloud specialist`

Escalation is driven by measurable capability gaps, not by default provider preference.

## Inference contract

Every backend implements:

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

Provider-specific model IDs remain below this interface.

## Hardware-aware planner

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

The planner computes feasible profiles before execution and may reduce context, quantization, concurrency or model size before escalating.

## Quantization / offloading benchmark program

The supplied corpus describes GGUF quantization, CPU/GPU offloading and practical context ranges for constrained machines; these are hypotheses to benchmark, not universal guarantees. fileciteturn69file6L258-L289

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

Multi-drive aggregation may be used only when source identity, provenance, freshness and authorization survive the abstraction.

## Research mode

For internet-enabled research, use a private search/retrieval layer plus MCP tools. External content is untrusted evidence and carries:

`source + captured_at + content_hash + provenance + freshness + confidence`.

## Verification fabric

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

## Multimodal edge runtime

Text, vision, audio and video are routed to the best available local/edge backend. Multimodal observations remain evidence and never become authorization.

## Privacy-preserving router

```text
DATA CLASS
   ×
PRIVACY
   ×
QUALITY
   ×
LATENCY
   ×
COST
   ×
DEVICE CAPABILITY
   ×
ENERGY
```

`local_only` data cannot automatically enter a cloud route.

## MCP capability boundary

```text
DISCOVER → PROVENANCE → ALLOWLIST → AUTHORIZE → CALL → VALIDATE → AUDIT
```

MCP is an interoperability mechanism, not a trust authority.

## Offline-first resilience

```text
CLOUD UNAVAILABLE
       ↓
EDGE
       ↓
LOCAL
       ↓
DETERMINISTIC FALLBACK
```

Tasks are checkpointed and resumed using validated state rather than blindly replayed.

## Cloud / edge integration

Project 38 can use the edge-to-cloud continuum established by Projects 37 and 39:

```text
LOCAL / EDGE
     ↓ capability gap
AGENT-BROKERED CLOUD ESCALATION
     ↓
SPECIALIST MODEL / GPU / SANDBOX
     ↓
VERIFIED ARTIFACT
     ↓
RETURN TO SOVEREIGN STATE
```

Cloud execution must declare reason, data classes, destination, capability scope, expiry and audit identity.

## Security invariants

1. Local inference does not bypass policy.
2. Open or modified weights do not constitute a safety boundary.
3. Model output never authorizes tool execution.
4. Secrets are excluded from model context whenever possible.
5. Cloud escalation requires explicit data-egress policy.
6. Persistent state is separated from ephemeral context.
7. Tool results require validation before becoming trusted state.
8. Browser/device state is untrusted until authoritative readback.
9. Edge and local runtimes are execution substrates, not policy authorities.
10. Adaptive optimization may not reduce mandatory safety controls.

## Evaluation program

### Quality
- task success;
- factuality/evidence coverage;
- structured-output validity;
- model-routing regret against an oracle benchmark.

### Performance
- TTFT;
- tokens/s;
- p50/p95 latency;
- RAM/VRAM;
- thermal throttling;
- recovery time.

### Sovereignty
- cloud data-egress rate;
- local-only policy violations;
- percentage of tasks completed without cloud;
- provenance completeness.

### Economics / energy
- cost per successful task;
- Wh per successful task;
- cloud escalation cost;
- model storage overhead.

### Security
- unauthorized capability rate;
- injection acceptance rate;
- stale-state overwrite rate;
- secret-exposure rate;
- fallback correctness.

## Definition of Done

- provider-neutral inference contract;
- hardware-aware capability probe;
- quantization/offload benchmark harness;
- sovereign local data plane;
- private research mode;
- MCP capability boundary;
- multimodal wrappers;
- verification gate;
- offline checkpoint/resume;
- cloud-egress policy;
- edge-to-cloud adapter;
- security/evaluation suite;
- reproducible deployment profile.

## Position in portfolio

Project 38 is the sovereign execution substrate beneath Projects 17, 21, 37, 39, 40, 41 and 48. Its purpose is not to eliminate cloud usage categorically, but to make **where inference happens a measurable, policy-controlled decision**.
