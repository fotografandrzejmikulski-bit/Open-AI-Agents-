# OmniCore Self-Evolving Computing Substrate — 2026-09-09

## Source scope

Consolidated from the ten newly uploaded OmniCore documents and reconciled with the repository's existing OmniCore, assurance and discovery architecture. Duplicate prototype PDFs are treated as corroborating variants.

## Core synthesis

The corpus converges on a vertical stack:

`Rust no_std kernel → AI Supervisor → SemanticFS → HAL/DBT → Omnis/MLIR/CIRA → AI Foundry → MeshBus → PUI/3DGS → private experimental Forge`.

The kernel prototype explicitly initializes hardware abstraction, learned scheduling, semantic storage and a distributed device bus. fileciteturn311file0L10-L30

The hybrid-language corpus proposes Omnis as a common substrate for heterogeneous languages, with Nexus, WASM and CIRA providing interoperability and AI-assisted transformation. fileciteturn313file4L193-L228

The MLIR material defines hybrid memory types and lowering for RAII/GC domains and positions CIRA as an intelligent compiler pass. fileciteturn312file12L522-L568

The AI Foundry concept combines hardware discovery, technical-document retrieval, local model analysis and generated Rust drivers; generated low-level code remains untrusted until build/test/verification. fileciteturn313file15L764-L769

The MeshBus architecture treats devices as nodes in a distributed actor system and supports resource-aware offloading. fileciteturn313file8L413-L439

The PUI corpus describes 3DGS, local SLMs, episodic memory and affective adaptation as an interaction layer. fileciteturn313file9L458-L474

## New architectural insight

The new capability is not any individual OmniCore component. It is the **closed-loop experimental evolution of the computing substrate itself**:

```text
OBSERVE
 → UNKNOWN / BOTTLENECK
 → COMPETING ENGINEERING HYPOTHESES
 → GENERATE VARIANTS
 → BUILD
 → SIMULATE / QEMU / HIL
 → MEASURE
 → VERIFY
 → REPLICATE
 → STAGED RELEASE
 → HEALTH READBACK
 → LEARN
```

This is a concrete specialization of Project 79's discovery loop applied to Project 61/68's computing substrate and bounded by Project 72 assurance.

## Epistemic boundary

The source material contains ambitious claims concerning AI-native kernels, universal portability, generated drivers, low latency and autonomous adaptation. These are design hypotheses or targets unless reproduced experimentally. Existing repository doctrine therefore requires explicit separation of source assertion, observation, simulation, measurement, inference and established result.

## Safety boundary

Self-evolution is implemented as versioned candidate generation, not unrestricted privileged self-modification. The required lifecycle is:

`DETECT → ISOLATE → SNAPSHOT → GENERATE → CHECK → TEST → SIGN → STAGE → HEALTH VERIFY → ROLLBACK/PROMOTE`.

The model is a proposal engine. Policy, capability authorization, deterministic safety constraints and authoritative readback remain outside model authority.

## Reusable research primitives

- immutable baseline during experiments;
- multi-objective/Pareto evaluation;
- reproducible workload suites;
- variant registries;
- semantic engineering memory;
- cross-platform invariance tests;
- independent replication;
- staged activation;
- health verification;
- automatic rollback;
- provenance-linked failure memory.

## Portfolio mapping

- Project 61: OmniCore/Omnis/PUI convergence substrate.
- Project 68: constitutional runtime and lifecycle control.
- Project 72: assurance, authorization, verification and rollback boundary.
- Project 79: discovery, hypothesis competition and experiment selection.
- Projects 58/60: monitorability and adversarial resilience.
- Project 77: formal mathematical verification backend.
- Projects 71/74/76: physical, device and interactive experimental substrates.
