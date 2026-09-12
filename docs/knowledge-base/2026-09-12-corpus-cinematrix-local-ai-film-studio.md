# CineMatrix — Local Autonomous AI Film Studio Corpus

**Date:** 2026-09-12
**Source:** supplied architectural report, including its 47 cited references
**Classification:** SOURCE-DERIVED ARCHITECTURAL INPUT; external claims are not independently re-verified by this ingest

## Executive finding

CineMatrix describes a local-first desktop AI film-production system intended to automate a long-form pipeline from screenplay through direction, visual generation, audio, lip-sync, rendering and QA. Its central architectural contribution is not a new media model but a **production orchestration layer** that coordinates multiple specialized local models and preserves narrative/entity continuity across many generated shots.

The supplied report proposes a hierarchical agent topology inspired by ViMax/VideoAgent: Screenwriter → Director → Producer/Orchestrator → visual/audio engines, with a multimodal critic verifying generated results and triggering bounded regeneration.

## Portfolio mapping

The corpus maps most strongly to **P97 — Project MIDAS Recursive Multimedia Production Factory MAX**, with direct strengthening of **P113 — OmniVisual Prompt Compiler & Virtual Art Direction Engine MAX**, **P114 — OmniCognitive Engineering Memory & Verification Substrate MAX**, **P100 — NeXus AI Code OMEGA-X**, and the broader **P07 Agentic Creative Studio** boundary.

No separate numbered project is created. CineMatrix is a specialized local film-studio profile/productization of the existing multimedia-production boundary rather than a distinct architectural domain.

## Core synthesis

```text
FILM BRIEF
   ↓
SCREENWRITER / STORY PLANNER
   ↓
PROJECT WORLD STATE
   ├── characters / identities
   ├── locations / scenography
   ├── events / continuity
   ├── voices / music
   └── visual grammar
   ↓
DIRECTOR / SHOT PLANNER
   ↓
P113 STRUCTURED VISUAL SPECIFICATION
   ↓
LOCAL MODEL ROUTER
   ├── IMAGE
   ├── VIDEO
   ├── TTS
   ├── SFX / MUSIC
   └── LIP-SYNC
   ↓
COMFYUI / RENDER EXECUTION
   ↓
VLM / MULTIMODAL QA
   ↓
REGENERATE / ACCEPT / ESCALATE
   ↓
EDIT / MIX / MASTER
   ↓
ARTIFACT PROVENANCE + REPLAY RECORD
```

## 1. Orchestrator and VRAM scheduler

The report identifies VRAM as the critical local resource and proposes sequential model residency rather than assuming all models can coexist in GPU memory. The durable architectural pattern is a resource-aware scheduler:

```text
TASK
 ↓
RESOURCE REQUIREMENTS
 ↓
VRAM / RAM / DISK CHECK
 ↓
LOAD MODEL
 ↓
EXECUTE
 ↓
READBACK
 ↓
EVICT / CACHE POLICY
 ↓
NEXT STAGE
```

This should be treated as a scheduler policy rather than a hard-coded claim that particular model sizes always fit particular GPUs. Exact memory requirements remain benchmark-dependent.

## 2. Production state

The report proposes JSON project state containing characters, locations and event history. This should evolve into a provenance-bearing **Film World State** rather than a flat collection of prompts.

Minimum entities:
- `Project`
- `Character`
- `Location`
- `Scene`
- `Shot`
- `Performance`
- `Voice`
- `AudioCue`
- `Asset`
- `RenderJob`
- `ContinuityConstraint`
- `QAResult`
- `Artifact`

Every generated asset should retain source shot, model/version, seed or equivalent generation parameters where available, reference assets, workflow identity and validation state.

## 3. Shot-level intermediate representation

CineMatrix materially strengthens P113's scene schema by introducing a film-specific shot matrix. A candidate canonical representation is:

```yaml
shot_id:
scene_id:
sequence_id:
characters: []
location_id:
continuity_refs: []
action:
dialogue:
emotion:
camera:
  shot_size:
  lens:
  movement:
  angle:
lighting:
  key:
  fill:
  rim:
  atmosphere:
visual_style:
reference_frames: []
start_frame:
end_frame:
audio:
  dialogue:
  voice_id:
  music:
  sfx: []
target_duration:
fps:
render_backend:
model_versions: []
validation:
provenance: {}
```

The schema is an internal contract. It is not evidence that any specific vendor or model accepts these fields directly.

## 4. Long-form continuity

The report's SVI/error-recycling approach highlights a major P97 problem: short generative clips must be composed into longer cinematic sequences without visible continuity breaks.

Required continuity state should include:
- last accepted frame;
- next-shot reference frame;
- character appearance state;
- costume/prop state;
- location geometry state;
- lighting/color state;
- camera trajectory;
- motion phase;
- audio/dialogue timing;
- continuity exceptions and accepted deviations.

A generated continuation is never accepted merely because it rendered successfully; it must pass continuity QA.

## 5. Character and location consistency

The report proposes casting/reference generation, LoRA for principal characters, IP-Adapter for lighter identity conditioning, panoramic/location references, depth conditioning and ControlNet-style structural guidance.

Portfolio interpretation:
- principal-character identity is a persistent entity state;
- reference assets are versioned evidence inputs;
- LoRA/IP-Adapter/ControlNet are selectable generation mechanisms, not guaranteed requirements;
- identity similarity must be measured rather than assumed;
- generated character identity is distinct from real-person identity and authorization.

## 6. Multimodal critic loop

CineMatrix adds a concrete audiovisual self-correction loop to P97:

```text
SHOT SPEC
 ↓
GENERATE
 ↓
VLM INSPECTION
 ├── subject/entity
 ├── action
 ├── color
 ├── anatomy/artifact
 ├── camera
 ├── continuity
 └── scene semantics
 ↓
QA RESULT
 ├── ACCEPT
 ├── REGENERATE
 └── HUMAN ESCALATION
```

This must remain bounded. Regeneration loops require attempt budgets, failure classification and escalation; otherwise an agent can spend unbounded local compute without improving the artifact.

## 7. Audio pipeline

The report separates TTS, voice identity, lip-sync, SFX and music. This is architecturally useful because each is a different artifact class with different validation criteria.

```text
DIALOGUE
 ↓
TTS / PERFORMANCE
 ↓
VOICE ARTIFACT

VIDEO + VOICE
 ↓
LIP-SYNC
 ↓
PERFORMANCE VIDEO

SCENE AUDIO PLAN
 ├── DIALOGUE
 ├── SFX
 └── SCORE
 ↓
MIX / MASTER
```

Voice cloning requires an explicit consent/rights policy in production; a technical ability to clone a voice is not authorization to use it.

## 8. Local desktop architecture

The report proposes Electron/React frontend + FastAPI middleware + ComfyUI backend, with Pinokio as installation/process-management infrastructure and Ollama/vLLM as local LLM runtime options.

The durable boundary is:

```text
ELECTRON / REACT UI
        ↓
FASTAPI CONTROL PLANE
        ↓
JOB / STATE / POLICY LAYER
        ↓
COMFYUI / LOCAL MODEL ADAPTERS
        ↓
GPU / CPU / DISK
```

The UI remains a projection of project state. It is not an authorization authority and must not directly expose unrestricted model/runtime controls.

## 9. Relationship to existing projects

### P97 — MIDAS
CineMatrix supplies a concrete long-form film specialization: screenplay → shot list → asset generation → audiovisual assembly → multimodal QA → recursive regeneration → final master.

### P113 — OmniVisual Prompt Compiler
CineMatrix supplies the downstream consumer for P113's structured scene representation and strengthens the need for camera, lens, lighting, action, timeline, entity and continuity fields at shot level.

### P114 — Memory / RAG substrate
The report's local RAG design requires semantic retrieval over screenplay, character state, locations, prior shots and continuity history. Retrieval must remain provenance-bearing and stable-ID based.

### P100 — NeXus AI Code
The Electron/FastAPI/local-runtime stack creates a desktop agent engineering target with the existing Git, DevSecOps, dependency, artifact, security and authorization controls.

### P07 — Agentic Creative Studio
CineMatrix is a concrete creative-studio specialization and can provide a high-complexity reference workflow for multimodal artifact generation and verification.

## 10. Evidence corrections / bounded claims

The supplied report contains many historical or model-specific performance claims. They are retained as source context but are **not promoted as current verified facts** without independent validation.

In particular, the following require fresh benchmarking or current documentation before implementation decisions:
- exact VRAM requirements of Wan/Hunyuan variants;
- exact model file sizes;
- generation speed and 90-minute-film estimates;
- superiority claims between video models;
- exact SVI behavior and supported integrations;
- exact versions/capabilities of Kokoro, F5-TTS, LatentSync, MuseTalk, AudioLDM and MusicGen;
- Pinokio installation semantics;
- ComfyUI API/WebSocket behavior for the selected release;
- availability and licensing terms of all model weights and training datasets.

The report should therefore be treated as an architectural hypothesis plus source map, not as deployment proof.

## 11. Security and rights boundary

The production system must explicitly separate:

`TECHNICAL CAPABILITY ≠ AUTHORIZATION ≠ RIGHTS TO USE`

Required controls include:
- model/license registry;
- source/reference provenance;
- voice/likeness consent records where applicable;
- asset licensing metadata;
- local secret isolation;
- no credential material in prompts or scene JSON;
- policy-gated generation and export;
- artifact hashing and provenance;
- bounded autonomous regeneration;
- human approval for consequential publication/export where required.

## 12. Verification program

1. screenplay-to-shot schema validation;
2. character continuity regression suite;
3. location/scenography continuity suite;
4. camera/lens/lighting coherence checks;
5. start/end-frame continuity tests;
6. temporal flicker and color-drift metrics;
7. dialogue/audio duration synchronization;
8. lip-sync quality evaluation;
9. VLM semantic QA with known ground truth;
10. regeneration-budget tests;
11. VRAM scheduling and OOM recovery tests;
12. model load/evict correctness;
13. deterministic/replayable workflow capture where supported;
14. artifact hash/provenance validation;
15. local-only/offline mode tests;
16. Electron/FastAPI IPC and network boundary tests;
17. dependency/license/model-weight inventory;
18. crash/recovery and partial-render resume;
19. final master integrity validation;
20. human cinematic review before release.

## Status
`ARCHITECTURE ABSORBED INTO EXISTING PORTFOLIO — P97 SPECIALIZATION / P113-P114-P100 EXTENSIONS — NO NEW NUMBERED PROJECT`
