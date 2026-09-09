# Project 76 — NEURO-SYNC Sensory Browser Game Engine MAX

## Status
PROPOSED → ARCHITECTURE BASELINE → PROJECT GENESIS 2026-09-09

## Mission
Evolve the supplied single-file `NEURO-SYNC: TERMINAL` prototype into a production-grade, browser-native interactive experience while preserving its terminal/CRT aesthetic, command-driven interaction, synchronized audiovisual presentation and deterministic game-state architecture.

## Product identity
This is a distinct project from the physical-game and UE5 projects. Its core deliverable is a **web-native sensory narrative runtime** that can ship as a lightweight standalone experience.

## Source-derived baseline
The prototype already contains:
- full-screen HTML/CSS layout;
- CRT scanlines and glitch effects;
- Canvas2D animated geometry;
- terminal-style chat/log;
- synchronization progress UI;
- command input;
- Web Audio initialization after user interaction;
- stereo oscillator routing;
- lightweight NLP/command responses and hidden commands. fileciteturn189file1L51-L85 fileciteturn189file7L319-L327

## Target architecture
```text
BOOT
 ↓
CAPABILITY CHECK
 ↓
AUDIO / VISUAL INITIALIZATION
 ↓
COMMAND ROUTER
 ↓
NARRATIVE STATE MACHINE
 ↓
SENSORY STATE SYNTHESIS
 ↓
RENDER + AUDIO
 ↓
STATE PERSISTENCE
 ↓
REPLAY / TELEMETRY
```

## Modules
1. **Boot Controller** — user gesture, capability detection and graceful fallback.
2. **Audio Engine** — Web Audio graph, volume ceiling, pause/mute and device-loss recovery.
3. **Visual Engine** — Canvas2D renderer, CRT, geometry, glitch and performance tiers.
4. **Command Engine** — typed command grammar and explicit state transitions.
5. **Narrative Engine** — branching state, hidden discoveries and replayable progression.
6. **Accessibility Layer** — subtitles, visual-only/audio-reduced modes, motion reduction and keyboard control.
7. **Persistence Layer** — versioned save state and migration.
8. **Integrity Harness** — deterministic command tests, state-transition tests and replay comparison.

## State contract
```yaml
GameState:
  version:
  session_id:
  sync_level:
  discovered_flags: []
  narrative_node:
  command_history: []
  sensory_profile:
  accessibility_profile:
  seed:
```

## Sensory design boundary
The source prototype uses audiovisual immersion. The production system must keep all sensory effects voluntary, interruptible and configurable. No hidden physiological targeting, covert persuasion or dependency optimization is part of the product contract.

## Performance tiers
```text
Tier A — Canvas + audio + full effects
Tier B — reduced visual effects
Tier C — static/low-motion presentation
Tier D — text-first accessibility mode
```

## Portfolio integration
Extends Projects 01, 07, 22, 42, 44, 50, 51, 52, 53, 54, 57, 65 and 72 while remaining a separate browser-game runtime.

## Definition of Done
- Runs as a standalone web artifact without a build-time server dependency.
- Audio starts only after permitted user interaction.
- Commands are typed and deterministic.
- Narrative state is versioned and replayable.
- Accessibility alternatives exist for audio and motion.
- Sensory effects can be interrupted immediately.
- State transitions have automated tests.
- Performance tiers work on desktop and mobile browsers.
- No sensory feature is an authorization mechanism.
