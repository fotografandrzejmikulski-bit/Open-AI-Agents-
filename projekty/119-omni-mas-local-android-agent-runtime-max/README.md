# Project 119 — OmniMAS Local Android Agent Runtime MAX

## Status
SOURCE INGESTED → ARCHITECTURE BASELINE — 2026-09-11

## Mission
Build a local-first Android multi-agent runtime in which a Planner, Grounding layer, Executor and Supervisor cooperate over device UI state, with local LLM inference and explicit verification.

## Source implementation witness
The supplied README describes the runtime as `Planner → Grounding → Executor → Supervisor`, with optional local Ollama at `127.0.0.1:11434`. ADB/Termux is explicitly outside the production core and may be used only for debugging. fileciteturn78file0L3-L5

Declared modules are AccessibilityService for UI perception/action, NotificationListenerService for authorized local notifications, Planner, Grounding, Executor, Supervisor and task-local Memory. fileciteturn78file0L7-L14

The source explicitly rejects undocumented Samsung intents, a fictitious ADB Burst Mode, private system-setting manipulation and embedding API keys in the application. fileciteturn78file0L16-L18

## Android platform evidence

The supplied manifest defines `MainActivity`, an exported launcher activity, a non-exported `OmniAccessibilityService` protected by `BIND_ACCESSIBILITY_SERVICE`, and a non-exported `OmniNotificationListener` protected by `BIND_NOTIFICATION_LISTENER_SERVICE`. fileciteturn78file1L8-L35

The accessibility configuration requests window-content retrieval and gesture execution, and observes window-state/content changes plus view-click/focus events. fileciteturn78file2L1-L8

The Android project is named `OmniMAS-Local-Android`, uses an `:app` module, Android Gradle Plugin 8.13.0 and Kotlin Android plugin 2.2.21. The app module declares namespace/application ID `pl.omnimas.local`, compile/target SDK 36 and min SDK 28. Dependencies include AndroidX Core/Activity/Lifecycle, Jetpack Compose Material 3, coroutines, OkHttp 5.1.0 and JSON processing. fileciteturn79file0L10-L16 fileciteturn79file1L27-L30 fileciteturn79file2L41-L67

## Canonical architecture

```text
USER INTENT
    ↓
PLANNER / LOCAL LLM
    ↓
GROUNDER
    ↓
STRUCTURED UI STATE
    ↓
EXECUTOR
    ↓
ACCESSIBILITY ACTION
    ↓
READBACK
    ↓
SUPERVISOR
    ├── VERIFY
    └── REPLAN
         ↓
      TASK MEMORY
```

## 1. Planner

Planner converts an operator task into bounded executable intent. Local Ollama is the source-described LLM path. Networked providers are not implied by this artifact.

## 2. Grounding

Grounding converts the current Android accessibility/UI observation into a semantic representation suitable for planning. Raw UI events remain observations; they are not authoritative proof of final application state.

## 3. Executor

Executor owns bounded UI actions such as clicks, text entry, gestures and navigation. Accessibility gesture capability is directly evidenced by the service configuration. fileciteturn78file2L3-L6

## 4. Supervisor

Supervisor verifies postconditions and triggers re-planning when the observed state does not satisfy the intended outcome. This maps directly onto the repository doctrine:

`OBSERVE → PLAN → AUTHORIZE → ACT → READBACK → VERIFY`.

## 5. Notification boundary

Notification access is an independent capability and must remain disabled unless explicitly authorized. The manifest declares a dedicated notification-listener service rather than exposing it as an ordinary exported component. fileciteturn78file1L27-L35

## 6. Local-first LLM boundary

The source specifies Ollama as a local endpoint and notes that localhost access from a separate Android process may require runtime-specific adaptation. fileciteturn78file0L25-L30

The architecture therefore treats the LLM provider as an adapter:

```text
LOCAL TASK
   ↓
LLM ADAPTER
   ├── Ollama / local
   └── future explicitly authorized provider
   ↓
PLAN
```

No API secret belongs in the Android client.

## 7. Relationship to P117

P119 is an implementation-level local Android agent runtime that materially strengthens P117.

- **P117** remains the ecosystem-level Android/mobile capability boundary, package intelligence and verification substrate.
- **P119** supplies a concrete local multi-agent execution pattern for Android UI automation.
- P117 should absorb P119's Planner/Grounding/Executor/Supervisor decomposition as a reference runtime profile.

P119 must not bypass P117's authorization, provenance, readback or sandbox rules.

## 8. Relationship to P100

P100 can treat P119 as a local mobile execution adapter:

```text
P100 OCN / MODEL INTENT
          ↓
P117 CAPABILITY BROKER
          ↓
P119 LOCAL ANDROID RUNTIME
          ↓
PLANNER → GROUNDING → EXECUTOR
          ↓
SUPERVISOR / READBACK
          ↓
P117 ARTIFACT LEDGER
```

The local runtime is therefore an execution substrate, not a second global orchestration authority.

## 9. UX / design-system requirements

The supplied Android theme currently uses a Material Light NoActionBar theme, sans font and white status/navigation bars. fileciteturn78file3L1-L6

This is accepted as source implementation evidence, but it does **not** replace the NeXus product design contract. A future P119 product shell should inherit P100's design system while preserving Android accessibility conventions.

The supplied strings identify the product as `OmniMAS Local` and describe it as a local Android UI automation agent controlled by the user. fileciteturn78file4L1-L4

## 10. Security doctrine

- Accessibility and notification access are privileged capabilities and require explicit user authorization.
- Model output is an untrusted plan, not authorization.
- UI event emission is not success evidence.
- Every consequential action requires readback and postcondition verification.
- Local LLM inference is preferred where privacy/cost require it.
- No undocumented OEM intents or private settings manipulation.
- No credential extraction, authentication bypass or hidden endpoint discovery.
- API credentials remain outside the APK.
- Notification content is sensitive context and must be selectively projected to the planner.
- Task memory is scoped to the current task unless an explicit persistent-memory policy exists.

## 11. Verification program

1. Accessibility-service enable/disable tests.
2. UI-tree grounding determinism tests.
3. Click/type/gesture action readback tests.
4. Supervisor replan tests after failed postconditions.
5. Notification authorization and redaction tests.
6. Ollama connectivity/error/recovery tests.
7. Offline operation tests.
8. Android-version compatibility tests.
9. Foreground/background lifecycle tests.
10. Capability-policy enforcement tests.
11. Prompt-injection resistance for hostile UI text.
12. Task-memory isolation tests.
13. End-to-end `intent → plan → ground → act → readback → verify` replay.

## Definition of Done

P119 advances beyond architecture baseline when the supplied runtime builds reproducibly, local LLM connectivity is observable, accessibility actions are bounded by policy, every consequential action has authoritative readback, supervisor replanning is deterministic under test, notification data is permission-scoped, and P117/P100 integration passes end-to-end verification.

## Evidence classification

- supplied README: **OBSERVED / SOURCE-DERIVED**;
- Gradle configuration: **OBSERVED / SOURCE-DERIVED**;
- Android manifest/accessibility XML: **OBSERVED / SOURCE-DERIVED**;
- theme/strings: **OBSERVED / SOURCE-DERIVED**;
- missing Kotlin implementation files: **NOT OBSERVED in this intake**;
- architecture above: **SYNTHESIS / IMPLEMENTATION TARGET**.

## Dependencies

P40, P54, P57, P59, P61, P72, P100, P114, P117.
