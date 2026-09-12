# Knowledge Corpus — CineMatrix Cloud GPU Render Farm

Date: 2026-09-12
Source: user-provided CineMatrix "Studio w Chmurze" VM-cluster architecture and deployment notes.
Evidence class: source-derived architecture proposal; provider availability, GPU performance, VRAM requirements and exact software compatibility require independent benchmarking/verification.

## Decision

This corpus extends the existing CineMatrix/P97 film-production architecture. It does not warrant a new numbered project.

## Core architectural contribution

The local CineMatrix studio is extended with an optional **Cloud GPU Render Fabric** for parallel video generation/rendering while retaining the local studio as the canonical production/control architecture.

Proposed topology:

`STUDIO / ORCHESTRATOR → JOB QUEUE → GPU WORKER FARM → SHARED STORAGE → QA → ACCEPT / REGENERATE → EDIT / MASTER`

## VM roles

### Brain VM

Responsibilities:
- orchestration;
- screenplay/LLM workloads;
- RAG and project state;
- file/job management;
- dispatch to render workers.

Source proposal: 64 GB RAM, strong CPU, low-GPU or CPU-oriented inference runtime.

### Factory VM

Responsibilities:
- ComfyUI/video generation only;
- horizontally scalable GPU workers;
- execution of queued render jobs.

Source examples: RTX 4090, A6000, H100; multiple workers may operate concurrently.

### Shared storage

A shared volume is proposed so workers can access project assets and outputs without repeated file copying. Production implementation must still define locking, artifact immutability, partial-write handling, consistency semantics and tenant/project isolation.

## Render scheduling

The existing CineMatrix local resource scheduler should evolve from single-host allocation to a distributed scheduler:

`SHOT → RESOURCE ESTIMATE → QUEUE → WORKER SELECTION → MODEL/WORKFLOW LOAD → RENDER → READBACK → ARTIFACT REGISTER → QA → RETRY/REGENERATE`

Worker selection should consider VRAM, model residency, queue depth, expected duration, disk/network throughput, failure history and project priority.

## ComfyUI worker contract

Each worker should expose a versioned execution contract containing:
- worker identity;
- GPU/device profile;
- CUDA/runtime version;
- ComfyUI version;
- workflow hash/version;
- model/checkpoint identifiers;
- input artifact hashes;
- output artifact hashes;
- seed and generation parameters where applicable;
- execution start/end;
- resource usage;
- failure state;
- provenance.

`COMFYUI AVAILABLE ≠ WORKFLOW COMPATIBLE`

## Wan 2.1 / VRAM claim boundary

The source proposes minimum/comfortable VRAM figures for Wan 2.1 14B. These values are preserved as **benchmark hypotheses**, not canonical requirements. Actual feasibility depends on model variant, precision, quantization, resolution, frames, batch size, attention implementation, offloading and workflow configuration.

## Deployment notes

The source proposes a Dockerized ComfyUI image with CUDA 12.x and optionally Pinokio for easier installation on Ubuntu. It also proposes exposing ComfyUI with `--listen` so the orchestration VM can submit jobs.

Production security requirement:
- do not expose ComfyUI directly to an untrusted network;
- place workers behind an authenticated job gateway;
- use project-scoped credentials/capability leases;
- validate workflow payloads before execution;
- isolate worker filesystem and network egress;
- never treat a reachable worker API as authorization.

## Distributed failure model

Cloud rendering introduces new failure classes:
- worker loss;
- GPU OOM;
- model-load failure;
- CUDA/driver mismatch;
- shared-storage timeout;
- artifact corruption/partial write;
- duplicate job execution;
- stale worker state;
- network partition;
- scheduler retry storms.

Required controls include idempotency keys, leases, heartbeats, bounded retries, cancellation, checkpointing, atomic artifact publication and authoritative job-state readback.

## Continuity and provenance

CineMatrix film continuity remains above the infrastructure layer. A render worker may regenerate a shot, but it must not silently change the canonical Shot IR, Film World State or continuity constraints.

`SHOT SPEC → RENDER JOB → WORKER EXECUTION → OUTPUT ARTIFACT → VLM QA → CONTINUITY CHECK → ACCEPT`

## Architectural relation to existing projects

Primary: P97 CineMatrix / multimedia production factory.

Supporting:
- P113 visual prompt/shot specification and cinematic compilation;
- P114 memory/provenance/verification substrate;
- P100 capability broker, sandbox, runtime and release controls.

## Security and evidence invariants

- `CLOUD COMPUTE ≠ CLOUD AUTHORITY`
- `WORKER REACHABILITY ≠ EXECUTION AUTHORIZATION`
- `SHARED STORAGE ≠ IMMUTABLE PROVENANCE`
- `RENDER SUCCESS ≠ CINEMATIC CORRECTNESS`
- `GPU AVAILABILITY ≠ MODEL COMPATIBILITY`
- `LOWER RENDER TIME ≠ PROVEN PRODUCTIVITY GAIN`
- `SANDBOX SUCCESS ≠ PRODUCTION SAFETY`

## Strategic outcome

CineMatrix becomes **hybrid-local by architecture and cloud-scalable by execution**: local orchestration, memory, continuity and control can remain canonical while burst GPU workers provide parallel rendering capacity. This preserves the original local-studio direction without making the render backend a single-host bottleneck.
