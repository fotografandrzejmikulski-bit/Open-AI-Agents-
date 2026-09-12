# Knowledge Base — IBM Cloud Zenoh / DGM / RSI Native App Factory

## Intake

Date: 2026-09-12
Source: user-supplied architecture corpus describing an E2E autonomous evolutionary agent system on IBM Cloud for native desktop/mobile application generation.

## Scope

The corpus proposes a cloud control plane combining IBM Cloud Code Engine, VPC/GPU infrastructure, Zenoh transport, hierarchical memory, DGM/RSI evolution, JEPA/world-model concepts, MCP, sandboxed native builds, adversarial gating and HSM-backed artifact signing.

This is source-derived architecture material. Vendor-specific limits, exact latency figures, pricing, product availability, SDK versions and claimed performance are treated as claims requiring independent verification before production use.

## Architectural synthesis

```text
CHATGPT / MCP INTENT
↓
CAPABILITY + POLICY RESOLUTION
↓
TASK DAG
↓
MEMORY / RETRIEVAL
↓
ZENOH TRANSPORT
↓
NATIVE BUILD / TEST SANDBOX
↓
READBACK + ADVERSARIAL EVALUATION
↓
ARTIFACT DIGEST + SIGNING
↓
POSTCONDITION VERIFICATION
↓
PROMOTION / ROLLBACK
↓
PROVENANCE + MEMORY
```

## Important additions

### 1. Zenoh as transport, not authority

Zenoh can be modeled as a low-latency message/data plane between agent components. Transport success does not authorize an operation and does not establish the truth of a payload.

`TRANSPORT ≠ AUTHORIZATION`

`MESSAGE ≠ TRUSTED INSTRUCTION`

`LOW LATENCY ≠ SAFETY`

### 2. Hierarchical/holographic memory

The proposed SHIMI hierarchy complements the existing memory substrate. Retrieval remains an observation mechanism; similarity is not calibrated certainty. Memory records require provenance, temporal validity and conflict handling before becoming decision inputs.

### 3. DGM / RSI for native tooling

The digital-genotype concept is useful for versioned scaffolds, build adapters and evaluator configurations. Promotion must remain gated by reproducible builds, regression tests, security analysis, policy checks, artifact identity and rollback capability.

`SELF-IMPROVEMENT ≠ SELF-AUTHORIZATION`

### 4. Native build factory

The corpus materially strengthens the existing native/game build-factory model by introducing a common multi-platform abstraction for Swift, Kotlin, Rust/Tauri and related toolchains. Platform-specific signing, SDK licensing, emulator availability and host constraints remain explicit build capabilities rather than assumed universal properties.

### 5. Objective-hacking resistance

The proposed OESI/SEGPA/PNSA layers reinforce an existing principle: an evaluator must obtain independent evidence. Generated code must not control the evaluator's evidence path, fabricate logs, alter test results or silently redefine the fitness function.

`BUILD SUCCESS ≠ RUNTIME SUCCESS`

`RUNTIME SUCCESS ≠ SECURITY`

`FITNESS SCORE ≠ INTELLIGENCE`

### 6. HSM signing boundary

Cryptographic signing establishes artifact integrity/authenticity relative to the signing authority. It does not prove that the artifact is safe, correct or aligned. Signing therefore follows verification rather than replacing it.

### 7. Cloud separation

The architecture should distinguish control plane, build plane, evaluation plane, artifact plane and production plane. Build/evaluation workloads require least privilege, egress controls, ephemeral isolation and explicit promotion gates.

## Source-code audit observations

The supplied Python/Rust snippets are architectural PoCs, not production-ready implementations.

Observed risks include:

- placeholder API credentials must never be used as defaults;
- random embeddings do not constitute a semantic memory index;
- AST parsing/compilation alone is insufficient adversarial gating;
- checking a few forbidden substrings is insufficient code-safety analysis;
- `pass` inside an import restriction loop does not block imports;
- a model-generated mutation must be treated as untrusted executable input;
- Zenoh multicast/scouting requires an explicit network trust model;
- `unwrap()` in infrastructure/runtime paths requires controlled error handling;
- simulated build success must never be presented as actual artifact verification;
- direct model output must not become an executable deployment instruction without policy and authorization;
- temperature settings do not guarantee deterministic generation;
- TTT/R3Titans claims require empirical validation and a safe parameter-update boundary.

## Integration decision

No new standalone project is required. The corpus is a cross-cutting architecture extension to P100, P86, P119 and P121, with strongest impact on autonomous software engineering, native build/evaluation and RSI governance.
