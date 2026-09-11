# P100 — Iteration 39: StoryWorld Orchestration Adapter

## Trigger

The Fable corpus demonstrates a product pattern in which one user intent can span persistent narrative context, character identity, image generation, voice, music, video, editing and publication.

## P100 upgrade

P100's capability broker should expose a **StoryWorld domain adapter** rather than implementing story semantics directly.

Required orchestration objects:

- `storyworld.create`
- `storyworld.read`
- `storyworld.plan_chapter`
- `storyworld.plan_scene`
- `storyworld.generate_media`
- `storyworld.revise`
- `storyworld.continuity_check`
- `storyworld.export`

Every operation remains capability-scoped and requires explicit side-effect metadata, budget and verification method.

## Context-broker requirement

The StoryWorld State should be selectively projected into each model/agent call. P100 must avoid indiscriminately injecting the entire story history.

```text
STORYWORLD STATE
      ↓
SEMANTIC CONTEXT BROKER
      ↓
TASK-SPECIFIC PROJECTION
      ↓
MODEL / OCN AGENT
      ↓
CANDIDATE ARTIFACT
      ↓
DOMAIN QUALITY GATE
```

## Continuity as verification

P100 should treat character, narrative, visual and audio continuity results as structured observations. A model's statement that an artifact is consistent is not authoritative evidence.

## Security

Personal photos, memories and voice references are sensitive user-controlled data. The orchestration layer must carry consent/provenance metadata and must not silently broaden a capability scope from `storyworld.read` to media export, voice creation, publication or spending.

## Boundary

P100 = orchestration/control plane.
P118 = story domain.
P116 = photographic/visual continuity specialist.
P117 = mobile/device boundary.
