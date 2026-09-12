# PROJECT EVOLUTION — ITERATION 69

**Date:** 2026-09-12  
**Trigger:** CHEMIA complete intimate two-player game specification

## Portfolio decision

**NEW PROJECT: P122 — CHEMIA**

A repository search found no existing CHEMIA-specific project. The concept is a distinct game-product architecture rather than another generic card generator and therefore receives its own project lineage.

## P122 additions

- 8-category deck and 520-card v1.0 target;
- four intensity levels;
- Heat 0–100 with Afterglow transition;
- weighted adaptive CardSelector;
- anti-repeat and skipped-tag suppression;
- Chain ×1–×4;
- Partner Choice branching;
- private Secret Missions;
- `JESZCZE JEDNA` dual-confirmation mechanic;
- Afterglow and Endless continuation;
- private per-player adaptation;
- one-phone offline MVP;
- future Bluetooth/Wi-Fi Direct two-phone architecture;
- Kotlin/Jetpack Compose/Room implementation boundary;
- deterministic replay and property-based state-machine verification.

## Canonical engine

`GameState → ConsentFilter → CardSelector → HeatEngine → ChainEngine → EventEngine → NextCard`

## Privacy architecture

`PLAYER_PRIVATE_STATE ≠ SHARED_GAME_STATE`

Secret cards, missions, answers and individual preferences remain private. Shared state is limited to the explicitly defined game projection.

## New reusable primitives

- consent-aware-card-filter
- adaptive-weighted-card-selector
- heat-progression-engine
- chain-state-machine
- private-secret-mission-engine
- player-choice-branching
- afterglow-continuation-state
- two-player-private-shared-state-model
- seeded-selector-replay
- consent-game-property-tests

## Safety invariants

`HEAT ≠ CONSENT`  
`RANDOM ≠ PERMISSION`  
`SKIP ≠ FAILURE`  
`PRIVATE ≠ SHARED`  
`INTENSITY ≠ GRAPHIC CONTENT`

Past participation, Heat, mission completion or previous consent cannot implicitly authorize a future activity.

## Relation to existing portfolio

P86 remains the general game-production factory. P122 is the product/game architecture and should consume shared build, testing and verification primitives rather than duplicate the factory layer.

**Status:** `architecture-integrated`
