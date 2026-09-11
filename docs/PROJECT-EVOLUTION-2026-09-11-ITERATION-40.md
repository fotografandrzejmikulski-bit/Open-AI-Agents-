# Project Evolution — Iteration 40 — OmniMAS Local Android

## Trigger

New Android source bundle for `OmniMAS-Local-Android`: Gradle configuration, AndroidManifest, AccessibilityService configuration, theme, strings and project README.

## Directly observed

- local multi-agent decomposition: Planner → Grounding → Executor → Supervisor;
- local Ollama endpoint pattern at `127.0.0.1:11434`;
- AccessibilityService for UI perception/action;
- NotificationListenerService for authorized notifications;
- task-local Memory;
- explicit rejection of undocumented Samsung intents, fake ADB Burst Mode, private settings manipulation and embedded API keys. fileciteturn78file0L3-L18
- non-exported privileged Android services protected by Android binding permissions. fileciteturn78file1L15-L35
- accessibility window-content retrieval and gesture execution. fileciteturn78file2L1-L8
- AGP 8.13.0, Kotlin 2.2.21, SDK 36/36/28 and Compose/OkHttp/coroutines dependencies. fileciteturn79file0L10-L16 fileciteturn79file1L27-L30 fileciteturn79file2L41-L67

## Portfolio decision

The material does **not** replace P117. It supplies a concrete implementation profile for P117's Android execution boundary and a local execution adapter for P100.

A distinct project **P119 — OmniMAS Local Android Agent Runtime MAX** is justified because the supplied material constitutes a coherent local runtime boundary with its own Planner/Grounding/Executor/Supervisor lifecycle, while remaining downstream of the broader P117 capability/security boundary.

## Existing-project upgrades

### P117

- adopt Planner/Grounding/Executor/Supervisor as a reference mobile execution profile;
- formalize AccessibilityService and NotificationListenerService as separately authorized capabilities;
- add local-LLM execution profile;
- add supervisor-driven replan/readback tests;
- distinguish semantic UI grounding from authoritative application state.

### P100

- add P119 as a local Android execution adapter;
- route OCN/model intent through P117 authorization rather than direct accessibility control;
- treat P119 task results as observations requiring verification.

### P116 / P118

No domain ownership changes. P119 provides device execution only; P116 remains photographic production and P118 remains StoryWorld/narrative continuity.

## Security doctrine

Accessibility and notification access are privileged capabilities. Model output is an untrusted proposal. Click/gesture emission is not proof of success. Consequential actions require readback and postcondition verification. No undocumented OEM control, credential extraction, private settings manipulation or authentication bypass is introduced.

## Verification state

- Android project configuration: directly observed;
- manifest/service configuration: directly observed;
- actual Kotlin runtime implementation: not included in this intake;
- build success: not independently reproduced in this iteration;
- architecture: synthesis from supplied source and repository doctrine.

## Root README

`readme_sync: PENDING`.
