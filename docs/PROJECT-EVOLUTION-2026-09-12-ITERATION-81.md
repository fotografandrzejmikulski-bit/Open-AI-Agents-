# Project Evolution — 2026-09-12 — Iteration 81

## Input

CineMatrix "Studio w Chmurze" architecture: Brain VM + scalable GPU Factory VMs, shared storage, ComfyUI workers, optional Pinokio/CUDA environment and cloud/self-hosted GPU deployment.

## Decision

**Primary project:** P97 — CineMatrix / Recursive Multimedia Production Factory MAX  
**Classification:** existing-project extension  
**New standalone project:** no

## Architectural change

P97 gains a **Cloud GPU Render Fabric** that turns the existing local resource scheduler into a distributed, horizontally scalable render scheduler.

The local CineMatrix studio remains the canonical orchestration/control plane. Cloud GPU machines are execution workers.

## New topology

`STUDIO → SHOT IR → RESOURCE ESTIMATE → JOB QUEUE → GPU WORKER LEASE → COMFYUI/VIDEO RENDER → ARTIFACT READBACK → VLM/CONTINUITY QA → ACCEPT / REGENERATE / ESCALATE`

## New capabilities

- distributed GPU render scheduling;
- VRAM-aware worker placement;
- horizontal worker scaling;
- worker capability leases;
- shared artifact storage contract;
- atomic artifact publication;
- distributed job idempotency;
- worker health/heartbeat;
- GPU OOM and worker-failure recovery;
- cloud-burst execution mode;
- provider-neutral GPU worker adapter;
- ComfyUI workflow/model provenance;
- render cost/throughput accounting.

## Existing-project strengthening

P97's previous local scheduler was:

`TASK → RESOURCE ESTIMATE → MODEL LOAD → EXECUTE → READBACK → EVICT/CACHE`

It now becomes:

`TASK → RESOURCE ESTIMATE → QUEUE → WORKER SELECTION → LEASE → EXECUTE → READBACK → REGISTER → QA → RETRY/ESCALATE`.

This preserves the existing film semantics while removing single-GPU execution as the scalability bottleneck.

## Cross-project mappings

- **P100:** capability broker, policy, sandbox, credentials, network gateway, release controls.
- **P113:** canonical Shot IR / visual specification.
- **P114:** memory, provenance and verification substrate.
- **P97:** film-world state, continuity, production orchestration and final cinematic QA.

## Security boundary

ComfyUI `--listen`, a shared volume or an available cloud VM does not grant authorization. Worker execution must be bounded by project-scoped leases, authenticated job dispatch, workflow validation, network policy and artifact provenance.

## Reliability boundary

Distributed rendering adds worker loss, OOM, CUDA mismatch, storage consistency, network partitions, duplicate execution and retry storms. These become first-class test scenarios.

## Evidence boundary

Exact claims about Wan 2.1 14B VRAM requirements, RTX 4090/A6000/H100 suitability, CUDA versions, Pinokio installation, RunPod/Vast.ai/Proxmox economics and expected speed are source-derived and require workload-specific benchmarks.

## New invariants

`CLOUD COMPUTE ≠ AUTHORITY`

`WORKER REACHABILITY ≠ AUTHORIZATION`

`RENDER SUCCESS ≠ CINEMATIC CORRECTNESS`

`PARALLEL WORKERS ≠ LINEAR SPEEDUP`

`SHARED STORAGE ≠ IMMUTABLE PROVENANCE`

`CLOUD CAPACITY ≠ UNBOUNDED BUDGET`

## Outcome

CineMatrix is now architecturally **hybrid-local / cloud-scalable**: the canonical film state and control logic can remain local while rendering bursts across multiple GPU VMs. The design supports later provider substitution without coupling CineMatrix to one cloud vendor.
