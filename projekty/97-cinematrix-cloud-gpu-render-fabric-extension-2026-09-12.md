# P97 Extension — CineMatrix Cloud GPU Render Fabric

Date: 2026-09-12
Parent: P97 — CineMatrix / Recursive Multimedia Production Factory MAX
Classification: EXISTING PROJECT EXTENSION

## Mission

Add a horizontally scalable GPU render fabric to CineMatrix without replacing its local orchestration, film-world state, continuity, shot specification or verification layers.

The cloud layer is an execution substrate, not the authority for cinematic state.

## Target architecture

```text
CINEMATRIX STUDIO
      ↓
FILM WORLD STATE / SHOT IR / PROVENANCE
      ↓
RENDER PLANNER
      ↓
RESOURCE ESTIMATOR
      ↓
DISTRIBUTED JOB QUEUE
      ↓
┌─────────────────────────────────────────┐
│ GPU WORKER POOL                         │
│ ComfyUI / VIDEO BACKENDS                │
│ Worker A   Worker B   Worker C   ...    │
└─────────────────────────────────────────┘
      ↓
ATOMIC ARTIFACT REGISTRATION
      ↓
VLM QA + CONTINUITY QA
      ↓
ACCEPT / REGENERATE / ESCALATE
      ↓
EDIT / MIX / MASTER
```

## Brain VM

The Brain VM owns orchestration, screenplay/LLM services, RAG, project database, job management and worker dispatch.

The supplied architecture proposes 64 GB RAM and a strong CPU with optional low-GPU/CPU model serving. These are starting-point sizing assumptions, not verified requirements.

## Factory VM

Factory VMs are specialized render workers. Their principal responsibility is ComfyUI/video generation. The pool may scale horizontally according to queued render demand.

Candidate hardware from the source:
- RTX 4090;
- RTX A6000;
- NVIDIA H100.

Hardware selection must be benchmarked against actual CineMatrix workflows rather than inferred from GPU names alone.

## Shared storage plane

A shared volume may reduce asset-transfer overhead between workers. It must implement:
- project/tenant isolation;
- atomic publication;
- artifact locking or immutable versioning;
- partial-write detection;
- checksums/content hashes;
- stale-write protection;
- lifecycle/retention policy.

The canonical artifact identity remains in CineMatrix provenance rather than in a worker's local filesystem.

## Distributed Render Scheduler

New control loop:

`SHOT → RESOURCE ESTIMATE → QUEUE → LEASE WORKER → LOAD WORKFLOW/MODEL → EXECUTE → READBACK → REGISTER ARTIFACT → QA → COMPLETE / RETRY / ESCALATE`

Scheduling dimensions:
- VRAM/RAM requirements;
- model residency;
- GPU class;
- queue depth;
- project priority;
- expected duration;
- worker health;
- storage/network capacity;
- historical failure rate;
- budget/cost ceiling.

## Worker lease

Each render job should receive a bounded worker capability lease containing:
- project/tenant;
- shot/job identity;
- workflow version/hash;
- allowed backend/model;
- input artifact set;
- output location;
- resource/time budget;
- network policy;
- expiration;
- correlation/idempotency key.

A worker must not infer additional authority from the job payload.

## ComfyUI API boundary

ComfyUI is treated as a backend adapter. Its network API must be placed behind an authenticated job gateway or equivalent control boundary. `--listen` is a connectivity setting, not an authorization mechanism.

Workflow payloads require schema validation and policy checks before dispatch. Model files, custom nodes and workflows require provenance and compatibility validation.

## Render reproducibility

For every output CineMatrix should preserve:

`SHOT_IR + WORKFLOW_HASH + MODEL_ID/VERSION + INPUT_HASHES + SEED + PARAMETERS + WORKER_PROFILE + RUNTIME_VERSION + TIMESTAMP + JOB_ID → OUTPUT_HASH`

Where the generator does not provide deterministic output, reproducibility means replayable configuration/provenance rather than guaranteed byte-identical pixels.

## Failure and recovery

Required distributed-runtime controls:
- worker heartbeat;
- lease expiration;
- idempotent job identity;
- bounded retry policy;
- retry classification;
- GPU OOM handling;
- worker quarantine after repeated faults;
- checkpoint/partial-render handling;
- atomic artifact publication;
- stale-state rejection;
- cancellation;
- authoritative scheduler readback.

Retry must not silently produce multiple canonical outputs for one Shot IR version.

## Continuity boundary

A worker may render or regenerate a shot but cannot mutate canonical film continuity by itself.

```text
CANONICAL SHOT SPEC
       ↓
RENDER CANDIDATE
       ↓
VLM / CONTINUITY EVALUATION
       ↓
ACCEPTED ARTIFACT
```

A regenerated shot remains a candidate until QA and provenance checks pass.

## Cloud burst mode

The architecture supports three operating modes:

1. **LOCAL:** all workloads on the workstation/local studio;
2. **HYBRID:** local Brain + burst GPU Factory workers;
3. **CLOUD FARM:** orchestrator and workers distributed across GPU VMs.

Mode switching must not change authorization semantics or canonical project state.

## Provider abstraction

RunPod, Vast.ai and self-hosted Proxmox/GPU-Passthrough are source-proposed deployment options. They are provider candidates, not verified recommendations. P97 should expose a provider-neutral worker contract so the scheduler can select a backend based on cost, capacity, locality, privacy and compatibility.

## Verification backlog

- end-to-end queued shot execution;
- concurrent worker scheduling;
- VRAM-aware placement;
- worker lease expiration;
- duplicate-job suppression;
- shared-storage consistency;
- GPU OOM recovery;
- CUDA/driver mismatch detection;
- ComfyUI workflow compatibility;
- model/custom-node provenance;
- artifact hash verification;
- VLM/continuity QA after distributed rendering;
- local/hybrid/cloud equivalence tests;
- cost and throughput benchmark;
- failure-injection tests;
- recovery after worker/network loss.

## New invariants

`CLOUD COMPUTE ≠ AUTHORITY`

`WORKER REACHABILITY ≠ AUTHORIZATION`

`JOB ACCEPTANCE ≠ ARTIFACT CORRECTNESS`

`RENDER SUCCESS ≠ CINEMATIC QUALITY`

`SHARED VOLUME ≠ IMMUTABLE STORAGE`

`GPU CLASS ≠ GUARANTEED PERFORMANCE`

`PARALLELISM ≠ LINEAR SPEEDUP`

`CLOUD SCALE ≠ UNBOUNDED BUDGET`

## Portfolio relation

P97 owns film-production semantics and orchestration.

P113 owns visual/shot specification.

P114 owns memory/provenance/verification patterns.

P100 owns capability, policy, sandbox, runtime, credential and release-control primitives.

The Cloud GPU Render Fabric is therefore a P97 execution-plane extension rather than a separate numbered project.

## Status

`ARCHITECTURE-INTEGRATED / IMPLEMENTATION-READY AFTER BENCHMARKING`

The supplied hardware, VRAM, provider and performance claims remain source-derived until measured against actual CineMatrix workloads.
