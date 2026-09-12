# P113 Extension — Current Google Multimodal Adapter Matrix

## Parent
P113 — OmniVisual Prompt Compiler & Virtual Art Direction Engine MAX

## Trigger
Google AI stack infographic + current official Gemini API verification + 2026-09-12 capability corpus.

## Rule
The infographic is treated as a capability map. Exact model IDs, product names, pricing, free tiers and availability shown in static graphics are volatile and must not become hard-coded architectural truth.

Current official documentation shows active Gemini 3.x, Nano Banana 2 / Gemini 3.1 Flash Image, Nano Banana Pro / Gemini 3 Pro Image and Veo 3.1 families, while older preview identifiers can be deprecated. Therefore P113 requires a live model registry rather than static prompt templates.

## Adapter contract

```yaml
GoogleModelAdapter:
  provider: google
  model_id:
  product_surface:
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

## Google capability stack mapping

The supplied Google infographic is useful as a high-level workflow map spanning:

- Gemini / custom Gems;
- Google AI Studio;
- NotebookLM;
- Gemini Live;
- image generation/editing;
- Veo video generation;
- Firebase Studio / app building;
- Gemini in Sheets;
- YouTube-oriented Gemini workflows;
- Google educational / source-grounded workflows.

These should be modeled as **capability surfaces** that can be backed by different models and APIs over time, rather than as one monolithic Google model.

```text
USER INTENT
 ↓
GOOGLE CAPABILITY SURFACE
 ↓
LIVE MODEL / API REGISTRY
 ↓
INPUT + TOOL COMPATIBILITY
 ↓
POLICY / SAFETY
 ↓
GENERATION / TRANSFORMATION
 ↓
OUTPUT QA
 ↓
PROVENANCE
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

## Cross-provider abstraction

The broader AI-tool corpus contains image, video, audio, writing, presentation, design, coding and research providers. P113 should expose a provider-neutral intermediate representation so that a workflow can request a capability without embedding one vendor's UI or model name into the canonical scene graph.

```text
CANONICAL IR
   ↓
CAPABILITY REQUIREMENTS
   ↓
PROVIDER ADAPTERS
   ├── Google
   ├── OpenAI
   ├── Adobe
   ├── Midjourney
   ├── Runway
   ├── ElevenLabs
   └── other verified providers
```

Provider fallback is valid only when semantic capability, quality, modality, privacy, licensing and provenance requirements remain satisfied.

## Implications

- Nano Banana / image-generation knowledge remains an adapter, not the canonical IR.
- Veo belongs to the video adapter family and must expose current audio/control capabilities through verified metadata.
- Gemini reasoning models remain model-provider capabilities, not assumptions about all Google endpoints.
- Model shutdown/deprecation must invalidate stale adapter entries rather than silently falling back.
- Static tool rankings and free/paid labels are discovery metadata, not routing authority.
- A tool being listed in an infographic does not establish API access, current availability or account authorization.

## Status
`ARCHITECTURE ENHANCED — LIVE MODEL REGISTRY REQUIRED`
