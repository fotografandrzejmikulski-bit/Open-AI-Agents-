# Project 80 — OmniCore Self-Evolving Computing Substrate MAX

## Status
PROPOSED → ARCHITECTURE BASELINE → PROJECT GENESIS 2026-09-09

## Thesis

Project 80 turns the OmniCore concept from an AI-native operating system into a **measurable, self-improving computing substrate**.

The key distinction from Projects 61, 68 and 79 is the closed loop between **scientific discovery and the system that performs the discovery**:

```text
OBSERVE OMNICORE
      ↓
DISCOVER BOTTLENECK / DEFECT / OPPORTUNITY
      ↓
FORM COMPETING ENGINEERING HYPOTHESES
      ↓
GENERATE CANDIDATE KERNEL / COMPILER / DRIVER / RUNTIME CHANGE
      ↓
BUILD ISOLATED VARIANTS
      ↓
BENCHMARK / FORMALLY CHECK / HIL TEST
      ↓
COMPARE AGAINST BASELINE
      ↓
INDEPENDENT VERIFICATION
      ↓
SIGNED STAGED RELEASE
      ↓
HEALTH OBSERVATION
      ↓
ROLLBACK OR PROMOTE
      ↺
```

This is **not** unrestricted self-modifying code. Evolution is an experimentally controlled, versioned and reversible process.

## Why this is a new project

Project 61 converges Omnis, the learned kernel and PUI. Project 68 defines the constitutional runtime. Project 72 provides assurance. Project 79 provides autonomous scientific discovery.

Project 80 creates the missing **self-evolution substrate**: a concrete domain in which Project 79 can operate on the architecture itself while Project 72 prevents the discovery loop from becoming an authority loop.

The source corpus independently supplies the required building blocks: Rust `no_std` kernel prototypes, AI Supervisor scheduling, SemanticFS, HAL/DBT, AI Foundry driver synthesis, Omnis/MLIR, CIRA, MeshBus, 3DGS/PUI and a private QEMU/GPU agent factory. The prototype kernel explicitly separates boot, hardware abstraction, learned scheduling, semantic storage and distributed bus initialization. fileciteturn311file0L10-L30

## 1. System architecture

```text
                         OMNICORE
                            │
          ┌─────────────────┼──────────────────┐
          │                 │                  │
      OBSERVATION       KNOWLEDGE          AUTHORITY
          │                 │                  │
          └────────────┬────┴───────┬──────────┘
                       ↓             ↓
                 OMNIDISCOVERY    POLICY / 72
                    (79)             │
                       ↓             │
               ENGINEERING HYPOTHESES
                       ↓
                VARIANT COMPILER
                       ↓
        ┌──────────────┼──────────────┐
        ↓              ↓              ↓
     KERNEL         OMNIS/CIRA      DRIVER/HAL
     VARIANT          VARIANT         VARIANT
        └──────────────┼──────────────┘
                       ↓
              DIGITAL EXPERIMENTAL LAB
                 QEMU / SIM / HIL
                       ↓
              ASSURANCE + REPLICATION
                       ↓
             STAGED ARTIFACT REGISTRY
                       ↓
             CONTROLLED ACTIVATION
                       ↓
                HEALTH READBACK
```

## 2. Four evolutionary domains

### A. Kernel evolution

Candidate changes include scheduling policy, memory paths, IPC, interrupt handling and resource allocation.

The AI Supervisor remains a bounded optimizer. Deterministic fairness, watchdogs, resource ceilings, emergency fallback and rollback remain authoritative. The source prototype already treats learned scheduling as a kernel component, but the supplied implementation is a PoC rather than evidence of production viability. fileciteturn311file5L31-L49

### B. Compiler evolution

Omnis uses MLIR to represent hybrid memory semantics, including `LinearRef`, `GcRef` and explicit hybrid scopes. The source material describes lowering and CIRA as an intelligent compiler pass. fileciteturn312file12L522-L568

Project 80 lets the discovery loop test compiler transformations against reproducible workloads rather than assuming a transformation is beneficial.

### C. Hardware / driver evolution

AI Foundry can inspect hardware, retrieve authoritative documentation and propose Rust drivers. The source explicitly presents this as a generation-and-build loop; Project 80 adds mandatory quarantine, compilation, sandbox/QEMU/HIL testing, signing and staged activation. fileciteturn313file15L764-L769

### D. Distributed substrate evolution

MeshBus exposes a device-level actor model with location transparency and predicted resource-aware task migration. The source describes moving computation from a battery-powered device to a nearby workstation when latency, energy and workload conditions justify it. fileciteturn313file8L413-L439

## 3. Engineering Discovery Object

```yaml
EvolutionCase:
  id:
  baseline_artifact:
  target_layer:
  observed_problem:
  hypotheses: []
  candidate_variants: []
  workload_suite: []
  invariants: []
  predicted_effects: []
  measured_effects: []
  regressions: []
  security_findings: []
  formal_evidence: []
  replication_refs: []
  rollout_policy:
  rollback_policy:
  status:
```

## 4. Variant laboratory

No candidate replaces the baseline directly.

```text
BASELINE B
   │
   ├── V1
   ├── V2
   ├── V3
   └── Vn
        ↓
CONTROLLED BENCHMARK
        ↓
STATISTICAL COMPARISON
        ↓
SAFETY / CORRECTNESS GATES
        ↓
INDEPENDENT RE-RUN
        ↓
PROMOTION CANDIDATE
```

A candidate is rejected when it improves one metric while violating a hard invariant, even if its aggregate score is better.

## 5. Multi-objective optimization

The system must not optimize only for throughput.

A candidate vector is evaluated across:

- latency;
- throughput;
- energy;
- memory pressure;
- fairness;
- crash/recovery behavior;
- security surface;
- determinism;
- compilation cost;
- portability;
- observability;
- reproducibility.

The optimization result is therefore a Pareto frontier, not a single opaque score.

## 6. Constitutional evolution boundary

The system distinguishes four classes:

```text
MODEL PROPOSAL
ENGINEERING ARTIFACT
VERIFIED CANDIDATE
AUTHORITATIVE RELEASE
```

No transition is implicit.

```text
proposal → artifact: compiler/build gate
artifact → candidate: tests + invariants
candidate → release: independent assurance + approval policy
release → active: staged deployment + health verification
```

This directly preserves the repository invariant that model output never authorizes privileged execution. Project 61 already defines generated drivers as quarantined until verification and self-repair as versioned replacement with rollback. fileciteturn333file0L2-L2

## 7. SemanticFS as evolutionary memory

SemanticFS becomes more than a user file system. It stores searchable engineering evidence:

```text
artifact
benchmark
trace
failure
counterexample
hardware profile
compiler decision
release
rollback
```

Semantic similarity remains discovery only; access still requires provenance, capability and authorization. The source architecture explicitly defines SemanticFS around embeddings/HNSW and natural-language queries. fileciteturn311file0L50-L57

## 8. AI Foundry + Omniscience + OmniDiscovery

The three loops are composed rather than duplicated:

```text
OMNISCIENCE
knowledge injection + interdisciplinary critique
                 ↓
OMNIDISCOVERY 79
unknown → hypotheses → discriminating experiment
                 ↓
OMNICORE 80
experiment → system variant → measured result
                 ↓
PROJECT 72
assurance → verification → release decision
                 ↓
KNOWLEDGE
                 ↺
```

The Omniscience source already separates knowledge injection, multidisciplinary analysis, hypothesis generation, adversarial critique and verification. fileciteturn326file0L2-L2

## 9. Private experimental forge

The supplied infrastructure material describes a GCP Forge combining nested virtualization, GPU inference, local models, vector retrieval, QEMU/KVM and federated coding agents. These configurations are treated as reference scenarios, not universal requirements. fileciteturn322file0L2-L2

Project 80 uses the Forge as an experimental substrate with this boundary:

```text
HOST
  ↓
L1 BUILD / AGENT ENVIRONMENT
  ↓
L2 ISOLATED OMNICORE IMAGE
  ↓
TEST / FAULT INJECTION / BENCHMARK
  ↓
EVIDENCE
```

## 10. PUI / Human Factor evolution

The source proposes a personified interface using 3D Gaussian Splatting, WebGPU, local SLM inference, episodic memory and an affective loop. fileciteturn313file9L458-L474

Project 80 treats PUI as another measurable subsystem, not as a privileged authority:

- rendering latency;
- interaction latency;
- multimodal synchronization;
- accessibility;
- adaptation accuracy;
- privacy;
- user-visible control of adaptation.

Affective or biometric observations cannot silently change capabilities or permissions.

## 11. Cross-platform invariance

The source proposes one codebase across x86_64 and AArch64, with WASM and binary translation used for portability. fileciteturn313file2L99-L113

Project 80 defines an invariance suite:

```text
SAME SEMANTIC PROGRAM
        ↓
 x86_64 | AArch64 | WASM
        ↓
COMPARE
  semantics
  safety
  resource profile
  observable behavior
```

Portability is accepted only where the behavior has been measured.

## 12. Scientific operating principle

Project 80 adopts Project 79's epistemic discipline:

```text
simulation ≠ hardware observation
benchmark ≠ universal law
model agreement ≠ evidence
performance gain ≠ correctness
single run ≠ replication
```

Every important improvement must have a baseline, workload, environment, measurement protocol, uncertainty characterization and replication path.

## 13. Hard invariants

1. The system may propose changes; it cannot self-authorize privileged changes.
2. Every release is versioned and rollback-capable.
3. Baselines remain immutable during an experiment.
4. Learned scheduling cannot violate deterministic safety constraints.
5. Generated drivers remain untrusted until independently verified.
6. Semantic retrieval never grants permission.
7. Presentation state never becomes authoritative system state.
8. A performance improvement cannot compensate for a safety regression.
9. One experiment cannot establish a universal engineering claim.
10. Independent replication is required for promotion of high-impact discoveries.
11. Failed variants become evidence rather than disappearing history.
12. Human approval, where required, is a resumable state transition.
13. Monitorability degradation increases verification requirements.
14. Supply-chain and documentation inputs remain untrusted until validated.
15. Unknown, hypothesis, observation, simulation and established result remain distinct epistemic types.

## 14. Evaluation gates

| Gate | Requirement |
|---|---|
| E0 | reproducible baseline |
| E1 | variant builds successfully |
| E2 | semantic/invariant checks pass |
| E3 | deterministic regression suite passes |
| E4 | isolated QEMU/sandbox test passes |
| E5 | performance/energy measurements recorded |
| E6 | security and supply-chain checks pass |
| E7 | independent rerun reproduces result |
| E8 | staged activation succeeds |
| E9 | authoritative health readback succeeds |
| E10 | rollback path demonstrated |

## 15. Roadmap

### Phase I — Experimental substrate
QEMU boot, immutable images, baseline benchmark suite, artifact manifests and deterministic fallback.

### Phase II — Learned scheduler laboratory
Compare deterministic baselines with bounded learned scheduling under identical workloads.

### Phase III — Omnis/CIRA laboratory
Implement a small MLIR dialect, controlled transformations and equivalence/regression tests.

### Phase IV — AI Foundry laboratory
Build documentation-to-driver pipeline with quarantine, compilation and HIL/QEMU verification.

### Phase V — Cross-device laboratory
Evaluate MeshBus-style actor migration across heterogeneous devices.

### Phase VI — Closed self-evolution loop
Connect Project 79 experiment selection to Project 80 variant generation, with Project 72 acting as the assurance boundary.

### Phase VII — External replication
Reproduce the strongest findings on an independent environment and hardware class.

## 16. Definition of Done

Project 80 is not complete when OmniCore boots.

It is complete when the system can demonstrate, reproducibly:

- generation of multiple competing system variants;
- automated benchmark execution;
- rejection of unsafe or regressive variants;
- independent reproduction of selected improvements;
- staged promotion and verified rollback;
- provenance-linked engineering memory;
- cross-platform behavior comparison;
- a complete `observe → hypothesize → build → test → verify → release → learn` loop.

## Evidence boundary

**SOURCE-DERIVED:** the uploaded OmniCore documents describe the kernel, AI Supervisor, SemanticFS, Omnis/MLIR, CIRA, AI Foundry, MeshBus, PUI and private experimental infrastructure. fileciteturn311file2L2-L17

**INFERRED:** these components can form a self-evolution architecture only when connected through an experimental controller and strict authority boundaries.

**PROPOSED:** Project 80 is an engineering research program. It does not claim that an autonomous self-improving operating system has already been demonstrated.
