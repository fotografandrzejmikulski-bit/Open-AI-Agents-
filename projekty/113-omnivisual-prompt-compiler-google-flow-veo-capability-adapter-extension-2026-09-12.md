# P113 Extension — Google Flow / Veo Live Capability Adapter

Date: 2026-09-12
Parent: P113 — OmniVisual Prompt Compiler & Virtual Art Direction Engine MAX
Classification: EXISTING PROJECT EXTENSION

## Mission
Extend the Google multimodal adapter matrix with the current Google Flow product surface and model-specific video feature matrix.

## Adapter contract

```yaml
provider: google
surface: google_flow
modality: image|video|multimodal
model_id:
resolution:
aspect_ratios: []
durations: []
text_to_video: false
first_frame_to_video: false
first_last_frame_to_video: false
ingredients_to_video: false
video_to_video: false
extend_video: false
image_generation: false
image_editing: false
audio_generation:
credit_profile:
account_requirements:
lifecycle:
verified_at:
source:
```

## Current feature-matrix principle

Google's official Flow documentation explicitly shows that capabilities vary by model. Current examples include Veo 3.1 Lite/Fast/Quality and Gemini Omni Flash with different support for text-to-video, frame conditioning, ingredients, video editing and extension.

Therefore P113 must route by capability compatibility rather than by product name alone.

## Canonical pipeline

`SHOT IR → CAPABILITY REQUIREMENTS → LIVE FLOW MODEL MATRIX → COMPILER → POLICY → GENERATION → QA → PROVENANCE`

## Reference-aware generation

Flow's ingredients, characters, uploaded assets, saved frames and first/last frames become adapter-level mechanisms for satisfying canonical reference requirements.

Reference identity must remain stable in the P113 IR even when the provider represents it as an asset, ingredient or character.

## Version lineage

Flow maintains edit history and prompts for edited assets and permits frames from prior generations to become future inputs. P113 should capture this as:

`PARENT_ARTIFACT → EDIT_VERSION → FRAME_DERIVATIVE → NEW_GENERATION`

This supports cinematic provenance and replay.

## Model lifecycle

P113 must treat model names, feature availability, resolution and credit cost as volatile metadata. The official Flow UI/documentation instructs users to inspect the active model, resolution and current credit costs before generation.

Stale adapter entries must fail closed or route to an independently verified compatible adapter; they must not silently assume equivalent capability.

## Status

`LIVE-REGISTRY-EXTENSION / CURRENT GOOGLE FLOW EVIDENCE INTEGRATED`
