# Project 117 — NeXus Mobile Multimodal Agent Runtime MAX

## Status
PROPOSED → ARCHITECTURE BASELINE → PACKAGE-ANATOMY EVIDENCE — 2026-09-11

## Mission
Build the mobile execution substrate for the NeXus ecosystem: a guarded Android capability plane combining device perception, camera/audio input, screen/UI semantics, touch/gesture actuation, mobile-world context, static APK/XAPK/BAPK inspection and authoritative verification.

## Why this is a distinct project

- **P100** owns the NeXus AI developer environment and general agent/model/MCP control plane.
- **P116** owns photographic production: image analysis, identity lock, retouch/generative editing and quality gates.
- **P117** owns the Android/mobile boundary between agents and real devices/apps.

P117 therefore becomes the mobile equivalent of the desktop/world-control boundary, without absorbing domain-specific photo production or general developer orchestration.

## Source-derived inputs

The NeXus corpus specifies camera and desktop vision, microphone/STT/TTS, mouse/keyboard hands, Rust + Zenoh low-latency transport, Android automation, MCP and multi-panel agent control. The new binary corpus adds APK/XAPK/BAPK artifacts from visual-editing, AI and navigation-oriented applications. The uploaded binaries are treated as untrusted research inputs.

A newly supplied `manifest.json` provides directly observed package anatomy for a Touch Retouch 4.23 XAPK: package `com.touch.retouch.removeobject.photo`, version code 58, min SDK 22, target SDK 30, total bundle size 6,511,836 bytes, with a base APK plus language/resource splits and an `arm64_v8a` ABI split. The manifest also declares camera, storage, internet/network, wake-lock and boot-completed permissions. fileciteturn70file0L1-L1

This manifest is stronger evidence than the previous filename-only observation and is now the canonical package-anatomy witness for this iteration. The individual split APKs are still treated as untrusted binary artifacts; their internal DEX/resource/native contents are not asserted without direct decoding.

Public documentation for TomTom 9.41.0 provides an external example of a split Android navigation bundle with a base APK, architecture splits and DPI splits, plus location, traffic, Bluetooth, Android Auto and overlay capabilities. This is architectural comparison material, not a claim about the exact uploaded binary.

Public descriptions of Android retouch applications provide external feature-pattern evidence for object removal, people/background removal, watermark cleanup, tracking, cutout/paste/clone and enhancement workflows. These patterns inform UX requirements without copying proprietary implementation.

## Canonical architecture

```text
                    OPERATOR / AGENT
                           ↓
                 MOBILE INTENT LAYER
                           ↓
                CONTEXT + POLICY BROKER
                           ↓
        ┌──────────────────┼──────────────────┐
        ↓                  ↓                  ↓
    DEVICE SENSE       APP INSPECT        WORLD CONTEXT
 camera / mic /       APK/XAPK/BAPK       location / time /
screen / UI tree     manifest / DEX      connectivity / route
        ↓                  ↓                  ↓
        └──────────────────┼──────────────────┘
                           ↓
                    ACTION PLANNER
                           ↓
                  AUTHORIZATION GATE
                           ↓
               SANDBOXED MOBILE ACTUATOR
                           ↓
             TOUCH / GESTURE / APP ACTION
                           ↓
                 AUTHORITATIVE READBACK
                           ↓
                 POSTCONDITION VERIFY
                           ↓
                  ARTIFACT / EVENT LEDGER
```

## 1. Mobile Capability Plane

Capabilities are typed and independently authorized:

- `mobile.device.inspect`
- `mobile.screen.observe`
- `mobile.camera.observe`
- `mobile.audio.observe`
- `mobile.ui.inspect`
- `mobile.app.launch`
- `mobile.touch.act`
- `mobile.gesture.act`
- `mobile.media.import`
- `mobile.media.export`
- `mobile.context.read`
- `mobile.location.read`
- `mobile.package.inspect`
- `mobile.package.metadata`
- `mobile.readback.verify`

Each capability declares scope, side effects, approval policy, budget and verification method.

## 2. Android package intelligence

Static inspection pipeline:

```text
INPUT BINARY
    ↓
TYPE DETECTION
APK / XAPK / APKS / BAPK / TEMP CONTAINER
    ↓
CONTAINER INVENTORY
    ↓
MANIFEST / RESOURCE / DEX / NATIVE LIBRARY METADATA
    ↓
SIGNATURE + HASH RECORD
    ↓
PERMISSION / COMPONENT / ABI / SPLIT MAP
    ↓
STATIC RISK REPORT
    ↓
READ-ONLY ARTIFACT LEDGER
```

### Package split model learned from the new manifest

The inspection model must distinguish at least three split classes:

1. **Functional/base package** — the primary application APK.
2. **Locale/resource splits** — language or locale-specific APKs such as `config.ru`, `config.my`, `config.zh`, `config.vi`, `config.ko`, `config.th`, `config.tr`, `config.pt` and other declared locales.
3. **Device-configuration splits** — ABI and density variants such as `config.arm64_v8a` and `config.xxxhdpi`.

The package ledger therefore records a normalized relation:

```text
XAPK
 ├── BASE
 ├── LOCALE SPLITS[*]
 ├── ABI SPLITS[*]
 └── DENSITY / DEVICE SPLITS[*]
```

The exact uploaded manifest declares 20 split configurations, including locale, ABI and density variants, and identifies the base APK separately. fileciteturn70file0L1-L1

This becomes a P117 design requirement: package intelligence must reason about the **bundle graph**, not treat every APK file as an independent application.

The parser must never execute package code during inspection.

## 3. Mobile perception

P117 unifies:

- screenshot and screen-region observation;
- accessibility/UI-tree semantics where the platform exposes them;
- camera frames;
- microphone/audio events;
- app identity and foreground state;
- network/connectivity state;
- location/time context when explicitly authorized;
- external-display/car integration adapters.

Sensor observations carry timestamp, source, confidence and freshness metadata.

## 4. Safe actuation

All consequential actions use:

`OBSERVE → PLAN → AUTHORIZE → ACT → READBACK → VERIFY`.

Examples:

- tapping a button is not proof that the action succeeded;
- launching an application is not proof that its target screen opened;
- submitting a form is not proof that the server accepted it;
- exporting an image is not proof that the resulting file matches the requested operation.

## 5. P116 integration

P117 supplies the mobile execution substrate to P116:

```text
P117 CAMERA / GALLERY / SCREEN
            ↓
P116 VISUAL ANALYSIS
            ↓
P116 IDENTITY + STRUCTURE LOCK
            ↓
P116 EDIT GRAPH
            ↓
P117 MOBILE RENDER / EXPORT ADAPTER
            ↓
P116 QUALITY GATE
            ↓
P117 FILE + UI READBACK
```

The photo runtime remains responsible for image semantics and production quality; P117 remains responsible for device/app boundaries.

## 6. P100 integration

P100 consumes P117 through the capability broker rather than direct unrestricted device control.

Required integration points:

- model/agent intent → mobile plan;
- OCN agent or swarm → bounded mobile capability request;
- MCP → typed mobile tools;
- DGM candidate code → sandboxed test device only;
- telemetry → authoritative mobile execution metrics;
- artifact ledger → screenshots, package metadata and postcondition evidence.

## 7. Mobile-world context graph

The runtime maintains a bitemporal/event-oriented context model:

```text
DEVICE
 ├─ APP
 ├─ SCREEN
 ├─ USER INTENT
 ├─ SENSOR STATE
 ├─ LOCATION
 ├─ CONNECTIVITY
 ├─ MEDIA
 └─ TASK STATE
```

Context is selective and provenance-bearing. Agents receive only the subset required for the current task.

## 8. Security

- APK/XAPK/BAPK inputs are untrusted.
- Static inspection is isolated from execution.
- No credential extraction, license bypass or authentication bypass is part of the design.
- No hidden endpoint discovery is required.
- Mobile permissions are capability-scoped.
- Location, microphone, camera and contacts/calendar data require explicit policy authorization.
- Secrets are never exposed to untrusted model output.
- Network egress is policy-controlled.
- High-impact actions require explicit approval or a pre-authorized policy.
- Readback is mandatory for consequential actions.

## 9. UX principles

The NeXus luxury design system is inherited as a product contract:

- obsidian base;
- restrained platinum/rhodium borders;
- gold/copper semantic accents;
- inline SVG icons;
- Polish-first labels;
- quiet status indicators;
- no fake success states;
- responsive mobile layouts;
- reduced-motion support;
- accessible touch targets and semantic labels.

The exact visual tokens remain owned by the NeXus design-system contract rather than duplicated in every feature module.

## 10. Verification program

1. APK/XAPK/BAPK container classification tests.
2. Manifest/resource/DEX/native-library inventory tests.
3. Hash/signature evidence recording.
4. Permission and component risk classification.
5. Split-graph reconstruction: base/locale/ABI/density/device configuration.
6. Device screen observation replay.
7. UI-tree versus screenshot consistency tests.
8. Touch/gesture readback tests.
9. App launch/readback tests.
10. Camera/microphone authorization tests.
11. Location-context freshness tests.
12. P116 image import/export round-trip tests.
13. Offline/reconnect recovery tests.
14. Android-version and ABI matrix.
15. Sandboxed test-device execution for agent-generated actions.
16. Full intent → action → readback → verification replay.

## 11. Definition of Done

P117 advances beyond architecture baseline when:

- package inspection is reproducible and read-only;
- XAPK/APK split graphs are reconstructed deterministically;
- Android capability contracts are typed and authorization-aware;
- device observations carry provenance/freshness;
- consequential actions have authoritative readback;
- P100 and P116 integrations pass end-to-end tests;
- camera/audio/location handling passes privacy/security tests;
- sandboxed agent-generated actions cannot escape their capability policy;
- failures and partial actions are recoverable and auditable.

## Evidence classification

- NeXus source requirements: **SOURCE-DERIVED**;
- uploaded `manifest.json`: **OBSERVED / DIRECTLY PARSED SOURCE**;
- uploaded split APK filenames and sizes: **OBSERVED**;
- uploaded binary internals beyond the manifest: **NOT OBSERVED in this iteration**;
- TomTom bundle/feature facts: **EXTERNAL-VERIFIED CONTEXT**;
- Retouch feature patterns: **EXTERNAL-VERIFIED CONTEXT**;
- P117 architecture: **SYNTHESIS / IMPLEMENTATION TARGET**.

## Dependencies

P40, P57, P61, P72, P97, P100, P114, P116.
