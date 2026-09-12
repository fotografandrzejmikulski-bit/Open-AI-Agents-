# P113 Extension — CineMatrix Shot Matrix / Cinematic Compilation

## Parent
P113 — OmniVisual Prompt Compiler & Virtual Art Direction Engine MAX

## Contribution
CineMatrix strengthens P113 with a film-specific intermediate representation between screenplay semantics and executable image/video workflows.

## Canonical shot object

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

## Compiler role

`SCREENPLAY → SCENE GRAPH → SHOT MATRIX → MODEL-SPECIFIC PAYLOAD → VALIDATION → GENERATION → QA`

The compiler must preserve semantics, entity identity, camera/light intent, temporal constraints and provenance. It must not merely concatenate prompt keywords.

## Entity continuity

Character, location and reference-image IDs remain stable across shots. Appearance, action, voice and scene role are represented separately. Reference assets and generated descendants retain lineage.

## Film QA contract

- camera/lens coherence;
- lighting continuity;
- character/entity continuity;
- start/end-frame continuity;
- action semantics;
- temporal consistency;
- color/material consistency;
- model-adapter conformance;
- provenance completeness;
- replayability.

## Boundary

P113 compiles creative intent into structured generation specifications. P97 owns the production loop and render orchestration. P114 owns persistent semantic memory/retrieval. P100 owns desktop/runtime security and release controls.

## Evidence

The CineMatrix report is source-derived architecture. Specific model versions, capabilities and performance remain unverified until current documentation or local benchmarks establish them.
