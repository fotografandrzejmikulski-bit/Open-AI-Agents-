# P97 Extension — CineMatrix Google Flow / Veo Production Adapter

Date: 2026-09-12
Parent: P97 — Project MIDAS Recursive Multimedia Production Factory MAX
Classification: EXISTING PROJECT EXTENSION

## Mission
Add Google Flow as a provider-specific cinematic generation/editorial adapter while preserving CineMatrix Film World State, Shot IR, continuity, QA and provenance as canonical.

## Flow capability mapping

```text
CINEMATRIX SHOT IR
      ↓
GOOGLE FLOW ADAPTER
      ↓
MODEL/CAPABILITY CHECK
      ↓
TEXT / FRAMES / INGREDIENTS / REFERENCES
      ↓
VEO / GEMINI OMNI VIDEO GENERATION
      ↓
HISTORY / FRAME EXTRACTION / EXTENSION
      ↓
SCENE BUILDER
      ↓
CINEMATRIX QA
      ↓
ACCEPT / REGENERATE / ESCALATE
```

## Capability classes

- text-to-video;
- first-frame-to-video;
- first+last-frame-to-video where supported;
- ingredients/references;
- video editing where supported;
- clip extension where supported;
- image generation/editing;
- character/reference management;
- batch variation generation;
- scene assembly;
- version/history tracking.

Exact support is model-dependent and must be read from the live capability registry before routing. Current official documentation explicitly distinguishes Veo 3.1 Lite/Fast/Quality and Gemini Omni Flash capabilities.

## Film World State mapping

Google Flow's project/asset/character/scene organization becomes an external projection of CineMatrix state:

`CINEMATRIX PROJECT → FLOW PROJECT`

`CHARACTER ENTITY → FLOW CHARACTER/REFERENCE`

`SHOT REFERENCE → FLOW INGREDIENT/FRAME`

`SHOT OUTPUT → FLOW ASSET → CANDIDATE ARTIFACT`

Flow state never becomes the canonical CineMatrix state.

## Continuity contract

Flow's reusable ingredients, character references, saved frames, first/last frames, edit history and scene sequencing strengthen CineMatrix continuity handling.

For every Flow generation preserve, where available:
- source Shot IR version;
- character/location/reference IDs;
- Flow project/asset identity;
- model/version;
- active resolution;
- generation parameters;
- input/reference lineage;
- history/version lineage;
- output artifact hash after export;
- QA result.

## Cost-aware routing

Flow uses Google Flow/AI credits and current documentation instructs users to check active model, resolution and latest credit costs before generation.

P97 therefore adds:

`CAPABILITY MATCH → MODEL/RESOLUTION → CREDIT COST ESTIMATE → POLICY/BUDGET → GENERATE`

Credit availability is not authorization for unlimited production.

## Flow Agent benchmark

The Flow Agent is a benchmark for an agentic creative worker capable of brainstorming, storyboard planning, prompt refinement, model selection, generation, editing, batch generation and project-asset organization.

P97 may use the pattern as an external capability benchmark, but canonical cinematic decisions remain governed by CineMatrix's Director/Shot Planner and QA pipeline.

## Human approval benchmark

Current Flow Agent documentation includes a setting requiring confirmation before actions that consume AI credits. P97 adopts this as a UX benchmark for consequential creative operations:

`PLAN → SHOW COST/RISK → CONFIRM → GENERATE`

This is not treated as complete security; authorization, provenance and post-generation QA remain separate controls.

## SceneBuilder mapping

Flow's Scenebuilder provides an external reference architecture for sequence assembly: arrange clips, reorder, trim and preview a sequence before download.

CineMatrix retains its stronger canonical timeline/shot matrix and may use Flow scene assembly only as an adapter or export surface.

## Data boundary

Official Flow documentation describes collection of interactions, tool outputs, product-use information and feedback and exposes controls for data/project management. Sensitive CineMatrix assets must therefore be routed through an explicit provider/data-policy decision.

## Verification backlog

- live Flow model capability registry;
- Flow API/product-access verification;
- credit-cost accounting;
- ingredient/reference continuity tests;
- first/last-frame continuity tests;
- edit-history lineage tests;
- scene-builder export/readback;
- generated-output provenance;
- privacy/data-policy classification;
- Flow Agent confirmation-state tests;
- character/voice reference rights policy;
- provider outage/fallback behavior.

## Invariants

`FLOW PROJECT ≠ CANONICAL FILM WORLD STATE`

`FLOW ASSET ≠ ACCEPTED CINEMATIC ARTIFACT`

`MODEL SUPPORT ≠ UNIVERSAL FEATURE SUPPORT`

`GENERATION SUCCESS ≠ CINEMATIC CORRECTNESS`

`FLOW CREDIT ≠ AUTHORIZATION`

`AGENT CONFIRMATION ≠ COMPLETE SECURITY`

## Status

`ADAPTER-INTEGRATED / LIVE CAPABILITY VERIFICATION REQUIRED`
