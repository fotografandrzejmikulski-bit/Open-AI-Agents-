# Project 118 — NeXus StoryWorld Generator & Cinematic Narrative Runtime MAX

## Status
PROPOSED → ARCHITECTURE BASELINE — 2026-09-11

## Mission
Build a domain-specific multimodal storytelling runtime that converts an intent, prompt, photo or memory into a persistent **StoryWorld** containing characters, narrative state, visual identity, voices, music, scenes, video and publishable story artifacts.

P118 is not a general agent platform and not a photo editor. It is the narrative-production layer between P100 orchestration, P116 visual production, P117 mobile execution and the multimedia substrate.

## Why this is a distinct project

- **P100** owns general agent/model/MCP orchestration.
- **P116** owns forensic photographic analysis, identity lock, retouch and generative image production.
- **P117** owns the Android/mobile device and application boundary.
- **P97/P57** provide multimedia and multimodal infrastructure.
- **P118** owns the semantic continuity of a story world across text, images, voice, music, video and chapters.

## Source-derived trigger

The supplied `com.fableapp` package is directly identified by its manifest as Fable 3.3.0, target SDK 35, min SDK 24, approximately 160.65 MB, with a base APK and `armeabi-v7a`/`mdpi` splits. The manifest declares networking, billing, camera, notifications, media playback, messaging, ad-services and device/vendor integration permissions. These declarations are metadata, not proof of runtime behavior.

Public product documentation independently describes Fable as an AI story generator with personalized characters from photos, consistent story worlds, narration, dialogue, music, cinematic video, story editing, offline downloads, TV casting, multilingual operation and physical-book output. citeturn0search0turn0search1

The repository therefore adopts the **capability pattern**, not any proprietary implementation assumption.

## Canonical architecture

```text
                USER INTENT / PHOTO / MEMORY
                           ↓
                 STORYWORLD COMPILER
                           ↓
                STORYWORLD STATE GRAPH
                           ↓
        ┌──────────────┬───┴────┬──────────────┐
        ↓              ↓        ↓              ↓
    NARRATIVE       CHARACTER  VISUAL        VOICE
     ENGINE          REGISTRY  STYLE BIBLE   REGISTRY
        ↓              ↓        ↓              ↓
        └──────────────┴───┬────┴──────────────┘
                            ↓
                      CHAPTER / SCENE
                         TIMELINE
                            ↓
             ┌──────────────┼──────────────┐
             ↓              ↓              ↓
          IMAGE           AUDIO          VIDEO
          P116          VOICE/MUSIC     CINEMATIC
             └──────────────┼──────────────┘
                            ↓
                    CONTINUITY GATE
                            ↓
                 STORY ARTIFACT GRAPH
                            ↓
            LIBRARY / EXPORT / SHARE / PRINT
```

## 1. StoryWorld State

The central domain object is a versioned, provenance-bearing state graph:

```text
STORYWORLD
 ├─ world rules
 ├─ narrative tone
 ├─ character registry
 │   ├─ identity/reference assets
 │   ├─ appearance constraints
 │   └─ voice identity
 ├─ visual style bible
 ├─ sonic/music palette
 ├─ chapter graph
 │   └─ scene graph
 ├─ continuity constraints
 ├─ localization state
 ├─ generated artifacts
 ├─ rejected candidates
 └─ provenance / revisions
```

Every generation receives a constrained projection of this state and returns an artifact plus evidence. The UI is never the source of truth for continuity.

## 2. Character Continuity

P118 reuses P116's identity-lock doctrine.

Required checks:

- face/character identity;
- body and visual proportions;
- wardrobe and persistent attributes;
- age/appearance constraints where explicitly specified;
- species/object identity for non-human characters;
- voice identity;
- relationship consistency;
- chapter-to-chapter state transitions.

A generated frame is not accepted solely because it looks plausible in isolation.

## 3. Narrative Engine

The narrative layer maintains:

- premise;
- goals/conflicts;
- character motivations;
- world rules;
- chapter objectives;
- scene beats;
- dialogue constraints;
- pacing;
- moral/educational objectives when requested;
- continuity memory.

It must support both guided generation and explicit operator control.

## 4. Multimodal production adapters

P118 delegates rather than duplicates specialist systems:

- `story.image.create` → P116/provider-neutral image adapter;
- `story.image.edit` → P116 controlled edit graph;
- `story.voice.create` → voice provider capability;
- `story.music.create` → music capability;
- `story.video.create` → cinematic media pipeline;
- `story.chapter.extend` → narrative engine;
- `story.artifact.export` → publication/export pipeline.

All adapters require explicit side-effect declarations, budgets and verification.

## 5. Cinematic scene model

Each scene should carry:

- shot list;
- camera/framing intent;
- character blocking;
- environment;
- lighting/mood;
- dialogue/narration;
- music/SFX cues;
- transition type;
- duration target;
- continuity references;
- source and generated asset IDs.

This creates a structured bridge between story generation and cinematic video production instead of treating video as an opaque final-generation call.

## 6. Quality gates

```text
NARRATIVE VALIDITY
      ↓
CHARACTER CONTINUITY
      ↓
VISUAL CONTINUITY
      ↓
AUDIO / VOICE CONTINUITY
      ↓
SCENE / TEMPORAL CONSISTENCY
      ↓
LOCALIZATION CHECK
      ↓
SAFETY / CONSENT CHECK
      ↓
MEDIA QUALITY
      ↓
EXPORT / PUBLISH
```

Failed gates prevent silent promotion and preserve the rejected artifact as evidence when policy permits.

## 7. Mobile integration

P117 supplies:

- camera/photo import;
- mobile screen observation;
- app/UI observation;
- audio/video playback readback;
- download/export verification;
- casting-state observation where exposed;
- offline/online state;
- package/application metadata.

P117 remains the device boundary. P118 remains the story domain.

## 8. P100 integration

P100 owns orchestration:

```text
USER INTENT
   ↓
P100 CONTEXT BROKER
   ↓
P118 STORYWORLD PLAN
   ↓
CAPABILITY AUTHORIZATION
   ↓
P116 / VOICE / MUSIC / VIDEO / P117
   ↓
READBACK
   ↓
P118 CONTINUITY + QUALITY GATE
   ↓
ARTIFACT LEDGER
```

OCN agents may operate inside the workflow, but no agent receives unrestricted provider or device authority.

## 9. Privacy / consent

Because the domain can contain family photos, children's material and personal or cloned voices, P118 requires:

- explicit consent state for real-person likeness;
- explicit voice-creation/voice-cloning authorization;
- child-media policy controls;
- provenance for reference media;
- deletion and retention policy;
- provider disclosure boundary;
- export/download controls;
- spending/token authorization;
- background-processing visibility.

## 10. Internationalization

The story model must be locale-aware rather than translating only UI strings. Localization covers:

- narrative text;
- character dialogue;
- pronunciation/voice selection;
- captions;
- typography and text layout;
- cultural adaptation rules;
- metadata;
- export formats.

PL/EN are mandatory repository product baselines; the architecture supports additional locales.

## 11. UX architecture

System chrome inherits the NeXus luxury design system. Story content may have its own visual art direction.

```text
NE XUS SYSTEM CHROME
        ↓
STORYWORLD WORKSPACE
 ├─ Story
 ├─ Characters
 ├─ Scenes
 ├─ Voices
 ├─ Music
 ├─ Video
 ├─ Continuity
 └─ Library
```

The Fable icon is treated as a product-art-direction reference, not as a replacement for the system design language.

## 12. Verification program

1. StoryWorld schema validation.
2. Character registry round-trip tests.
3. Continuity regression across 10+ generated scenes.
4. Visual identity-lock regression using P116.
5. Voice identity/consent state tests.
6. Narrative memory and chapter continuation tests.
7. Scene timeline/audio synchronization tests.
8. Localization regression tests.
9. Media provenance and artifact lineage tests.
10. Export/download/readback verification on P117.
11. Offline/reconnect recovery.
12. Provider failure and partial-generation recovery.
13. Budget/token authorization tests.
14. Prompt-injection tests across imported text, metadata and media-derived instructions.
15. End-to-end intent → StoryWorld → scene → media → quality gate → export replay.

## Definition of Done

P118 advances beyond architecture baseline when:

- StoryWorld state is versioned and inspectable;
- character and visual continuity gates are reproducible;
- multimodal artifacts share common provenance;
- narrative, visual and audio state can be revised without destroying prior evidence;
- P100 orchestration is capability-bounded;
- P116 image production integrates without duplicating its core;
- P117 mobile workflows have authoritative readback;
- privacy/consent controls are enforced for personal media and voices;
- PL/EN localization passes;
- failure and partial-generation states are recoverable and auditable.

## Evidence classification

- uploaded manifest: **OBSERVED / DIRECTLY PARSED SOURCE**;
- uploaded icon: **OBSERVED VISUAL ASSET**;
- APK internals: **NOT ASSERTED**;
- public Fable product capabilities: **EXTERNAL-VERIFIED CONTEXT**;
- P118 architecture: **SYNTHESIS / IMPLEMENTATION TARGET**.

## Dependencies

P40, P57, P72, P97, P100, P114, P116, P117.
