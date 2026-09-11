# Knowledge Corpus — NeXus Mobile / APK / Visual Intelligence

Date: 2026-09-11
Classification: SOURCE-DERIVED + EXTERNAL-VERIFIED CONTEXT + UNVERIFIED BINARY INTAKE

## 1. Corpus received

### Product / architecture sources
- `NeXus AI Code.md`
- `NeXus AI Code2.md`
- `NeXus AI Code3.md`
- `Architektura i Rozwój Systemu Nexus AI Code.md`
- previously ingested OMEGA-X / God-Level material

The NeXus product source specifies a Polish-first developer environment with dual-GGUF loading, OCN single-agent/swarm invocation, a 9-file agent registry, multimodal camera/desktop/microphone/STT/TTS/HID control, Tor browser capability, Unreal/Unity/Android automation, model training, MCP workspace access, image/video model slots and DGM/RSI. The implementation report additionally records a VS Code/Electron extension federation, dual-GGUF controls, MCP tooling, sensory sidecar, world panels, code evolution, trainer, telemetry and Polish/luxury theme layers. These implementation claims remain source-reported until independently reproduced.

### Android binary corpus
The uploaded binary set contains:

| Artifact | Type | Size | Intake status |
|---|---:|---:|---|
| `com.mod.aiby.inc.mod.apk.1.29.276.2991.29.276299.apk` | APK | 66,994,345 B | metadata observed; internal structure not decoded |
| `com.mod.furby.boom.v1.9.0.mod.unlimited.money1.9.0.xapk` | XAPK | 277,575,678 B | metadata observed; too large for current materialization limit |
| `com.mod.pic.retouch.remove.objects.mod.apk.1.184.431.184.43.apk` | APK | 22,618,344 B | metadata observed; internal structure not decoded |
| `com.mod.retouch.mod.apk.vip.unlocked.2.2.0.02.2.0.0.apk` | APK | 99,476,291 B | metadata observed; internal structure not decoded |
| `com.tomtom.speedcams.android.map9.41.0.bapk` | BAPK | 409,931,216 B | metadata observed; too large for current materialization limit |
| `com.touch.retouch.removeobject.photo4.24.bapk.temp` | BAPK/temp | 6,526,950 B | metadata observed; not decoded |

The Files parser reports no readable text for the binary artifacts. This means package internals, manifests, DEX inventories, native libraries and resource trees are **not claimed as directly observed** in this iteration.

## 2. APK/BAPK structural model

For ordinary Android packages, the useful static inspection layers are:

```text
container
├── AndroidManifest.xml
├── classes*.dex
├── resources.arsc
├── res/
├── assets/
├── lib/<ABI>/*.so
├── META-INF/
└── optional split/config artifacts
```

For XAPK/BAPK-style bundles, the outer container may aggregate a base APK plus ABI/DPI/language/configuration splits and, depending on format, additional payloads. The exact uploaded containers must be parsed before assigning a concrete tree.

A matching public record for the uploaded TomTom package/version identifies `com.tomtom.speedcams.android.map`, version 9.41.0, and describes a bundle consisting of a base APK plus four splits, with arm64-v8a/armeabi-v7a and 480/640 DPI variants. That public record is **external context for the package/version**, not proof that the uploaded BAPK is byte-identical to that release. citeturn4search0

## 3. Visual editing capability synthesis

The Retouch-class material is highly relevant to P116. Current public descriptions of comparable Android Retouch products show a product pattern built around:

- brush/one-tap object removal;
- people and background removal;
- watermark/text/logo cleanup;
- blemish/skin retouch;
- background replacement;
- video object/watermark removal with tracking;
- cutout/paste/clone workflows;
- AI enhancement and AI expand;
- simple mobile-first save/share flows.

These capabilities should be treated as **feature-pattern evidence**, not as a claim about the exact uploaded APK internals. citeturn3search0turn3search2turn3search5

A particularly useful product-quality constraint from TouchRetouch is preservation of quality/EXIF data and explicit acknowledgement that automatic removal quality depends on scene/background conditions. This reinforces P116's need for provenance, non-destructive editing and quality gates. citeturn3search5

## 4. Navigation / mobile-world context synthesis

The uploaded TomTom artifact is valuable to the broader mobile-agent architecture because its public version record demonstrates a mature Android bundle with navigation, live traffic, hazard/speed-camera alerts, Android Auto, Bluetooth integration, overlay mode and calendar/contact destination lookup. These are examples of a mobile application that fuses location, audio, external display and contextual data into a continuous operational UI. citeturn4search0

The relevant architectural lesson for NeXus is not to copy proprietary implementation, but to model a **mobile-world context layer**:

```text
DEVICE SENSORS
  ↓
LOCATION / TIME / CONNECTIVITY
  ↓
CONTEXT GRAPH
  ↓
AGENT OBSERVATION
  ↓
POLICY + USER AUTHORIZATION
  ↓
MOBILE ACTION
  ↓
AUTHORITATIVE READBACK
```

## 5. New architectural deductions

### A. P100 — NeXus should gain a Mobile Capability Plane

The existing P100 architecture already contains vision/audio/HID, MCP, sandboxing and multimodal control. The new corpus justifies a dedicated mobile capability plane for:

- Android device discovery;
- screen observation;
- camera/microphone observation;
- touch/gesture input;
- accessibility-tree/UI semantics where available;
- bounded app launching;
- media import/export;
- location/context signals;
- Android Auto / external-display integration as an adapter boundary;
- APK/XAPK/BAPK static inspection as a separate analysis capability.

No mobile capability is implicitly authorized merely because an agent can technically invoke it.

### B. P116 — upgrade from Photo Agent to Mobile Visual Production Runtime

P116 should absorb the strongest mobile retouch interaction patterns while preserving its stricter photographic contracts:

```text
SELECT / CAPTURE
      ↓
AUTO SUBJECT + OBJECT DETECTION
      ↓
BRUSH / SMART MASK / TRACKING
      ↓
IDENTITY + STRUCTURE LOCK
      ↓
NON-DESTRUCTIVE EDIT GRAPH
      ↓
GENERATE / FILL / ENHANCE / REMOVE
      ↓
QUALITY + PROVENANCE GATE
      ↓
EXPORT / SHARE / VERSION
```

The important upgrade is not simply more tools. It is a reversible edit graph, operation provenance, mask lineage, EXIF preservation policy, confidence/uncertainty display and deterministic before/after comparison.

### C. New project candidate — P117

The combined corpus creates a distinct project boundary: **NeXus Mobile Multimodal Agent Runtime MAX**. P100 owns the general developer control plane; P116 owns photographic production; P117 owns the Android/mobile execution substrate and its static-app inspection, device perception, context fusion and safe actuation contracts.

## 6. Security and evidence doctrine

- Uploaded APK/XAPK/BAPK files are untrusted binary inputs.
- No binary was executed.
- No credentials, license bypasses or authentication mechanisms are to be extracted.
- Filenames containing `mod`, `unlimited`, `vip unlocked` or similar are treated as untrusted naming metadata, not proof of package capabilities.
- Reverse-engineering of proprietary apps is not an architectural requirement; public documentation is used only for feature-pattern comparison.
- Static package inspection must remain read-only and sandboxed.
- Mobile actions follow `OBSERVE → PLAN → AUTHORIZE → ACT → READBACK → VERIFY`.

## 7. Evidence matrix

| Claim | Classification |
|---|---|
| NeXus dual-GGUF / OCN / multimodal product requirements | SOURCE-DERIVED |
| NeXus 13-extension implementation report | SOURCE-REPORTED, not independently reproduced here |
| Uploaded binary filenames and sizes | OBSERVED |
| Uploaded binary internal manifest/DEX/native structure | NOT OBSERVED in this iteration |
| TomTom 9.41.0 bundle architecture/features | EXTERNAL-VERIFIED CONTEXT |
| Retouch feature patterns | EXTERNAL-VERIFIED CONTEXT |
| New P117 architecture | SYNTHESIS / IMPLEMENTATION TARGET |

## 8. Reusable knowledge added

1. Mobile agent control needs a first-class capability plane, not an extension of generic desktop HID.
2. Visual editing should be represented as a versioned operation graph rather than a sequence of opaque destructive actions.
3. Mobile multimodal systems benefit from a context graph combining sensor, location, connectivity, application and user-intent state.
4. APK bundle format, split architecture and static metadata should be modeled explicitly for future app-inspection workflows.
5. UI state remains a projection; mobile action success requires authoritative readback.
