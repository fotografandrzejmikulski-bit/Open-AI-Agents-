# P97 Extension — CineMatrix Local Autonomous AI Film Studio

## Parent
P97 — Project MIDAS Recursive Multimedia Production Factory MAX

## Decision
CineMatrix is absorbed as a **specialized local long-form film-production profile of P97**, not as a new numbered project. P97 already owns the multimedia production loop; CineMatrix contributes a concrete desktop/local implementation profile and stronger continuity, VRAM and audiovisual QA contracts.

## Production topology

```text
FILM BRIEF
 ↓
SCREENWRITER / STORY PLANNER
 ↓
FILM WORLD STATE
 ↓
DIRECTOR / SHOT PLANNER
 ↓
P113 VISUAL SPECIFICATION
 ↓
LOCAL MODEL ROUTER
 ├── IMAGE
 ├── VIDEO
 ├── TTS
 ├── SFX / MUSIC
 └── LIP-SYNC
 ↓
COMFYUI / RENDER
 ↓
VLM QA
 ↓
ACCEPT / REGENERATE / ESCALATE
 ↓
EDIT / MIX / MASTER
 ↓
PROVENANCE / REPLAY
```

## Local resource scheduler

`task → VRAM/RAM/disk estimate → model load → execute → readback → evict/cache → next stage`.

The supplied report's exact VRAM/model-size/speed figures remain hypotheses until locally benchmarked.

## Film World State

Persistent entities:
`Project, Character, Location, Scene, Shot, Performance, Voice, AudioCue, Asset, RenderJob, ContinuityConstraint, QAResult, Artifact`.

Continuity state includes reference frames, character appearance/costume/props, location geometry, lighting/color, camera trajectory, motion phase and dialogue timing.

## Shot-level contract

P97 consumes P113's canonical visual representation and adds film-specific shot identity, scene/sequence lineage, character/location references, action, dialogue, emotion, camera, lighting, start/end frames, audio, duration/FPS, backend/model versions, validation and provenance.

## Multimodal QA

```text
SHOT → GENERATE → VLM INSPECT → ACCEPT / REGENERATE / HUMAN ESCALATION
```

Regeneration requires bounded attempt budgets, failure classification and escalation. A successful render is not a correctness proof.

## Audio contract

Dialogue/TTS, voice identity, lip-sync, SFX and music are separate artifact classes. Voice cloning requires explicit rights/consent policy; technical capability is not authorization.

## Long-form continuity

SVI/error-recycling concepts from the supplied report are retained as research inputs. Production use requires current compatibility evidence and continuity benchmarks. The pipeline must preserve start/end-frame lineage and detect temporal flicker, color drift and identity drift.

## Desktop implementation profile

The source proposes Electron/React frontend, FastAPI middleware and ComfyUI backend, with local LLM runtimes such as Ollama/vLLM and Pinokio for installation/process management. P100 owns desktop security/release controls; P97 owns film semantics and production orchestration.

## Verification backlog

- screenplay-to-shot compilation;
- character/location continuity regression;
- temporal/color consistency;
- dialogue/audio duration synchronization;
- lip-sync evaluation;
- VLM semantic QA;
- bounded regeneration;
- VRAM/OOM recovery;
- model load/evict correctness;
- workflow replay;
- artifact hashing/provenance;
- offline mode;
- partial-render recovery;
- final master integrity;
- human cinematic review.

## Evidence boundary

Source claims concerning specific model versions, memory requirements, generation speed, SVI, TTS/lip-sync quality, model superiority and 90-minute production time are **SOURCE-DERIVED / NOT VERIFIED LOCALLY**.
