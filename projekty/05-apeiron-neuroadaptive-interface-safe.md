# 05 — APEIRON NEUROADAPTIVE INTERFACE — SAFE EDITION

## Purpose
Evolve the supplied Aperion card/application concept into a high-end interactive cognitive-art product while explicitly removing covert persuasion, hidden commands and manipulative engagement mechanisms.

The source design uses symmetry, Moiré patterns, micro-typography, an attentional anchor, Spot UV, thermochromic/UV layers and glitch aesthetics as intentional perceptual effects. fileciteturn195file4L2-L27 fileciteturn195file4L43-L67

## Product direction

Turn the experience from a "neuro-trap" into a **user-controlled perceptual instrument**:

```text
visual stimulus
     ↓
voluntary exploration
     ↓
user-selected mode
     ↓
interactive interpretation
     ↓
reflection / creative output
```

No hidden behavioral directives. No covert commands. No dark-pattern loops. No attempt to override informed user choice.

## Digital architecture

```text
React / Next.js UI
      │
      ├── Card Engine
      ├── Perception Engine
      ├── Accessibility Layer
      ├── Session State
      └── Export Layer
              │
          Domain API
              │
       Optional Agent Runtime
              │
          MCP interface
```

## Card engine

Each card is a versioned content object:

```ts
type Card = {
  id: string;
  title: string;
  archetype: string;
  visualLayers: VisualLayer[];
  interactionProfile: InteractionProfile;
  accessibilityText: string;
  provenance: Provenance;
};
```

## Perceptual modes

### Visible
High-contrast artistic composition.

### Heat / touch simulation
Digital approximation of thermochromic reveal for devices without physical thermochromic media.

### UV
Reveal explicitly labeled hidden artwork or metadata.

### Accessibility
Reduce animation, motion, contrast fluctuation and perceptual intensity. Provide text descriptions and keyboard operation.

## Agent capabilities

An optional agent may:
- explain a card's visual composition;
- generate a reflective interpretation from user-provided context;
- build a spread according to user-selected rules;
- compare cards statistically or semantically;
- export a reading/artifact;
- maintain a private session journal.

The agent must not infer sensitive psychological traits for manipulation or alter UI behavior to increase compulsive use.

## Event model

```text
CARD_DRAWN
CARD_FLIPPED
UV_ENABLED
MODE_CHANGED
INTERPRETATION_REQUESTED
INTERPRETATION_RETURNED
EXPORT_CREATED
SESSION_ENDED
```

Avoid retaining unnecessary behavioral telemetry.

## Physical/digital bridge

The printed deck can use the same stable card IDs as the digital system. A QR/NFC marker may resolve to card metadata, but should not silently transmit personal data.

## Creative upgrade

The original Aperion aesthetic can be expanded into two complementary systems:

**Aperion 2.0 — Light / Order**
- white + cyan + silver
- symmetry
- geometric grid
- controlled reveal

**Black System 2.2 — Shadow / Disruption**
- black + graphite + red
- broken symmetry
- glitch / noise
- explicit "system state" visual language

## Safety-by-design

Every hidden layer must be discoverable as an artistic mechanism. Any encoded text should be semantically inert or informational. Avoid hidden imperative language aimed at changing the user's behavior without awareness.

## MVP

1. 22-card database schema.
2. Responsive card renderer.
3. three visual modes.
4. accessible mode.
5. deterministic draw engine with seeded sessions.
6. export to JSON/PNG/PDF.
7. optional AI interpretation using a constrained schema.
8. privacy-first analytics disabled by default.

## Evaluation

Measure:
- render performance
- animation smoothness
- accessibility compliance
- deterministic reproducibility
- interpretation consistency
- user satisfaction
- false-positive personalization

## Future
Integrate this project with the project's MCP layer so the deck becomes an agent-addressable creative application rather than a standalone UI demo.