# P113 Extension — Current Google Multimodal Adapter Matrix

## Parent
P113 — OmniVisual Prompt Compiler & Virtual Art Direction Engine MAX

## Trigger
Google AI stack infographic + current official Gemini API verification.

## Rule
The infographic is treated as a capability map. Exact model IDs in the image are volatile and must not become hard-coded architectural truth.

Current official documentation shows active Gemini 3.x, Nano Banana 2 / Gemini 3.1 Flash Image, Nano Banana Pro / Gemini 3 Pro Image and Veo 3.1 families, while older preview identifiers can be deprecated. Therefore P113 requires a live model registry rather than static prompt templates.

## Adapter contract

```yaml
GoogleModelAdapter:
  provider: google
  model_id:
  modality: text|image|video|audio|multimodal
  generation_mode:
  input_types: []
  output_types: []
  resolution:
  context_limits:
  reference_limits:
  tool_capabilities: []
  grounding:
  audio:
  cost_profile:
  latency_profile:
  lifecycle: preview|ga|deprecated|shutdown
  verified_at:
  source:
```

## Pipeline

```text
CANONICAL SCENE GRAPH
 ↓
CAPABILITY MATCH
 ↓
LIVE MODEL REGISTRY
 ↓
MODEL-SPECIFIC COMPILER
 ↓
POLICY / SAFETY GATE
 ↓
GENERATION
 ↓
OUTPUT QA
 ↓
PROVENANCE / MODEL VERSION RECORD
```

## Implications
- Nano Banana / image-generation knowledge remains an adapter, not the canonical IR.
- Veo belongs to the video adapter family and must expose current audio/control capabilities through verified metadata.
- Gemini reasoning models remain model-provider capabilities, not assumptions about all Google endpoints.
- Model shutdown/deprecation must invalidate stale adapter entries rather than silently falling back.

## Status
`ARCHITECTURE ENHANCED — LIVE MODEL REGISTRY REQUIRED`
