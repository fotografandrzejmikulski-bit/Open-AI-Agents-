# Project 109 — OmniDigital Human Autonomous Presence Runtime MAX

## Status
PROPOSED → ARCHITECTURE BASELINE

## Mission
Build a real-time embodied digital-presence runtime in which a selectable virtual character combines multimodal perception, local/edge cognition, persistent persona and memory, streaming voice, synchronized facial/body animation, affect-aware response, and authorized device/system agency.

The objective is not to simulate consciousness or claim that the avatar is human. The objective is to engineer and measure the **perceived human factor** of a responsive digital presence while preserving explicit boundaries between presentation, inference, authority and evidence.

## Why this is a new project
Existing portfolio lineages already own major components:
- P57 — multimodal intelligence / PUI;
- P61 — OmniCore convergence/runtime substrate;
- P81 — voice-native AI-character interaction;
- P91 — synthetic persona/cognitive style engineering;
- P97 — multimedia production;
- P100 — NeXus agentic development environment;
- P105 — verified Android GUI perception and actuation;
- P54/P72/P108 — cognitive security, assurance and defensive LLM validation.

None owns the integrated runtime whose primary product boundary is **persistent embodied real-time presence**: the coordinated avatar, cognition, memory, voice, affect, temporal synchronization and authorized agency stack.

## Canonical architecture

```text
                         DIGITAL PRESENCE RUNTIME
                                  │
                 ┌────────────────┴────────────────┐
                 │ PRESENCE ORCHESTRATOR           │
                 └────────────────┬────────────────┘
                                  │
       ┌──────────────┬───────────┼───────────┬──────────────┐
       ↓              ↓           ↓           ↓              ↓
   VISUAL         COGNITIVE     VOICE      AFFECT        PERSONA /
   EMBODIMENT     ENGINE        I/O        FUSION        MEMORY
       │              │           │           │              │
   3DGS/mesh/     local SLM/   ASR/TTS     camera +      Character
   VRM/engine     LLM/NPU      streaming   microphone    state + RAG
       └──────────────┴───────────┬───────────┴──────────────┘
                                  ↓
                        TEMPORAL EVENT FABRIC
                                  ↓
                    TEXT + AUDIO + FACE + BODY + GAZE
                                  ↓
                         REAL-TIME PRESENTATION
                                  ↓
                  OPTIONAL AUTHORIZED SYSTEM AGENCY
                                  ↓
                    POLICY / CAPABILITY GATE
                                  ↓
                         ACTION + READBACK
                                  ↓
                     AUTHORITATIVE POSTCONDITION
                                  ↓
                    EVIDENCE / TELEMETRY / REPLAY
```

## 1. Presence state model

The runtime maintains distinct state planes:

```text
PRESENTATION STATE
      ≠
PERSONA / COGNITIVE STATE
      ≠
SENSOR / INFERENCE STATE
      ≠
AUTHORIZED CAPABILITY STATE
      ≠
AUTHORITATIVE DEVICE / SYSTEM STATE
```

No model-generated statement can substitute for authoritative state or evidence.

## 2. Human-factor measurement

The project turns the source report's qualitative "human factor" into measurable engineering dimensions:

| Dimension | Example measurements |
|---|---|
| temporal fluency | p50/p95 voice-to-first-response latency |
| conversational continuity | interruption recovery, turn overlap handling |
| multimodal coherence | text/audio/facial-motion timing error |
| embodiment quality | lip-sync, gaze and gesture alignment |
| persona consistency | cross-session behavioral/style agreement |
| memory continuity | retrieval precision, stale-memory rejection |
| affect adaptation | calibrated response under uncertain affect signals |
| agency reliability | task success + verified postcondition rate |
| privacy | sensor retention and egress surface |
| resource efficiency | FPS, thermal load, memory and battery |

The report's approximately 200 ms conversational target is retained as a **benchmark hypothesis**, not a universal perceptual law.

## 3. Visual embodiment fabric

Support multiple visual classes behind a common avatar contract:
- stylized 2D/2.5D;
- VRM-based 3D characters;
- skeletal mesh avatars;
- 3D Gaussian Splatting representations;
- high-fidelity MetaHuman/UE5-class avatars;
- talking-head/video embodiments where appropriate.

The avatar contract separates visual assets from behavior:

```yaml
AvatarDefinition:
  visual_asset:
  renderer:
  rig_type:
  animation_contract:
  persona_ref:
  voice_ref:
  provenance:
  version:
```

3DGS is a candidate renderer, not a mandatory representation. Precise dynamic deformation may require meshes or hybrid pipelines.

## 4. Cognitive engine

The cognitive layer may run locally, remotely or in a hybrid mode, selected by the runtime router according to latency, device resources, privacy and consequence.

Preferred edge path:
```text
USER SPEECH
 ↓
LOCAL ASR / INTENT
 ↓
LOCAL MEMORY RETRIEVAL
 ↓
LOCAL SLM/LLM
 ↓
RESPONSE PLAN
```

Cloud escalation is an adapter, not an authority bypass.

Candidate model/runtime families named by the source include mobile SLMs, NPU execution, quantization and local vector retrieval. Exact model selection is benchmark-driven.

## 5. Persona and character state

Character Cards V2-style structures can be used as an interchange layer, but the runtime owns a stricter canonical schema:

```yaml
PersonaState:
  persona_id:
  version:
  identity_label:
  behavioral_traits: []
  dialogue_style:
  boundaries: []
  relationship_state:
  memory_refs: []
  allowed_capabilities: []
  provenance:
```

Persona is a controllable behavioral configuration. It is not evidence of consciousness, legal identity or authority.

P91 remains the research laboratory for persistent cognitive style; P109 owns its embodied real-time deployment boundary.

## 6. Memory / relationship continuity

Local episodic memory is partitioned into:
- interaction events;
- user-approved memories;
- character state;
- semantic retrieval index;
- provenance and confidence;
- expiration / invalidation metadata.

Memory poisoning, stale retrieval and unauthorized persistence are first-class test cases.

## 7. Voice fabric

The voice subsystem supports:
- streaming ASR/TTS;
- partial transcript events;
- low-latency first audio;
- prosody and speaking-rate controls;
- consent-governed voice cloning;
- barge-in;
- VAD;
- AEC;
- interruption cancellation.

The core event contract is:

```text
AUDIO_IN → PARTIAL_ASR → INTENT → RESPONSE_PLAN
       → TTS_PARTIAL → AUDIO_OUT
       → INTERRUPT / CONTINUE
```

Raw audio retention is not required for ordinary operation and must be explicit when enabled.

## 8. Embodiment synchronization

A shared temporal event fabric coordinates:

```text
WORDS
  ↕
PHONEMES / PROSODY
  ↕
LIP / FACE
  ↕
GAZE
  ↕
GESTURE / BODY
  ↕
RENDER FRAME
```

No subsystem should independently invent timestamps for the same conversational turn.

Degraded modes must preserve coherence: if high-fidelity facial animation cannot keep up, the runtime falls back to a simpler validated animation mode instead of producing visibly contradictory signals.

## 9. Affective perception

Inputs may include facial-expression features, speech prosody and interaction context. The system creates an uncertain affect state rather than a claim about the user's true internal emotion:

```yaml
AffectEstimate:
  valence:
  arousal:
  confidence:
  modality_support: []
  timestamp:
  uncertainty:
```

Fusion rules must tolerate disagreement and sensor dropout. Affective estimates cannot independently authorize consequential actions.

## 10. Agentic device integration

P105 supplies the Android execution boundary:

```text
NATURAL-LANGUAGE REQUEST
        ↓
TASK / COMMAND IR
        ↓
CAPABILITY POLICY
        ↓
AUTHORIZED ACCESSIBILITY / ADB
        ↓
ACTION
        ↓
READBACK
        ↓
POSTCONDITION VERIFICATION
```

The avatar can appear to "do" something, but the authoritative proof comes from the device/system readback, not from generated dialogue.

## 11. Launcher / shell mode

Optional deployment modes:
- ordinary application;
- persistent overlay where platform policy permits;
- Android launcher;
- desktop shell/interface.

A presentation mode never implicitly expands capability scope.

## 12. Security architecture

Threat model includes:
- prompt/persona injection;
- memory poisoning;
- voice impersonation;
- non-consensual voice cloning;
- synthetic facial identity abuse;
- camera/microphone privacy violations;
- sensor spoofing;
- unauthorized Accessibility actions;
- malicious tool outputs;
- temporal desynchronization;
- model hallucinated device state;
- capability escalation.

Security integration:
```text
P54 COGNITIVE SECURITY
        ↓
P72 RUNTIME ASSURANCE
        ↓
P108 LLM SECURITY VALIDATION
        ↓
P109 PRESENCE RUNTIME
        ↓
P105 AUTHORIZED DEVICE CONTROL
```

## 13. Privacy architecture

Default:
- on-device perception where feasible;
- minimized telemetry;
- explicit camera/microphone indicators;
- explicit recording state;
- user-controlled memory persistence;
- configurable retention;
- no hidden continuous monitoring;
- auditable external-service egress.

## 14. Verification

### Latency
Measure p50/p95 from end-of-user-speech detection to first avatar response audio and visible response.

### Synchronization
Measure timestamp error among transcript, phoneme/prosody, audio, facial motion and render frame.

### Persona
Run blinded repeated-session consistency tests against a fixed persona version.

### Memory
Test retrieval precision, contradiction handling, deletion/invalidation and poisoning resistance.

### Affect
Evaluate calibration, false confidence and modality disagreement. Do not score an inferred emotion as ground truth merely because the model reports it.

### Agency
Use P105-style postcondition verification and stale-state rejection.

### Security
Run P108-style injection, replay, resource exhaustion, tool-boundary and credential-leak tests.

### Device
Benchmark FPS, thermals, RAM, battery and degraded-mode behavior on target Android hardware.

## 15. MVP

1. Android client.
2. One stylized 3D avatar plus one lightweight fallback embodiment.
3. Local/edge ASR and TTS.
4. One local SLM/LLM profile.
5. Persistent persona state.
6. Local episodic memory.
7. Full-duplex barge-in.
8. Shared temporal event fabric.
9. Basic facial/lip synchronization.
10. One affect-estimation modality plus uncertainty.
11. Five authorized Android actions through P105 boundary.
12. Authoritative readback and audit trace.
13. P108 security regression suite.
14. Latency/thermal benchmark harness.

## 16. Definition of done — architecture milestone

- Avatar can be selected independently of persona.
- Persona can be versioned independently of visual assets.
- Conversation continues across a restored session through validated memory.
- First audio and first visible response are benchmarked.
- Barge-in cancels active speech/animation without state corruption.
- Face/body/audio remain temporally coherent within a measured tolerance.
- Affect estimates carry confidence and uncertainty.
- Device actions require explicit capability authorization.
- Device actions are verified through authoritative readback.
- No model self-report is accepted as proof of external state.
- Sensor and memory privacy boundaries are testable.
- Security regression tests cover injection, poisoning and capability escalation.
- Offline/degraded operation fails predictably.

## 17. Project boundaries

**P81:** voice-native AI-character game runtime; P109 is a general digital-presence runtime and does not inherit game-economy authority.

**P91:** persona/cognitive-style research; P109 operationalizes persona in an embodied runtime.

**P105:** Android GUI perception/actuation; P109 consumes it through an authorization boundary.

**P57/P61:** multimodal/PUI and convergence substrate; P109 is the embodied product/runtime layer.

**P97:** multimedia generation/production factory; P109 is the live interactive runtime, not merely content production.

**P100:** agentic development environment; P109 is the deployed digital-presence experience.

## Evidence classification

**SOURCE-DERIVED:** The supplied report proposes 3DGS/WebGPU, mobile SLM/NPU execution, local RAG, Character Cards V2, streaming TTS, voice cloning, Audio2Face/Live2D, full-duplex interaction, affective sensing and Android Accessibility integration.

**INFERRED:** The combination forms a distinct embodied real-time presence runtime boundary.

**PROPOSED:** Project 109 is justified as a new lineage because existing projects own the components but not their complete persistent Digital Human runtime integration.

**NOT ESTABLISHED:** The supplied report does not independently establish universal <200 ms latency, guaranteed 60 FPS mobile 3DGS, elimination of the uncanny valley, genuine empathy, consciousness or human equivalence.
