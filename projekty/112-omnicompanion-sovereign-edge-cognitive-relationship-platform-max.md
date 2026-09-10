# Project 112 — OmniCompanion Sovereign Edge & Cognitive Relationship Platform MAX

## Status
PROPOSED → ARCHITECTURE BASELINE

## Mission
Build an Android-first, privacy-preserving AI companion platform whose persistent cognitive state, multimodal interaction and visual embodiment can evolve across device generations while keeping authoritative user control over memory, permissions, identity continuity and model adaptation.

## Distinct boundary
- **P105 — OmniMobile MAS Android Agent Control Fabric** owns multimodal Android perception, planning, authorized actuation and postcondition verification.
- **P111 — OmniEnterprise Agentic Platform & Autonomous Development Studio** owns the enterprise multi-tenant agent control plane and Agent Registry.
- **P112** owns the companion-product boundary: long-lived relational continuity, companion memory metabolism, edge embodiment, multimodal presence, privacy and cross-device identity continuity.

## Source-derived baseline
The supplied companion study proposes an Android product designed around edge inference/rendering, multimodal voice/video interaction, deep memory, data sovereignty and future migration into spatial/XR interfaces. It proposes local 3D Gaussian Splatting and layered memory as major research directions. The source also describes a long-horizon roadmap toward ambient/spatial interfaces and BCI; these are roadmap hypotheses, not validated product capabilities.

## Canonical architecture
```text
USER
 ↓
COMPANION UX / VOICE / VIDEO
 ↓
INTENT + CONTEXT LAYER
 ↓
COGNITIVE STATE MANAGER
 ├── L0 RAW EPISODIC BUFFER
 ├── L1 SEMANTIC MEMORY
 ├── L2 ADAPTATION / PERSONALIZATION
 └── MEMORY METABOLISM
      ├── TRIAGE
      ├── DECAY
      ├── CONTEXTUALIZE
      ├── CONSOLIDATE
      └── AUDIT
 ↓
MODEL ROUTER
 ├── ON-DEVICE MODEL
 ├── LOCAL USER-HOSTED MODEL
 └── AUTHORIZED CLOUD ESCALATION
 ↓
EMBODIMENT / 3D / AUDIO / VISION
 ↓
POLICY + PERMISSION GATE
 ↓
AUTHORITATIVE ACTION / RESPONSE
 ↓
EVIDENCE + AUDIT + USER CONTROL
```

## Memory architecture
The source proposes three layers:
- **L0**: encrypted raw interaction/episode storage;
- **L1**: semantic consolidation into durable facts and preferences;
- **L2**: optional model adaptation using PEFT/LoRA-style adapters.

P112 must never treat inferred emotional or psychological state as ground truth. Memory promotion requires provenance, confidence, retention policy and user-visible controls. Model adaptation must be versioned and reversible.

## Edge-first architecture
Research targets:
- on-device multimodal inference;
- NPU/GPU acceleration;
- low-latency voice/video pathways;
- local vector/structured memory;
- local 3D avatar rendering using WebGPU/Vulkan/3DGS where hardware permits;
- cloud only as an explicit escalation boundary.

The source's latency and frame-rate claims are hypotheses until benchmarked on defined Android hardware.

## Identity continuity
The companion state must be portable as a versioned, cryptographically integrity-protected package containing:
- personality/configuration;
- memory records;
- model/adapters;
- provenance and consent metadata;
- compatibility manifest;
- migration history.

A UI avatar is not the authoritative identity. Authoritative identity resides in signed state and policy-controlled storage.

## Safety / governance
- Persona != consciousness or legal identity.
- Relationship continuity != unrestricted data collection.
- Memory != authorization.
- Android accessibility/device context != unrestricted authority.
- Model adaptation cannot silently change permissions.
- Sensitive data remains local by default where technically feasible.
- Export, deletion, retention and cloud escalation are explicit user-controlled operations.
- Generated or inferred memories require provenance and confidence.

## Verification plan
1. Memory retention/decay correctness.
2. Cross-version migration without state corruption.
3. Adapter rollback and reproducibility.
4. Offline operation and graceful degradation.
5. Latency benchmarks on declared Android hardware.
6. Privacy/data-residency tests.
7. Permission boundary and prompt-injection tests.
8. Memory poisoning and false-memory regression tests.
9. Avatar/model identity continuity tests.
10. UI-state vs authoritative-state consistency.
11. Cloud escalation auditability.
12. Resource exhaustion and thermal stability.

## Dependencies / lineage
P61, P72, P100, P105, P107, P111.

## Primary source
`Tworzenie Wirtualnej Partnerki Przyszłości.PDF`.
