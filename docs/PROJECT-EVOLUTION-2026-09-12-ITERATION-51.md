# Project Evolution — Iteration 51

**Date:** 2026-09-12
**Corpus:** CineMatrix architectural report with 47 cited sources

## Objective
Evaluate the CineMatrix proposal against the existing portfolio and absorb all non-redundant architectural knowledge into the appropriate project boundaries.

## Decision

**NO NEW NUMBERED PROJECT.** CineMatrix does not introduce a new architectural domain. Its core responsibility — autonomous multimedia production — is already owned by P97. What is new is a concrete local long-form film specialization, which is recorded as an extension rather than duplicated as another production-factory project.

## Portfolio impact

### P97 — MIDAS
Highest impact. Added the CineMatrix local-film specialization: screenplay → Film World State → director/shot planning → multimodal generation → VLM QA → bounded regeneration → master.

Added VRAM-aware scheduling, shot-level continuity, audio artifact separation and long-form continuity verification.

### P113 — OmniVisual Prompt Compiler
Added a film-specific shot matrix containing scene/sequence/entity identity, action, dialogue, emotion, camera, lighting, reference frames, start/end frames, audio, duration, FPS, model versions, validation and provenance.

### P114 — Memory / RAG
Added a concrete film-memory workload for retrieving character, costume, prop, location, event, dialogue and continuity state with provenance and stable identity.

### P100 — NeXus AI Code
Added a desktop-local runtime profile: Electron/React → FastAPI → policy/job layer → ComfyUI/local model adapters → GPU/CPU/disk → readback/verification.

## Canonical architecture

```text
BRIEF
 ↓
STORY / WORLD STATE
 ↓
SHOT MATRIX
 ↓
LOCAL MODEL ROUTING
 ↓
GENERATION
 ↓
MULTIMODAL QA
 ↓
BOUNDED REGENERATION / ESCALATION
 ↓
EDIT / MIX / MASTER
 ↓
PROVENANCE / REPLAY
```

## New invariants

```text
RENDER SUCCESS ≠ SEMANTIC CORRECTNESS
MODEL CAPABILITY ≠ RIGHTS TO USE
VOICE CLONING CAPABILITY ≠ VOICE AUTHORIZATION
LOCAL ENDPOINT AVAILABLE ≠ WORKFLOW CORRECT
VRAM CAPACITY CLAIM ≠ BENCHMARK EVIDENCE
GENERATED FRAME ≠ CONTINUITY VERIFIED
```

## Evidence boundary

The supplied report is source-derived architecture. Its model-version, VRAM, model-size, performance, SVI, TTS/lip-sync and 90-minute-film timing claims are not treated as verified current facts. They require current documentation and/or local benchmarks.

## Repository writes

- `docs/knowledge-base/2026-09-12-corpus-cinematrix-local-ai-film-studio.md`
- `projekty/97-cinematrix-local-film-studio-extension.md`
- `projekty/113-omnivisual-prompt-compiler-cinematrix-shot-matrix-extension.md`
- `projekty/114-cinematrix-film-world-state-rag-extension.md`
- `projekty/100-cinematrix-desktop-local-runtime-extension.md`
- this evolution record
- portfolio delta
