# Digital Human / Personified UI / Edge Presence — Knowledge Base

## Source provenance
Derived from the supplied Digital Human / Personified UI design document. Performance values and technology readiness claims are treated as design targets/source claims unless independently verified.

## Functional decomposition
- Visual rendering and avatar representation.
- Cognitive/on-device model inference.
- Voice synthesis and streaming interaction.
- Real-time animation/lip-sync.
- Multimodal perception and optional affective signals.
- OS-level integration through governed capabilities.

## Rendering
The source evaluates 3D Gaussian Splatting + WebGPU, MetaHuman/Unreal for premium rendering, and Unity/Godot for lighter mobile targets. Asset bundles decouple visual representation from behavior/persona.

## Low-latency architecture
The source uses a local/edge-first design with SLMs, quantization and NPU acceleration. Latency should be measured end-to-end rather than assumed from model inference speed alone: microphone/VAD → inference → TTS first audio → animation → presentation.

## Persona and memory
Character definitions should be versioned artifacts containing visual profile, voice profile, behavioral style, knowledge references and permissions. Episodic memory remains retrievable evidence; it must never override policy or authorization.

## Affective computing boundary
Emotion recognition from face, voice or other signals is probabilistic and context-dependent. It may support optional presentation/accessibility adaptation, but must not independently trigger consequential actions, hidden targeting, permission changes or coercive interaction.

## OS agency
Accessibility or UI automation capabilities require explicit typed capability grants, approval policy, action logging and authoritative readback/postcondition verification. Visual perception does not imply authorization.

## Human-agency requirement
The avatar should be clearly represented as software, provide inspection/disable controls for adaptive perception, preserve opt-out and reversibility, and avoid covert dependency mechanisms.

## Cross-project links
Extends Projects 5, 18, 21, 31, 36, 40, 41, 49, 53, 57, 58 and the OmniCore convergence architecture.
