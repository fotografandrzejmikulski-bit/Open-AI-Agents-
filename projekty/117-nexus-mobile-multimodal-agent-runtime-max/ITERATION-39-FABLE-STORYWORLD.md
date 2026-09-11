# P117 — Iteration 39: Fable StoryWorld Mobile Reference

## Trigger

New `com.fableapp` Android package corpus: manifest, base APK, `armeabi-v7a` split, `mdpi` split and icon.

## Direct evidence

The supplied manifest identifies Fable 3.3.0, package `com.fableapp`, version code 189, min SDK 24, target SDK 35 and a 160,653,317-byte bundle with one base APK and two configuration splits. It declares networking, billing, camera, notifications, media playback foreground service, storage, messaging and advertising/attribution-related permissions. fileciteturn73file0L1-L1

No internal DEX/native/resource behavior is asserted from the uploaded binaries in this iteration.

## New P117 reference class

Fable adds a new mobile application category to the P117 test matrix: **multimodal story-production app**.

P117 should be able to observe and verify workflows involving:

- photo/character input;
- story-generation progress;
- image editing;
- audio/narration playback;
- music playback;
- video/story playback;
- offline downloads;
- export/share state;
- casting where platform-visible;
- billing/consumable authorization state where explicitly exposed.

Public product documentation is used only as external capability context; it is not evidence of the uploaded binary's internal implementation. citeturn0search0turn0search1

## Architectural upgrade

P117's mobile verification model now explicitly covers **media-generation applications**, not only photo editors and navigation apps.

```text
MOBILE OBSERVE
      ↓
APP / STORY STATE
      ↓
GENERATION PROGRESS
      ↓
MEDIA READBACK
      ↓
CONTINUITY / ARTIFACT CHECK
      ↓
EXPORT / PLAYBACK VERIFY
```

The existing doctrine remains mandatory:

`OBSERVE → PLAN → AUTHORIZE → ACT → READBACK → VERIFY`.

## Security implications

Declared camera/storage/notifications/media/background/ad/billing permissions must be represented as typed capabilities. A manifest permission is never treated as authorization for an agent to exercise the capability.

Fable-like family/character workflows also strengthen P117 requirements for consent-aware media handling, especially when camera images or personal voices are involved.

## Status

P117 remains the mobile/device boundary. The new narrative domain is separated into P118 rather than being absorbed into P117.
