# Knowledge Base — OmniMAS Local Android Runtime

## Intake

Date: 2026-09-11
Source: uploaded Android project files for `OmniMAS-Local-Android`.

## Evidence

The supplied project README defines a local multi-agent Android runtime with the decomposition `Planner → Grounding → Executor → Supervisor`, optional local Ollama at `127.0.0.1:11434`, AccessibilityService, NotificationListenerService and task-local Memory. ADB/Termux is explicitly limited to debugging. fileciteturn78file0L3-L14

The source also explicitly rejects undocumented Samsung intents, fake ADB Burst Mode, private system-setting manipulation and API keys embedded in the app. fileciteturn78file0L16-L18

The Android manifest directly evidences an exported launcher activity plus non-exported AccessibilityService and NotificationListenerService protected by their respective Android binding permissions. fileciteturn78file1L8-L35

The accessibility configuration requests retrieval of window content and gesture execution and listens to window/view state events. fileciteturn78file2L1-L8

The build configuration identifies Android Gradle Plugin 8.13.0, Kotlin Android 2.2.21, compile/target SDK 36, min SDK 28, namespace/application ID `pl.omnimas.local`, Jetpack Compose Material 3, coroutines, OkHttp and JSON dependencies. fileciteturn79file0L10-L16 fileciteturn79file1L27-L30 fileciteturn79file2L41-L67

## Reusable architecture

```text
USER INTENT
   ↓
PLANNER / LOCAL LLM
   ↓
GROUNDER
   ↓
SEMANTIC UI STATE
   ↓
EXECUTOR
   ↓
ACCESSIBILITY ACTION
   ↓
AUTHORITATIVE READBACK
   ↓
SUPERVISOR
   ├─ VERIFY
   └─ REPLAN
        ↓
     TASK MEMORY
```

## Key synthesis

This material converts P117's abstract Android capability plane into a concrete local-runtime reference profile. The four-stage decomposition should be reusable as a bounded execution strategy:

- Planner = intent decomposition;
- Grounding = current-state interpretation;
- Executor = scoped actuation;
- Supervisor = postcondition verification and recovery.

The pattern is compatible with the repository's `OBSERVE → PLAN → AUTHORIZE → ACT → READBACK → VERIFY` doctrine.

## Security implications

Accessibility and notification access must be modeled as separate privileged capabilities. Notification text is sensitive context. Model-generated plans remain untrusted proposals. A gesture or click event cannot be promoted to success without readback. Local inference reduces dependency on external providers but does not itself constitute a security boundary.

## Relationship graph

`P100 → capability intent`

`P117 → Android authorization/package/verification boundary`

`P119 → local Planner/Grounding/Executor/Supervisor runtime`

`P116 → photographic workflows when media tasks are involved`

`P118 → StoryWorld workflows when narrative/multimedia tasks are involved`

## Explicit unknowns

The uploaded intake does not include the Kotlin implementation files such as the actual `Planner`, `Grounding`, `Executor`, `Supervisor`, `LocalLlmClient` or service implementation bodies. Therefore their exact algorithms, UI-tree serialization, prompt format, Ollama request schema, persistence mechanism and error handling remain unverified.

The supplied theme is currently Material Light/white chrome and is treated as implementation evidence, not as the final NeXus visual contract. fileciteturn78file3L1-L6
