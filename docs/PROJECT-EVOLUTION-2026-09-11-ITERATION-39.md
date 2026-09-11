# Project Evolution — Iteration 39 — Fable StoryWorld Corpus

## Trigger

New Android package corpus for `com.fableapp` plus manifest, split APKs and icon.

## Directly observed

- Fable 3.3.0;
- version code 189;
- min SDK 24;
- target SDK 35;
- 160,653,317-byte bundle;
- base APK + `armeabi-v7a` + `mdpi` splits;
- declared network, billing, camera, notification, media playback, messaging and ad/attribution permissions. fileciteturn73file0L1-L1

APK internals beyond the manifest are not asserted.

## External capability verification

Current public product descriptions identify Fable as an AI story generator with personalized character creation from photos, story memory/continuity, narration, dialogue, music, cinematic video, image editing, multilingual support and story publication/export patterns. citeturn0search0turn0search1

These facts are external product context, not proof of the uploaded APK's internal implementation.

## New knowledge

The key reusable concept is **StoryWorld State**: a persistent, provenance-bearing graph connecting narrative rules, characters, visual style, voices, music, scenes, chapters, continuity constraints, localization and generated artifacts.

## Portfolio decision

The corpus warrants a new project:

**P118 — NeXus StoryWorld Generator & Cinematic Narrative Runtime MAX**

Reason: the domain is materially distinct from P116 photographic production, P117 mobile execution and P100 general orchestration, while composing them.

## Existing-project upgrades

### P100
Added StoryWorld capability-broker/orchestration adapter and selective-context requirements.

### P116
Added Character Reference Contract and reusable visual-continuity bridge.

### P117
Added multimodal story-production apps as a mobile verification reference class and strengthened media-generation readback requirements.

## Security doctrine

Declared Android permissions remain metadata, not authorization. Personal photos, family memories and voices require provenance/consent state. UI events remain non-authoritative; consequential generation/export/publication requires readback and verification.

## Verification state

- Manifest evidence: directly observed.
- Icon: directly observed visual asset.
- APK internals: not decoded/claimed in this iteration.
- Public product capabilities: externally verified.
- P118 architecture: synthesis / implementation target.

## Root README

`readme_sync: PENDING` — root README remains intentionally untouched until a complete, non-destructive reconstruction/update can be performed.
