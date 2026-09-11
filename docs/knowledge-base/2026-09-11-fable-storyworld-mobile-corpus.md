# Knowledge Base — Fable Storyworld / Mobile Multimodal Corpus

## Intake

Date: 2026-09-11
Source package: `com.fableapp`
Source artifact: uploaded `manifest.json`, base APK and two split APKs, plus application icon.

## Evidence classification

- `manifest.json`: **OBSERVED / DIRECTLY PARSED SOURCE**.
- APK binaries: **UNTRUSTED INPUT / INTERNALS NOT ASSERTED**; this iteration does not claim decoded DEX/resource/native implementation.
- Icon: **OBSERVED VISUAL ASSET**; useful for brand/UI analysis, not functional evidence.
- Public Google Play/App Store descriptions: **EXTERNAL-VERIFIED PRODUCT CONTEXT**.
- Architecture below: **SYNTHESIS / IMPLEMENTATION TARGET**, not a claim about Fable's internal implementation.

## 1. Direct package anatomy

The supplied manifest identifies:

- package: `com.fableapp`;
- application name: `Fable`;
- version code: `189`;
- version name: `3.3.0`;
- min SDK: `24`;
- target SDK: `35`;
- declared bundle size: `160,653,317` bytes;
- base APK: `com.fableapp.apk`;
- split APKs: `config.armeabi_v7a.apk`, `config.mdpi.apk`;
- total split configurations: `config.armeabi_v7a`, `config.mdpi`.

The manifest declares Internet, in-app billing, notifications, camera, storage, connectivity/Wi-Fi, wake lock, foreground media playback, phone state, Firebase Cloud Messaging receive, Android ad-services attribution/topic/custom-audience permissions and multiple launcher-badge/vendor permissions. These are permission declarations only; they do not prove runtime behavior or data use.

## 2. Product capability pattern

Current public product descriptions identify Fable as an AI story generator that can turn a prompt, photo, family memory or idea into a personalized story world with illustrations, persistent characters, narration, dialogue, music and video. They also describe character creation from photos, custom/designed voices, story memory across chapters, cinematic camera angles, editing/Brush Mode, offline downloads, TV casting, multilingual operation and physical-book ordering. citeturn0search0turn0search1

The architectural significance is not the individual feature list but the **cross-modal continuity contract**:

```text
USER INTENT / MEMORY / PHOTO
            ↓
      STORY WORLD MODEL
            ↓
   CHARACTER + STYLE BIBLE
            ↓
       CHAPTER PLAN
       ↙    ↓     ↘
    IMAGE  VOICE   MUSIC
       \    ↓     /
        SCENE MEDIA
            ↓
      CINEMATIC VIDEO
            ↓
   STORYBOOK / AUDIO / VIDEO
            ↓
       LIBRARY / SHARE
```

## 3. New canonical concept — StoryWorld State

A story generator should not treat each image, paragraph, voice clip or video scene as an independent generation. The canonical state should include:

- story identity;
- world rules;
- character registry;
- character identity/reference assets;
- visual style bible;
- voice identity registry;
- music/sonic palette;
- narrative tone;
- chapter/scene graph;
- continuity constraints;
- provenance of generated assets;
- revisions and rejected candidates;
- localization state;
- safety/consent policy for real-person likeness and voice.

This extends the repository's existing identity-lock and bitemporal-memory patterns from photography and agentic systems into narrative production.

## 4. Continuity is a first-class quality gate

The strongest reusable insight is that multimodal generation requires a shared state model. A scene should be accepted only when the generated asset remains compatible with the active StoryWorld State.

Recommended verification dimensions:

1. character identity consistency;
2. wardrobe/appearance continuity;
3. environment/style continuity;
4. narrative continuity;
5. voice identity consistency;
6. temporal/chapter ordering;
7. music/dialogue synchronization;
8. localization consistency;
9. asset provenance;
10. user-requested constraints.

This should reuse P116's identity/structure lock rather than creating a second unrelated visual-consistency subsystem.

## 5. Cross-project implications

### P100 — NeXus AI Code OMEGA-X

Add a StoryWorld domain adapter to the general capability broker. P100 should orchestrate intent, context retrieval, model routing, agent delegation, generation jobs and verification, while remaining provider-neutral.

### P116 — WDA Photo Agent MAX

Extend photographic identity-lock concepts into character reference preparation, scene continuity and controlled visual editing. P116 remains the photo-production specialist; it should not become the narrative orchestrator.

### P117 — NeXus Mobile Multimodal Agent Runtime MAX

Treat Fable-like applications as a reference class for mobile multimodal production. P117 must support observation and verification of story creation, image editing, audio/video playback, downloads, casting and media export without assuming that a UI click equals successful generation.

### P97 / P57

Reuse multimedia lineage, multimodal perception and media quality gates rather than duplicating them inside the story runtime.

## 6. Security and privacy requirements derived for NeXus

The product pattern involves potentially sensitive family photos, personal memories, children's content and custom voices. Therefore a NeXus implementation must add explicit controls for:

- real-person likeness consent;
- voice creation/voice-cloning consent;
- child/family media handling;
- media retention and deletion;
- generated-asset provenance;
- offline/export boundaries;
- paid-generation authorization and quota;
- notification and background-processing scope;
- third-party analytics/ad attribution separation;
- provider-side data handling disclosure.

The package's billing, ad-services and messaging permissions strengthen the need for explicit capability accounting, but do not establish that each capability is actively used.

## 7. Design-system implication

The uploaded icon uses a bright illustrated, storybook-oriented visual language. This should not replace the NeXus obsidian/luxury shell. Instead, the architecture should separate:

- **system chrome** — NeXus design system;
- **storyworld canvas** — user-selected narrative art direction;
- **brand/iconography** — product-specific assets.

This prevents generated story aesthetics from leaking into system-level controls.

## 8. Project decision

The corpus is sufficient to justify a distinct project: **P118 — NeXus StoryWorld Generator & Cinematic Narrative Runtime MAX**.

Reason: the combined requirements form a domain-specific runtime spanning persistent story state, character/visual identity, narrative planning, image generation, voice, music, video, localization, editing and publication. This is materially broader than P116 photographic production and materially different from P100 general orchestration, while depending on P117 for mobile execution.

## 9. Explicit unknowns

Not established from the uploaded artifacts:

- internal DEX architecture;
- native libraries;
- embedded ML models;
- exact provider APIs;
- backend endpoints;
- runtime network graph;
- cryptographic/signature state;
- exact implementation of character/voice consistency;
- actual use of every declared permission.

No claim about these internals should enter the repository as fact until directly observed or independently verified.
