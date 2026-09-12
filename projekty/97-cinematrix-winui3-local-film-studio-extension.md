# P97 Extension — CineMatrix WinUI 3 Local Film Studio

## Parent
P97 — Project MIDAS Recursive Multimedia Production Factory MAX

## Boundary
CineMatrix is the local Windows-native specialization of P97: an autonomous long-form film-production workspace rather than a generic multimedia content factory.

## Target architecture

```text
WINUI 3 / XAML
      ↓
MVVM / STUDIO STATE
      ↓
FILM WORLD + SHOT IR
      ↓
ORCHESTRATOR / POLICY
      ↓
MODEL RESOURCE SCHEDULER
      ↓
LLM / IMAGE / VIDEO / AUDIO ADAPTERS
      ↓
RENDER / ASSEMBLY
      ↓
MULTIMODAL QA
      ↓
PROVENANCE / REPLAY / PROMOTION
```

## Native Windows layer
- WinUI 3 / Windows App SDK;
- XAML NLE-style workspace;
- CommunityToolkit.Mvvm;
- native media preview via MediaPlayerElement;
- asynchronous UI state projection;
- cinematic progress states during model loading/eviction.

## Execution adapters
CineMatrix must support a capability-selected execution boundary:

1. **Local process adapter:** ComfyUI on localhost with documented HTTP/WebSocket interfaces.
2. **Embedded Python adapter:** CPython integration such as CSnakes where dependency/runtime validation permits it.
3. **Native inference adapter:** llama.cpp/LLamaSharp or equivalent for selected local language workloads.

The application must not assume that embedding Python makes the entire video stack in-process. The actual execution boundary is recorded per adapter and per render job.

## Resource scheduler

The GPU resource manager becomes a first-class subsystem:

`RESOURCE SNAPSHOT → PLAN → EVICT/LOAD → VERIFY RESIDENCY → INFER → RELEASE → VERIFY → NEXT PHASE`

It tracks VRAM budget, model residency, CPU/RAM pressure, concurrent jobs, fallback strategy and failure recovery. `empty_cache()` or forced GC is only an implementation mechanism; it is not verification evidence.

## CineMatrix Shot IR

```yaml
shot_id:
scene_id:
sequence_id:
narrative_intent:
subject_refs: []
location_ref:
camera:
  shot_type:
  lens:
  movement:
  angle:
  depth_of_field:
lighting:
color_grade:
action:
dialogue:
audio_refs: []
start_frame_ref:
end_frame_ref:
duration_ms:
fps:
model_adapter:
workflow_ref:
seed:
quality_profile:
verification_requirements: []
```

The Shot IR is canonical. Model-specific prompts and ComfyUI node graphs are compiled artifacts and may change without changing film identity.

## Long-form production
P97's recursive loop is extended for feature-film continuity:

`SCRIPT → WORLD STATE → SHOT PLAN → CAST/LOCATION REFERENCES → GENERATE → VLM QA → REGENERATE/ESCALATE → EDIT → MASTER → VERIFY`

Continuity state must include character identity, wardrobe, props, location geometry, lighting language, temporal position, dialogue and previous/next shot constraints.

## Local persistence
SQLite/EF Core may serve as the in-process project database. Persistent objects require stable IDs and provenance. Project/world data is local by default; no cloud dependency is implied by the architecture.

## Packaging
Application binaries and model assets are separate release surfaces. The proposed external-location/sparse-packaging route is retained as a release candidate architecture and requires actual Windows packaging, install, update, permissions and model-path validation before promotion.

## Verification gates
- adapter startup and capability discovery;
- model residency before/after each phase;
- render job identity and completion readback;
- workflow schema validation;
- artifact existence, codec and duration validation;
- visual/audio QA;
- continuity regression;
- cancellation and crash recovery;
- installer/update/rollback verification;
- reproducibility using persisted seed/model/workflow metadata.

## Status
`ARCHITECTURE ENHANCED — IMPLEMENTATION NOT VERIFIED`

## Derived from
P97, P100, P113, P114 and the supplied CineMatrix WinUI 3 documents.
