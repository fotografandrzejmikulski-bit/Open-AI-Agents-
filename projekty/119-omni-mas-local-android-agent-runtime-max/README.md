# Project 119 — OmniMAS Local Android Agent Runtime MAX

## Status
SOURCE INGESTED → ARCHITECTURE BASELINE → KOTLIN IMPLEMENTATION EVIDENCE → COMPLETE GITHUB RELEASE-AUDIT INTEGRATION — 2026-09-11

## Mission
Build a local-first Android multi-agent runtime in which a Planner, Grounding layer, Executor and Supervisor cooperate over device UI state, with local LLM inference and explicit verification.

## Source implementation witness
The supplied README describes the runtime as `Planner → Grounding → Executor → Supervisor`, with optional local Ollama at `127.0.0.1:11434`. ADB/Termux is explicitly outside the production core and may be used only for debugging.

Declared modules are AccessibilityService for UI perception/action, NotificationListenerService for authorized local notifications, Planner, Grounding, Executor, Supervisor and task-local Memory.

The source explicitly rejects undocumented Samsung intents, a fictitious ADB Burst Mode, private system-setting manipulation and embedding API keys in the application.

## Android platform evidence

The supplied manifest defines `MainActivity`, an exported launcher activity, a non-exported `OmniAccessibilityService` protected by `BIND_ACCESSIBILITY_SERVICE`, and a non-exported `OmniNotificationListener` protected by `BIND_NOTIFICATION_LISTENER_SERVICE`.

The accessibility configuration requests window-content retrieval and gesture execution, and observes window-state/content changes plus view-click/focus events.

The Android project is named `OmniMAS-Local-Android`, uses an `:app` module, Android Gradle Plugin 8.13.0 and Kotlin Android plugin 2.2.21. The app module declares namespace/application ID `pl.omnimas.local`, compile/target SDK 36 and min SDK 28. Dependencies include AndroidX Core/Activity/Lifecycle, Jetpack Compose Material 3, coroutines, OkHttp 5.1.0 and JSON processing.

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
AUTHORITATIVE READBACK
    ↓
SUPERVISOR
    ├── VERIFY
    └── REPLAN
         ↓
      TASK MEMORY
```

## 1. Planner

Planner converts an operator task into bounded executable intent. Local Ollama is the source-described LLM path. Networked providers are not implied by this artifact.

The supplied Kotlin implementation confirms that planning and per-step action decisions are implemented in `LocalLlmClient`. The planner constrains missions to bounded Android steps and explicitly disallows financial operations, data deletion, password handling and irreversible communications without separate confirmation. The decision contract returns only bounded action types: `CLICK`, `TYPE`, `SCROLL`, `BACK`, `HOME`, `DONE`.

## 2. Grounding

Grounding converts the current Android accessibility/UI observation into a semantic representation suitable for planning. Raw UI events remain observations; they are not authoritative proof of final application state.

The supplied `GroundingAgent` recursively captures visible UI nodes with bounds, text/description, role/class name, resource ID, clickability, editability and enabled state. Node coordinates are derived from accessibility bounds.

## 3. Executor

Executor owns bounded UI actions such as clicks, text entry, gestures and navigation. Accessibility gesture capability is directly evidenced by the service configuration.

The supplied `ExecutionAgent` confirms bounded execution through `ACTION_CLICK`, `ACTION_SET_TEXT`, global BACK/HOME actions and gesture-based scrolling. `DONE` terminates the current mission path.

## 4. Supervisor

The current implementation does not contain a standalone `Supervisor` class. Supervision is presently embodied by the mission loop in `OmniAccessibilityService`: it captures fresh UI state, asks the local decision model for an action, executes it, stores successful actions, waits for state change and checks the declared `expectedNow` postcondition before proceeding or replanning.

This is therefore **supervision-by-orchestration**, not yet a separately testable Supervisor module. The architecture retains the Supervisor boundary as a target component.

## 5. Notification boundary

Notification access is an independent capability and must remain disabled unless explicitly authorized. The manifest declares a dedicated notification-listener service rather than exposing it as an ordinary exported component.

The supplied `OmniNotificationListener` extracts notification title/text and stores up to 100 notification items in an in-memory synchronized deque. This confirms a concrete local notification context path, but also creates a privacy requirement: notification projection to the LLM must be selective, redacted and task-scoped.

## 6. Local-first LLM boundary

The source specifies Ollama as a local endpoint and notes that localhost access from a separate Android process may require runtime-specific adaptation.

The supplied Kotlin client confirms the endpoint `http://127.0.0.1:11434` and a default local model `deepseek-r1:1.5b`. The client uses Ollama `/api/generate` for planning and action decisions. No API secret belongs in the Android client.

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
SUPERVISION / READBACK
          ↓
P117 ARTIFACT LEDGER
```

The local runtime is therefore an execution substrate, not a second global orchestration authority.

## 9. GitHub / DevSecOps integration learned from the complete supplied corpus audit

The GitHub reference corpus strengthens P119's **engineering and release boundary**, not its Android privilege model.

Required lifecycle:

```text
ANDROID SOURCE
   ↓
REPRODUCIBLE BUILD ENVIRONMENT
   ↓
TEST / LINT / SECURITY ANALYSIS
   ↓
CODEQL / SAST WHERE SUPPORTED
   ↓
DEPENDENCY / SUPPLY-CHAIN CHECK
   ↓
APK/AAB ARTIFACT
   ↓
DIGEST + ATTESTATION / PROVENANCE
   ↓
DEPLOYMENT / DEVICE TEST
   ↓
AUTHORITATIVE RUNTIME READBACK
```

GitHub Codespaces/dev containers are treated as reproducible development-environment patterns, not as a production execution dependency.

CodeQL is relevant to the Kotlin/Android source because GitHub supports Java/Kotlin analysis. CodeQL represents code as a queryable database and can produce SARIF results for code-scanning workflows. This becomes a future P119 CI security gate, not evidence that CodeQL has already run on this repository.

The npm corpus adds dependency audit, provenance, trusted publishing and credential-scope concepts to the release boundary, but npm is not itself a runtime dependency of the Android agent.

Artifact provenance/digest tracking becomes a release requirement for APK/AAB outputs. A successful build is not equivalent to a verified deployment.

The current GitHub ecosystem also exposes mobile CI/CD Actions through Marketplace. Such integrations must be treated as typed, permissioned capabilities with version/provenance metadata and post-deployment readback rather than trusted-by-installation.

## 10. Agentic GitHub boundary

Current GitHub organization sources expose agentic-workflow, MCP gateway, workflow-firewall, artifact-attestation and Copilot Agent SDK reference projects. P119 does not inherit their authority. If P119 is ever controlled from a GitHub-side agent, the boundary remains:

`agent intent → capability policy → mobile authorization → bounded action → device readback`.

MCP exposure or GitHub workflow availability never authorizes an Android action by itself.

## 11. UX / design-system requirements

The supplied Android theme currently uses a Material Light NoActionBar theme, sans font and white status/navigation bars.

This is accepted as source implementation evidence, but it does **not** replace the NeXus product design contract. A future P119 product shell should inherit P100's design system while preserving Android accessibility conventions.

The supplied strings identify the product as `OmniMAS Local` and describe it as a local Android UI automation agent controlled by the user.

## 12. Security doctrine

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
- Generated APK/AAB artifacts require digest/provenance records before promotion.
- CI security results are evidence inputs, not authorization by themselves.
- GitHub Marketplace, MCP and agentic workflows are capabilities, not Android authorization authorities.

## 13. Verification program

1. Accessibility-service enable/disable tests.
2. UI-tree grounding determinism tests.
3. Node identity/TOCTOU tests across changing UI snapshots.
4. Click/type/gesture action readback tests.
5. Supervisor/replan tests after failed postconditions.
6. Notification authorization and redaction tests.
7. Ollama connectivity/error/recovery tests.
8. Offline operation tests.
9. Android-version compatibility tests.
10. Foreground/background lifecycle tests.
11. Capability-policy enforcement tests.
12. Prompt-injection resistance for hostile UI text.
13. Task-memory isolation tests.
14. End-to-end `intent → plan → ground → act → readback → verify` replay.
15. CodeQL/SAST CI validation for supported Kotlin/Java paths.
16. Reproducible build and dependency-lock validation.
17. APK/AAB digest and provenance/attestation verification.
18. Deployment/device test with post-deployment readback.
19. Mobile CI/CD capability permission and version/provenance validation.
20. GitHub-agent-to-mobile authorization boundary test, if such integration is enabled.

## Definition of Done

P119 advances beyond architecture baseline when the supplied runtime builds reproducibly, local LLM connectivity is observable, accessibility actions are bounded by policy, every consequential action has authoritative readback, supervision/replanning is deterministic under test, notification data is permission-scoped, node identity remains valid across action execution, release artifacts carry verifiable digests/provenance, and P117/P100 integration passes end-to-end verification.

## Evidence classification

- supplied README/Gradle/manifest/XML: **OBSERVED / SOURCE-DERIVED**;
- supplied Kotlin implementation: **OBSERVED / DIRECT SOURCE IMPLEMENTATION EVIDENCE**;
- local Ollama and action schemas: **OBSERVED / DIRECT SOURCE IMPLEMENTATION EVIDENCE**;
- current supervision: **OBSERVED / ORCHESTRATION-LEVEL IMPLEMENTATION**, not standalone Supervisor;
- GitHub Codespaces/CodeQL/provenance/npm/Marketplace patterns: **EXTERNAL-VERIFIED CONTEXT / ENGINEERING REQUIREMENTS**;
- architecture above: **SYNTHESIS / IMPLEMENTATION TARGET**;
- CodeQL execution, reproducible release, attestations and artifact provenance in P119: **NOT YET VERIFIED**.

## Dependencies

P40, P54, P57, P59, P61, P72, P100, P114, P117.
