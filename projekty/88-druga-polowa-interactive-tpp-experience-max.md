# Project 88 — Druga Połowa Interactive TPP Experience MAX

## Status
PROPOSED → ARCHITECTURE BASELINE → PROJECT GENESIS 2026-09-10

## Mission
Create a distinct interactive adaptation of the comic **„Druga Połowa”** as a third-person narrative exploration experience in Unreal Engine 5.4+, preserving the source's winter-night, dreamlike atmosphere while translating memory, time and emotional states into gameplay systems.

## Product identity
This is a separate product from Project 73 (`Człowiek Roku`) and Project 82 (CCR transmedia universe). Shared technologies may be reused, but narrative canon and asset lineage remain independent.

## Core loop

```text
EXPLORE
 ↓
OBSERVE
 ↓
FIND MEMORY TRACE
 ↓
INTERACT
 ↓
TIME / PERCEPTION CHANGE
 ↓
RECONSTRUCT RELATIONSHIP
 ↓
NEW STATE OF THE WORLD
```

The source describes TPP exploration, time manipulation, memory particles and an atmosphere-first design rather than combat-first gameplay.

## Gameplay pillars

- **Metaphysical exploration** — an oneiric representation of locations.
- **Time stop / temporal rupture** — time can become an interaction state rather than a conventional level transition.
- **Soul Seeker** — a flashlight/light-based interaction mechanism.
- **Memory Particles** — collectible/interactable traces that reveal fragments of the world.
- **Interactive snow** — environmental material and movement feedback.
- **Contemplative movement** — pacing and traversal support the narrative rather than maximize action density.

## Character architecture

```text
PLAYER CHARACTER
 ↓
PLAYER CONTROLLER
 ↓
INTERACTION COMPONENT
 ↓
WORLD OBJECT / MEMORY ACTOR
 ↓
NARRATIVE STATE TRANSITION
```

The supplied source describes Andrzej and Paula as the central relational axis. Character traits are gameplay hypotheses derived from the source, not clinical diagnoses.

## UE5 architecture

Recommended modules:

```text
UDR_GameMode
UDR_Character
UDR_InteractionComponent
UDR_TimeStateSubsystem
UDR_MemoryParticle
UDR_EnvironmentState
UDR_CinematicDirector
UDR_SaveState
UDR_AudioState
UDR_VerificationSubsystem
```

## Memory Particle

A `MemoryParticle` is a typed world object with:

```yaml
MemoryParticle:
  id:
  location:
  memory_type:
  reveal_condition:
  source_scene:
  narrative_state:
  interaction_result:
  audiovisual_profile:
```

## Temporal state

```yaml
WorldTimeState:
  axis:
  world_revision:
  active_layer:
  transition:
  persistent_changes: []
```

Temporal changes must be deterministic and saveable. Presentation effects cannot become the authoritative narrative state.

## Technical direction

The source proposes UE5.4+, Lumen, Nanite and Niagara. These are treated as implementation options whose actual performance must be measured on target hardware.

Interaction uses Enhanced Input and a typed `IInteractable` contract. Memory particles can use Niagara for attraction/repulsion visual behavior.

## Audio / atmosphere

Winter night, silence, snow, spatial ambience and material response are first-class narrative systems. Audio state is versioned alongside world state so that changes remain reproducible.

## Verification

- every memory trace has a reachable reveal condition;
- temporal transitions are reversible where design requires it;
- save/load preserves world state;
- no essential narrative state depends on one sensory channel;
- performance budgets are measured on target GPU/CPU;
- generated code and assets pass static/runtime checks;
- cinematic interruptions restore authoritative state.

## Portfolio integration

- Project 50 — Physical Game & Phygital Experience Foundry
- Project 52 — Adaptive Game Designer & Procedural Playtest Foundry
- Project 57 — Multimodal Intelligence & Cognitive Interface Fabric
- Project 72 — Cross-Framework Agent Assurance
- Project 73 — Człowiek Roku game architecture (technology reuse only)
- Project 81 — Voice-Narrative AI Game Engine (optional future voice layer)
- Project 86 — OmniGame Text-to-Android Factory (future adaptation path)

## Definition of Done

1. UE5 vertical slice exists.
2. TPP exploration and interaction are playable.
3. Time-state and MemoryParticle systems work deterministically.
4. At least one complete narrative sequence is state-driven.
5. Atmosphere systems survive save/load.
6. Performance and accessibility are measured rather than assumed.
7. Project assets remain lineage-separated from other narrative universes.

## Iteration 25 evolution
Visual inspection of the supplied 5-page `Druga połowa` extract confirms a sequential-art progression from a snowy nocturnal city encounter through recognition/intimacy to a warm domestic morning and a new shared chapter. This is now a direct visual source witness for the atmosphere, pacing, relational-state transitions and contrast between cold exterior and warm interior states. The PDF contains no machine-readable text; the visual evidence is therefore explicitly page-image-derived.
