# Project 113 — OmniVisual Prompt Compiler & Virtual Art Direction Engine MAX

## Status
PROPOSED → ARCHITECTURE BASELINE

## Mission
Build a model-agnostic visual prompt compiler and virtual art-direction engine that translates natural-language creative intent into structured, provenance-bearing image/video specifications using photographic optics, lighting, composition, scenography, historical visual grammar and model-specific syntax.

## Distinct boundary
- **P107 — LUMEN Documentary Photography Intelligence Lab** owns photographic intelligence, documentary/street/photojournalism semantics, visual history, optics and photographic-language research.
- **P97 — Project MIDAS Recursive Multimedia Production Factory** owns recursive multimedia production, scene planning, rendering and production QA.
- **P113** owns the operational compilation layer between creative intent and executable generation specifications.

## Source-derived baseline
The supplied visual corpus describes a Virtual Art Director / Prompt Engineer, structured scene schemas, Nano Banana model variants, photographic optics, lighting, posing, negative space, environment and atmospheric controls, and model-specific prompt engineering. It also describes moderation-bypass strategies; those are explicitly excluded from operational capability and retained only as defensive evaluation context.

## Canonical pipeline
```text
HUMAN CREATIVE INTENT
 ↓
INTENT PARSER
 ↓
VISUAL SEMANTICS / PHOTOGRAPHIC KNOWLEDGE
 ↓
SCENE GRAPH
 ├── SUBJECTS / ENTITIES
 ├── ENVIRONMENT
 ├── CAMERA / LENS
 ├── LIGHTING
 ├── COMPOSITION
 ├── COLOR / MATERIAL
 ├── MOTION / TIMELINE
 └── STYLE / HISTORICAL GRAMMAR
 ↓
MODEL-SPECIFIC COMPILER
 ├── IMAGE MODELS
 ├── VIDEO MODELS
 └── LOCAL GENERATORS
 ↓
VALIDATOR / POLICY GATE
 ↓
GENERATION ADAPTER
 ↓
OUTPUT QA
 ↓
PROVENANCE / RECIPE / REPLAY RECORD
```

## Photographic compiler vocabulary
The source corpus supports explicit representation of:
- focal length, aperture, depth of field and sensor format;
- key/fill/rim/background light;
- Rembrandt, split, clamshell and cross-lighting;
- contrast, shadow geometry and atmospheric scattering;
- camera/lens rendering characteristics;
- film/emulsion/color and optical imperfections;
- posing, contrapposto, S-curve and negative space;
- architecture, scenography and environmental context.

The compiler should preserve physical coherence rather than merely concatenate keywords.

## Structured scene schema
A canonical intermediate representation should contain:
- `metadata`
- `entities`
- `environment`
- `camera`
- `lighting`
- `composition`
- `materials`
- `action`
- `timeline`
- `render_constraints`
- `negative_constraints`
- `provenance`
- `validation`

The schema is an internal representation, not a claim that any vendor's undocumented syntax is authoritative.

## Entity and reference-image registry
P113 should support stable local entity IDs and explicit reference assets. Appearance, action, voice and scene roles are represented separately to reduce accidental identity drift. Reference-image lineage is retained in the provenance record.

## Model adapters
Adapters translate the canonical scene representation into model-specific payloads. The adapter contract records model/version, supported controls, estimated cost, resolution, context/reference limits and known failure modes. No undocumented endpoint or credential-extraction behavior is required.

## Art-direction intelligence
The Virtual Art Director layer evaluates:
1. narrative intention;
2. visual hierarchy;
3. photographic plausibility;
4. lighting consistency;
5. material/texture coherence;
6. character/entity continuity;
7. composition and negative-space requirements;
8. model-specific prompt effectiveness;
9. safety/policy constraints;
10. reproducibility.

## Security / policy boundary
The source describes attempts to defeat image-safety gates using euphemism, staged generation, classifier/interface manipulation and hidden technical pathways. P113 must not implement such bypasses. Instead, it may model them as adversarial test cases for P108.

Explicitly excluded:
- CAPTCHA bypass;
- token/session extraction;
- hidden-endpoint abuse;
- watermark removal/evasion;
- policy circumvention recipes.

## Verification plan
- schema round-trip tests;
- prompt compiler determinism where intended;
- semantic preservation tests;
- camera/light consistency tests;
- entity consistency across image/video sequences;
- model-adapter conformance tests;
- negative/policy test suite;
- provenance completeness;
- cost/latency accounting;
- replayability;
- regression corpus;
- human expert photographic review.

## Dependencies / lineage
P07, P19, P57, P72, P97, P100, P107, P108, P111.

## Primary sources
- `Tworzenie Persony AI do Generowania Promptów Obraz...PDF`
- `Tworzenie Persony AI do Generowania Promptów Obraz..(1).PDF`
- `Tworzenie Promptów dla AI Fotografii.PDF`
- `Tworzenie Promptów do Aktu Artystycznego.PDF`
