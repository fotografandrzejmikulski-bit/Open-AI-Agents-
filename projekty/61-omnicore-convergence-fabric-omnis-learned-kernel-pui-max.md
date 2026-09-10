# Project 61 — OmniCore Convergence Fabric: Omnis + Learned Kernel + Personified Interface MAX

## Status
Research/architecture integration project derived from supplied source materials. This project is an original synthesis, not a claim that the described OS/language exists as a production system.

## Objective
Unify three previously fragmented research lines into one engineered stack:

1. **Omnis** — hybrid systems/application language and compiler architecture.
2. **OmniCore** — AI-native operating-system/runtime research.
3. **Personified UI / Digital Human** — multimodal first-person interface and edge interaction layer.

The design extends the existing portfolio with explicit compilation, state, authorization and verification boundaries.

## Converged architecture

```text
USER / OPERATOR
      │
      ▼
PERSONIFIED UI / VOICE / VISION
      │
      ▼
INTENT + CONTEXT COMPILER
      │
      ├── semantic/evidence state
      ├── repository/dependency graph
      ├── device/world state
      └── persona/presentation state
      │
      ▼
OMNIS FRONTEND + CIRA
      ▼
IR / MLIR / WASM / NATIVE TARGET
      ▼
OMNICORE RUNTIME
      │
      ├── deterministic kernel primitives
      ├── bounded learned scheduling
      ├── isolated services/drivers
      ├── HAL + DBT
      └── MeshBus / device federation
      ▼
CAPABILITY BROKER + POLICY
      ▼
SANDBOXED EXECUTION
      ▼
AUTHORITATIVE READBACK
      ▼
POSTCONDITION / SECURITY / AGENCY VERIFICATION
      ▼
SIGNED ARTIFACT / RELEASE / OBSERVABILITY
```

## Original engineering contributions

### A. State separation fabric
The system must distinguish authoritative state, observed state, retrieval state, model proposal, execution state and presentation state. No model-generated object may silently become authoritative system state.

### B. Dual compiler/runtime contract
Omnis compiles user intent into inspectable artifacts. CIRA operates as a refactoring/modernization subsystem. OmniCore executes only artifacts that have passed deterministic gates.

### C. Learned-kernel containment
Model = bounded optimizer/proposal engine; deterministic scheduler constraints = safety authority; fairness/starvation/priority ceilings/watchdogs = mandatory. Biometric signals are optional UX/accessibility evidence only; no sensitive signal can grant capability or permission.

### D. SemanticFS as two-plane architecture
`QUERY → SEMANTIC CANDIDATES → PROVENANCE/ACL/CAPABILITY CHECK → READ/MUTATE`.

Embedding similarity never means permission.

### E. Driver synthesis pipeline
`DEVICE ENUMERATION → AUTHORITATIVE DATASHEET → STRUCTURED REGISTER MODEL → CODE GENERATION → TYPE/EFFECT CHECK → STATIC ANALYSIS → SANDBOX/HIL → SIGN → STAGED ENABLEMENT → HEALTH READBACK`.

### F. Immutable self-repair
`DETECT → ISOLATE → SNAPSHOT → GENERATE → VERIFY → TEST → SIGN → ACTIVATE → VERIFY → ROLLBACK`.

### G. Personified interface contract
The Digital Human is a presentation and interaction layer. Persona modifies presentation and interaction policy but never capability authorization.

### H. Edge-first presence
The source material emphasizes on-device/edge inference, low latency, local RAG and multimodal synchronization. Project 61 measures the complete pipeline rather than assuming model-token speed equals conversational responsiveness.

## Omnis language specification extracted from the sources
- affine ownership / RAII kernel domain;
- ORC shared-object domain;
- isolated tracing-GC domain;
- reified generics;
- sound gradual typing;
- explicit nullable types;
- significant whitespace;
- inline multi-line blocks;
- exhaustive pattern matching;
- structured concurrency;
- actor-style mutable state isolation;
- MLIR-based heterogeneous lowering;
- proposed quantum-classical execution types as research direction only.

## UGR — Universal Graph Registry
UGR normalizes package metadata from multiple ecosystems and builds a unified dependency graph with provenance, compatibility constraints, SBOM, vulnerability scanning, capability sandboxing, license/compliance checks and reproducible lock/resolution state.

## CIRA — Compiler-Integrated Refactoring Agent
`SOURCE → AST → CFG/DFG/SEMANTIC GRAPH → MIGRATION PLAN → GENERATED TARGET → BUILD → TEST → EQUIVALENCE/INVARIANT EVIDENCE → SECURITY REVIEW → PROMOTION`.

Formal verification is evidence-producing, not magical. Where equivalence cannot be proved, migration remains non-authoritative.

## PUI / Digital Human safety architecture
Affective and behavioral adaptation is allowed only for transparent UX/accessibility scenarios. The system must expose what signals are observed, what adaptations are enabled, how to disable them, what data is retained, how to correct/delete memory and how to revert adaptation.

No covert dependency loop, hidden persuasion, emotional exploitation or vulnerability targeting is part of the system.

## Evaluation matrix
| Gate | Required evidence |
|---|---|
| G0 | Architecture/schema consistency |
| G1 | Boot and recovery |
| G2 | Scheduler fairness, determinism and boundedness |
| G3 | Driver isolation and crash containment |
| G4 | Semantic retrieval correctness + authorization separation |
| G5 | CIRA migration tests + equivalence evidence |
| G6 | WASM/native/DBT compatibility measurements |
| G7 | PUI latency + multimodal synchronization |
| G8 | Privacy + cognitive-sovereignty review |
| G9 | Adversarial multimodal/security evaluation |
| G10 | Signed staged release + rollback |

## Portfolio integration
This project is the convergence layer linking Projects 4, 9, 23, 26, 28, 31, 37, 39, 40, 41, 49, 57 and 58.

## Hard invariants
1. Model output never authorizes privileged execution.
2. Semantic retrieval never grants data access.
3. Persona never grants capability.
4. Biometric/affective observations never silently alter permissions.
5. Generated drivers never enter privileged execution before verification.
6. Self-healing operates through versioned artifacts and rollback.
7. Dependency imports are untrusted supply-chain inputs.
8. Learned scheduling cannot bypass deterministic fairness/safety constraints.
9. Presentation state never becomes authoritative state.
10. Claims of performance/readiness are measured on real targets before promotion to engineering guarantees.

## Iteration 13 — Android PUI / Godot 4.x / 3DGS implementation branch

The new PUI Launcher report turns the existing conceptual PUI line into a concrete mobile implementation branch. The proposed stack is:

```text
ANDROID HOME SHELL
      ↓
GODOT 4.x
      ├── visual scene / PUI state
      ├── GDScript / Compute Shader adaptation
      └── 3DGS renderer
      ↓
KOTLIN ANDROID PLUGIN
      ├── HOME intent
      ├── package/app enumeration
      ├── lifecycle integration
      └── platform permissions
      ↓
SENSOR FUSION
      ├── IMU / kinematics
      ├── touch behavior
      └── application context
      ↓
PUI STATE ESTIMATE
```

The source identifies raw 3DGS as too heavy for an always-on mobile launcher without compression. Therefore the implementation branch adds explicit gates for SOGS/quantized representations, spherical-harmonic reduction, render freezing when obscured, memory bandwidth and battery consumption.

### PUI evidence contract

```yaml
AffectiveObservation:
  modality: imu|touch|context|other
  raw_signal_ref:
  preprocessing_version:
  baseline_ref:
  inferred_state:
  confidence:
  uncertainty:
  retention_policy:
  consent_scope:
```

An inferred affective state is never an authorization primitive and cannot change capability, privacy settings or security policy.

### PUI release gates

- real-device 3DGS frame-time benchmark;
- memory and thermal profile;
- battery impact with launcher visible and obscured;
- sensor-fusion calibration and missing-modality behavior;
- false-positive/false-negative characterization for state inference;
- disclosure and opt-out UI;
- local data-retention verification;
- adaptation reversibility;
- adversarial testing for covert persuasion and vulnerability targeting.

This branch remains a research/engineering architecture until measurements on real Android devices establish performance claims.

## Iteration 26 — AI Launcher evidence integration

The 2025–2026 Android launcher report adds a more explicit contextual-AI branch to the PUI architecture. It describes three evolutionary paths: algorithmic optimization, cloud integration and on-device processing. It specifically identifies UsageStatsManager-derived behavior sequences, sensor/context signals such as GPS, accelerometer, battery state and time-of-day, and LLM-based semantic understanding of notifications/user intent. It also describes NPU-enabled local inference and agentic launchers capable of acting inside applications.

P61 absorbs these findings as engineering requirements rather than as a separate launcher project:

- **context engine:** usage sequence + system context + semantic intent;
- **local inference path:** quantized GGUF-class/on-device models where hardware permits;
- **promptless interaction:** intent inference must remain observable and reversible;
- **adaptive shell:** launcher state is presentation state, never authoritative permission state;
- **privacy modes:** local-only, hybrid and explicitly consented cloud processing;
- **evaluation:** latency, battery, thermal load, false positives, false negatives and user override rate.

The source reports that Smart Launcher 6 uses probabilistic/semantic organization and adaptive correction, while Niagara emphasizes a minimal adaptive list and context-sensitive promotion. These are treated as source observations to benchmark, not as proof of universal superiority.

## Iteration 27 — Home-compute / sovereign ASI architecture integration

The supplied home-ASI report strengthens P61's edge-first architecture with a system-level resource model: compute density, unified/discrete memory trade-offs, aggressive quantization, liquid cooling, high-speed interconnects, local inference, distributed model execution, Zenoh and bounded recursive self-improvement. It explicitly treats residential high-density compute as a thermodynamic and infrastructure problem rather than merely a model-selection problem. The report also proposes SNN/JEPA and 1-bit research directions.

P61 absorbs these as measurable subsystem requirements:
- power/thermal budget as first-class scheduler inputs;
- memory bandwidth and capacity as model-placement constraints;
- local/cloud split selected by privacy, latency and resource budgets;
- Zenoh/device federation treated as transport, never authorization;
- RSI operates through candidate generation, verification and rollback;
- no claim of ASI is inferred from cluster size or model capability alone.

The supplied report cites external market and technology sources and makes strong future-oriented claims; those claims remain source-derived hypotheses until reproduced. The report's own architecture is useful as a design witness, not as proof of achieved ASI.

## Iteration 27 — GQP integration boundary

GQP material is connected to P61 only at the substrate/interface level: heterogeneous compute, GIS/geodesic workloads, quantum-classical execution and visualization. Scientific claims are delegated to P104, which owns the falsification and hardware-validation program. P61 must not convert speculative GQP claims into runtime guarantees.
