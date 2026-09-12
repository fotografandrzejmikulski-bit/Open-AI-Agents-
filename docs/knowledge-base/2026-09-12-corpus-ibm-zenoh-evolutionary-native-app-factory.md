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

The supplied latency values and protocol-overhead figures remain source claims until measured in the target IBM Cloud topology. P2P/UDP/SHM paths also require explicit trust, routing, encryption and failure-domain design.

### 2. MCP gateway boundary

MCP should expose typed capabilities rather than become an authorization authority. A gateway translating MCP requests into Zenoh queries must preserve caller identity, request identity, capability scope, policy decision, idempotency information and provenance across the translation boundary.

```text
MCP REQUEST
↓
AUTHENTICATE
↓
SCHEMA / CAPABILITY CHECK
↓
POLICY DECISION
↓
ZENOH MESSAGE
↓
EXECUTOR
↓
READBACK
```

`MCP ≠ AUTHORIZATION`

`ZENOH ≠ AUTHORIZATION`

### 3. Hierarchical / holographic memory

The proposed SHIMI hierarchy complements the existing memory substrate. Retrieval remains an observation mechanism; similarity is not calibrated certainty. Memory records require provenance, temporal validity and conflict handling before becoming decision inputs.

The expanded corpus adds three useful memory distinctions:

- **Episodic** — build attempts, emulator failures, repair trajectories and iteration history;
- **Semantic** — native APIs, platform architecture and validated design patterns;
- **Procedural** — build scripts, toolchain procedures and validated scaffolds.

A bitemporal record can be represented conceptually as:

`E(u,v) = {(prop,val,[VTstart,VTend],[STstart,STend])}`

where valid time describes when a fact/rule is applicable and system/transaction time describes when the record entered the system. This is useful for regression analysis, dependency history and historical reconstruction, but does not itself establish factual correctness.

### 4. HRR / vector-symbolic layer

The proposed Holographic Reduced Representation layer is a candidate symbolic-compression mechanism for nested UI/component relationships. Circular convolution can bind representations in fixed-dimensional vectors, with FFT-based implementation reducing convolution cost asymptotically to `O(d log d)` under the stated formulation.

This should be treated as an indexing/representation primitive, not as a substitute for provenance, exact source retrieval or deterministic reconstruction. HRR similarity is likewise an observation signal, not authorization or calibrated truth.

### 5. Merkle-DAG / Bloom / CRDT synchronization

The combination can form a useful synchronization stack:

```text
SOURCE / STATE
↓
CONTENT DIGEST
↓
MERKLE-DAG LINEAGE
↓
BLOOM FILTER — candidate membership check
↓
CRDT — conflict-tolerant merge
↓
EXACT READBACK / VERIFICATION
```

Bloom filters remain probabilistic membership structures and therefore require exact verification after candidate discovery. CRDT convergence does not guarantee semantic correctness; merge policy and invariants remain necessary.

### 6. DGM / RSI for native tooling

The digital-genotype concept is useful for versioned scaffolds, build adapters and evaluator configurations. Promotion must remain gated by reproducible builds, regression tests, security analysis, policy checks, artifact identity and rollback capability.

```text
BASELINE
↓
MUTATION CANDIDATE
↓
STATIC / SECURITY ANALYSIS
↓
ISOLATED BUILD
↓
RUNTIME TEST
↓
ADVERSARIAL EVALUATION
↓
POLICY GATE
↓
APPROVAL WHEN REQUIRED
↓
PROMOTION
↓
READBACK
↓
ROLLBACK ON FAILED POSTCONDITION
```

`SELF-IMPROVEMENT ≠ SELF-AUTHORIZATION`

### 7. Native build factory

The corpus materially strengthens the existing native/game build-factory model by introducing a common multi-platform abstraction for Swift, Kotlin, Rust/Tauri and related toolchains. Platform-specific signing, SDK licensing, emulator availability and host constraints remain explicit build capabilities rather than assumed universal properties.

The important architectural split is between **source-generation capability** and **platform execution capability**. iOS/macOS builds, Android builds and Windows/Linux builds have different host, SDK, signing and runtime requirements and must not be collapsed into one generic "cross-compile" assumption.

### 8. Objective-hacking resistance

The proposed OESI/SEGPA/PNSA layers reinforce an existing principle: an evaluator must obtain independent evidence. Generated code must not control the evaluator's evidence path, fabricate logs, alter test results or silently redefine the fitness function.

`BUILD SUCCESS ≠ RUNTIME SUCCESS`

`RUNTIME SUCCESS ≠ SECURITY`

`FITNESS SCORE ≠ INTELLIGENCE`

### 9. HSM signing boundary

Cryptographic signing establishes artifact integrity/authenticity relative to the signing authority. It does not prove that the artifact is safe, correct or aligned. Signing therefore follows verification rather than replacing it.

### 10. Cloud separation

The architecture should distinguish control plane, build plane, evaluation plane, artifact plane and production plane. Build/evaluation workloads require least privilege, egress controls, ephemeral isolation and explicit promotion gates.

### 11. Cognitive modulation

The supplied design proposes adapting model sampling parameters to task criticality. This can be retained as an orchestration policy concept, but lower temperature does not guarantee deterministic behavior. Critical code paths should instead rely on constrained generation, reproducible toolchains, fixed inputs where required, independent tests and verification evidence.

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
- TTT/R3Titans claims require empirical validation and a safe parameter-update boundary;
- dynamic code injection into generated native projects must be capability-scoped and independently verified;
- a memory merge must not silently overwrite newer state or erase provenance;
- bitemporal storage provides temporal reconstruction, not truth certification.

## Integration decision

No new standalone project is required. The corpus is a cross-cutting architecture extension to P100, P86, P119 and P121, with strongest impact on autonomous software engineering, native build/evaluation, memory verification and RSI governance.
