# Knowledge Corpus — Iteration 30 — Digital Human / Autonomous Digital Presence

## Source
User-supplied report: **Architektura Systemu Autonomicznej Obecności Cyfrowej: Techniczna i Psychologiczna Synteza „Ludzkiego Współczynnika” w Interfejsach Czasu Rzeczywistego**.

## Evidence boundary
This artifact records the supplied report as a source-derived architecture proposal. Performance numbers, named implementations and SOTA claims are **not independently verified here**. They remain source claims until reproduced against controlled benchmarks.

## 1. Core thesis
The report defines a Digital Human as a real-time multimodal interface combining visual embodiment, cognition, voice, affective perception and authorized system agency. Its central construct is the **human factor / ludzki współczynnik**: perceived human presence emerges from coordinated temporal fluency, multimodal coherence and emotional resonance rather than from visual fidelity alone.

The report argues for edge/on-device processing to reduce network-induced latency and privacy exposure, while allowing cloud services as optional adapters rather than as the sole runtime dependency.

## 2. Human-factor parameters
The report proposes three pillars:
- temporal fluency / low response latency;
- multimodal consistency between words, voice, face and body;
- emotional resonance / adaptive affective behavior.

It cites an approximately 200 ms conversational timing target and 500–700 ms as a range in which cloud voice interaction may feel noticeably turn-based. These thresholds are **source-derived hypotheses/engineering targets**, not established universal perceptual constants in this artifact.

## 3. Visual embodiment
Candidate visual representations:
- 3D Gaussian Splatting (3DGS) + WebGPU for photorealistic browser/mobile rendering;
- Unreal Engine 5 / MetaHuman for premium high-fidelity deployments;
- Unity or Godot 4/Vulkan for mobile-oriented trade-offs;
- VRM for stylized/anime assets;
- glTF/USD-family representations for richer 3D asset pipelines.

The report highlights 3DGS for organic microdetail such as hair and skin, while explicitly noting that skeletal mesh animation remains more mature for precise deformation. The architecture therefore should not treat 3DGS as a universal replacement for meshes.

The proposed asset model separates:
```text
VISUAL DEFINITION ≠ BEHAVIORAL / PERSONA DEFINITION
```
allowing a visual body and a behavioral identity to be exchanged independently.

## 4. Cognitive layer
The proposed cognitive substrate is local-first:
- mobile SLM/LLM inference;
- NPU acceleration where supported;
- quantization such as INT4;
- local/offline operation;
- local vector retrieval / RAG;
- persistent episodic memory;
- Character Card V2-compatible persona packaging.

The report names Gemma 3n, Qwen 2.5 and Llama 3.1 as examples and cites MediaTek NeuroPilot / Qualcomm QNN and mobile vector databases. These are candidate technologies, not validated stack commitments.

Important portfolio invariant:
```text
PERSONA / MEMORY / MODEL CAPABILITY ≠ AUTHORITY
```

## 5. Voice and embodiment synchronization
The report proposes:
- streaming TTS;
- instant voice cloning with explicit consent for source voices;
- emotional/prosodic speech;
- Audio2Face or comparable audio-to-face systems;
- Live2D for lightweight stylized embodiments;
- talking-head approaches for weaker devices;
- full-duplex interaction;
- VAD + AEC + interruption / barge-in handling.

The key architectural requirement is a shared temporal clock / event stream so that text, audio, facial motion, gaze and body motion do not become independently scheduled subsystems.

## 6. Affective loop
The proposed loop is:
```text
CAMERA + MICROPHONE
        ↓
VISUAL / AUDIO AFFECT FEATURES
        ↓
MULTIMODAL STATE FUSION
        ↓
CHARACTER / RESPONSE POLICY
        ↓
TEXT + PROSODY + EXPRESSION + MOTION
        ↓
AVATAR PRESENTATION
```

The report suggests facial-expression recognition and speech-emotion recognition, with valence/arousal-like representations. These outputs should be treated as uncertain sensor estimates, not objective readings of a person's internal mental state.

## 7. Agency / Agentic OS integration
The Digital Human is proposed as more than a chatbot. On Android, Accessibility and ADB can provide authorized UI interaction; vision and UI-tree perception can support task execution. The existing P105 architecture is directly relevant.

Required separation:
```text
AVATAR INTENT
   ↓
TASK / COMMAND IR
   ↓
CAPABILITY + POLICY GATE
   ↓
AUTHORIZED ACTION
   ↓
READBACK
   ↓
AUTHORITATIVE POSTCONDITION
```

Accessibility is a capability channel, not unrestricted authority.

## 8. Launcher / shell embodiment
The report proposes a custom Android launcher or desktop shell in which the avatar becomes a persistent interface surface. This is a presentation/runtime boundary, not permission to silently control the underlying operating system.

## 9. New reusable architecture pattern
The corpus exposes a reusable **Embodied Presence Runtime** composed of:
```text
PRESENCE ORCHESTRATOR
├── AVATAR / RENDERING
├── COGNITIVE ENGINE
├── MEMORY / RETRIEVAL
├── VOICE I/O
├── FACIAL / BODY ANIMATION
├── AFFECT SENSOR FUSION
├── TEMPORAL SYNCHRONIZATION
├── PERSONA / CHARACTER STATE
├── CAPABILITY / POLICY GATE
├── SYSTEM / DEVICE ADAPTERS
└── EVIDENCE / TELEMETRY / REPLAY
```

The runtime must keep authoritative device/system state separate from model-generated interpretation and presentation state.

## 10. Security, privacy and governance implications
The source advocates local processing and low latency, but an autonomous persistent avatar introduces additional attack surfaces:
- voice cloning and impersonation;
- persona hijacking / prompt injection;
- memory poisoning;
- sensor spoofing;
- unauthorized Accessibility actions;
- hidden microphone/camera activation;
- model-controlled UI actions;
- emotional-state overreach;
- synchronization desynchronization causing misleading presentation;
- privacy leakage through multimodal sensor streams.

Therefore the system should integrate P54/P72/P108-style assurance rather than treat anthropomorphic presentation as evidence of trustworthiness.

## 11. Verification targets
Required benchmark families:
- p50/p95 end-to-end voice-to-response latency;
- audio/video/text synchronization error;
- frame-time and thermal behavior on target mobile hardware;
- speech interruption recovery;
- lip-sync accuracy;
- persona consistency across sessions;
- memory retrieval precision and stale-memory rejection;
- affect-estimation calibration and uncertainty;
- accessibility action authorization and postcondition verification;
- sandbox / capability boundary tests;
- replayability of interaction traces;
- sensor dropout and disagreement tests;
- privacy/egress audits;
- resource-exhaustion and degraded-mode tests.

## 12. Portfolio correlation
Strongest affected lineages:
- **P57** — multimodal intelligence / PUI substrate;
- **P61** — OmniCore convergence and runtime substrate;
- **P81** — voice-native AI-character interaction;
- **P91** — synthetic persona and cognitive style engineering;
- **P97** — multimedia production / avatar content pipeline;
- **P100** — NeXus agentic development environment;
- **P105** — verified Android perception and actuation;
- **P72/P54/P108** — assurance, cognitive security and defensive LLM security validation.

The corpus does not merely duplicate one of these. It combines them into a distinct product/runtime boundary: **persistent embodied real-time digital presence**.

## 13. Safety exclusions
No operationalization is made of covert surveillance, unauthorized device control, impersonation, non-consensual voice cloning, or psychological manipulation. Affective inference remains probabilistic and privacy-governed.

## 14. Classification
- **SOURCE-DERIVED:** architecture components and named technologies described in the report.
- **INFERRED:** the reusable system boundary is an embodied real-time presence runtime.
- **PROPOSED:** dedicated Project 109 is justified because no existing project owns the complete integrated Digital Human runtime.
- **NOT ESTABLISHED:** the report does not independently prove that any particular stack achieves universal <200 ms latency, eliminates the uncanny valley, or produces genuine empathy/consciousness.
