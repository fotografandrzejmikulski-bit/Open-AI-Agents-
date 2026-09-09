# 05 — APEIRON NEUROADAPTIVE INTERFACE — SAFE EDITION

## Status
**Engineering Specification Baseline — Safety-Critical UX Research Track**

## Mission
Build a user-controlled perceptual interaction system in which visual adaptation and multimodal interaction can respond to explicit user input without covert persuasion, hidden behavioral commands or manipulative engagement optimization.

## Safety invariant
**Perceptual adaptation may change presentation, never user autonomy.**

No hidden layer may contain an undisclosed imperative intended to modify behavior. No adaptive controller may optimize for compulsive usage, emotional dependency or inferred psychological vulnerability.

## Product architecture

```text
Presentation
  ├─ Visual Renderer
  ├─ Motion/Intensity Controller
  ├─ Accessibility Adapter
  └─ Input Adapter
          │
Interaction Domain
  ├─ Card Engine
  ├─ Session State
  ├─ User Preferences
  └─ Consent State
          │
Application Services
  ├─ Interpretation
  ├─ Export
  ├─ Journal
  └─ Optional Agent Adapter
          │
Privacy / Security Boundary
          │
Telemetry + Storage (minimal)
```

## Canonical card model

```ts
type CardId = string;

type PerceptualIntensity = 0 | 1 | 2 | 3 | 4;

type Card = {
  id: CardId;
  version: string;
  title: string;
  archetype: string;
  visualLayers: VisualLayer[];
  interactionProfile: InteractionProfile;
  accessibilityText: string;
  provenance: Provenance;
};
```

Each visual/interactive layer has an explicit purpose and content classification: `artistic`, `informational`, `interactive` or `accessibility`.

## Perceptual controller

The controller may adapt presentation using explicit signals such as user-selected mode, device capability and accessibility preference.

```ts
type PresentationPolicy = {
  motion: 'full' | 'reduced' | 'off';
  intensity: PerceptualIntensity;
  contrast: 'standard' | 'high';
  animationBudgetMs: number;
  allowFlashingEffects: boolean;
};
```

Implicit psychological inference is prohibited as a control signal.

## Modes

### Visible
Baseline composition.

### Heat / touch simulation
A digital visual metaphor of thermochromic change. The UI must label simulation clearly; it must not imply that the device measures physical temperature unless it actually does.

### UV
Explicitly activated hidden artwork or metadata. Hidden content remains semantically informational or artistic.

### Accessibility
Reduced motion, intensity and contrast fluctuation with equivalent functional access to content.

## Input and consent model

Explicitly record only product-relevant consent states:

```ts
type ConsentState = {
  visualEffects: boolean;
  personalizedInterpretation: boolean;
  journalPersistence: boolean;
  analytics: boolean;
};
```

No consent is inferred from continued presence in the application.

## Neuroadaptive boundary

The term *neuroadaptive* applies only to measurable or explicitly selected presentation inputs. This project does not claim to infer mental states from ordinary browsing behavior.

Any future physiological-signal integration must introduce a separate device/data contract, explicit consent, local processing preference and a substantially stricter security/privacy assessment.

## Agent boundary

The optional agent is advisory:

Allowed:
- explain visual composition;
- generate reflective text from user-provided context;
- build a user-selected spread;
- compare cards using explicit metadata;
- export artifacts;
- write to a private journal only through an authorized application command.

Forbidden:
- infer hidden psychological vulnerabilities for targeting;
- silently alter presentation to manipulate behavior;
- create hidden imperatives;
- fabricate physiological or psychological measurements;
- persist personal data outside the declared storage boundary.

## Event model

```ts
type PerceptionEvent =
  | { type: 'CARD_DRAWN'; cardId: CardId; sessionId: string; at: string }
  | { type: 'CARD_FLIPPED'; cardId: CardId; at: string }
  | { type: 'UV_ENABLED'; cardId: CardId; at: string }
  | { type: 'MODE_CHANGED'; mode: string; at: string }
  | { type: 'ACCESSIBILITY_MODE_CHANGED'; mode: string; at: string }
  | { type: 'INTERPRETATION_REQUESTED'; requestId: string; at: string }
  | { type: 'EXPORT_CREATED'; exportId: string; at: string }
  | { type: 'SESSION_ENDED'; sessionId: string; at: string };
```

Telemetry defaults to local/minimal operation. Product events must not become a covert behavioral surveillance system.

## Privacy architecture

### Data minimization
Do not collect data that is not required for the requested feature.

### Local-first preference
Session state, consent and journal data should remain local unless the user explicitly enables synchronization.

### Export control
Exports must disclose whether they contain interpretation text, journal content, identifiers or metadata.

### Retention
Every persisted data category requires an explicit retention rule. Temporary rendering telemetry should have the shortest feasible lifetime.

## Physical/digital bridge

Printed cards and digital records share stable IDs. QR/NFC links resolve only the required card resource and must not silently transmit personal identifiers. Server-side resolution, where used, should be privacy-preserving and rate-limited.

## Accessibility engineering

Required validation includes:

- keyboard-only completion of every functional path;
- reduced-motion mode;
- non-color state communication;
- text equivalents for every perceptual state;
- screen-reader announcements only for meaningful state changes;
- adequate contrast;
- no uncontrolled rapid flashing;
- touch/keyboard target sizing;
- focus order that remains coherent through reveal transitions.

## Security

- untrusted imported card content is sanitized before rendering;
- agent output is treated as untrusted data;
- export functions validate requested format and destination;
- journal data remains behind explicit authorization;
- analytics cannot access journal or interpretation content by default;
- remote AI endpoints, if enabled, use explicit data-sharing consent;
- no credentials or private session material in client logs.

## Test strategy

### Unit
Card schema, state transitions, consent logic, presentation policy and export manifests.

### Property-based
- presentation adaptation never changes authoritative card data;
- disabled effects cannot be activated by model output;
- consent revocation prevents subsequent use of the disabled data path;
- repeated deterministic sessions produce equivalent card sequences.

### Accessibility
Keyboard/E2E matrix, screen-reader semantics, reduced-motion and contrast checks.

### Security
XSS payload fixtures, malicious imported metadata, unsafe URL/export path tests, prompt-injection fixtures in card content and data-boundary tests for optional AI calls.

### Privacy
Verify analytics defaults, data minimization, retention behavior, export disclosure and local-storage separation.

## Performance

Measure:
- initial render;
- card transition latency;
- animation frame stability;
- CPU/GPU overhead of visual effects;
- memory growth over long sessions.

Accessibility mode must remain within the same functional performance envelope.

## Evaluation

Separate product quality from safety outcomes:

| Dimension | Example measurement |
|---|---|
| Usability | task completion rate |
| Accessibility | successful keyboard/screen-reader flows |
| Visual quality | perceptual review rubric |
| Performance | p95 interaction latency |
| Privacy | unauthorized-data-path tests |
| Safety | prohibited-adaptation regression pass rate |
| AI quality | schema validity + human evaluation |

## MVP

1. Versioned 22-card catalog.
2. Responsive renderer.
3. Visible / heat-simulation / UV modes.
4. Accessibility policy controller.
5. Deterministic seeded sessions.
6. Privacy-first local session store.
7. Export manifest + PNG/PDF/JSON exporters.
8. Optional constrained AI interpretation.
9. Security and accessibility regression suite.

## Definition of Done

**Implementation Ready** requires executable contracts for card content, visual modes, presentation policy, consent, event telemetry, persistence, export and AI boundaries. Production use additionally requires accessibility verification, security testing, privacy review and measured performance evidence.

## Non-goals

No covert persuasion engine, psychological profiling system, behavioral addiction optimization or unsupported claim of physiological/neural measurement.

## Relationship to Project 01

Project 05 shares card/session concepts with APEIRON Black System but has a distinct bounded context: **safe adaptive presentation and human-controlled interaction**. Shared card identifiers or infrastructure must not collapse its safety policy into a generic interpretation engine.
