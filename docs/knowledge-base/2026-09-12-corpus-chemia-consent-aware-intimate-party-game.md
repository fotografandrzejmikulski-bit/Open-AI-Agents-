# CHEMIA — Consent-Aware Intimate Two-Player Game Corpus

**Date:** 2026-09-12  
**Source:** user-provided complete game concept and MVP/1.0 specification  
**Classification:** new product/game architecture

## 1. Product definition

CHEMIA is a two-player intimate party game designed around a persistent session loop rather than a one-shot Truth-or-Dare structure.

Core loop:

`LOSuj → WYKONAJ → WYBIERZ REAKCJĘ → ZWIĘKSZ HEAT → ODBLOKUJ KOLEJNĄ WARSTWĘ → LOSUJ PONOWNIE`

A session has no automatic GAME OVER after reaching a target. Players decide when to stop.

## 2. Card taxonomy

Eight categories:

- CONNECTION — personal questions, confessions, memories, fantasies
- TEASE — flirt, tension, looks, provocative choices
- HEAT — bold tasks for both players
- ROLEPLAY — scenarios with defined roles and characters
- DESIRE — preferences, choices, secrets and fantasies
- CHAOS — random rules affecting subsequent rounds
- CONTROL — one partner chooses among safe variants
- AFTERGLOW — calmer, sensual continuation after an intense round

Initial 1.0 corpus target: **520 cards**.

| Category | Target cards |
|---|---:|
| CONNECTION | 60 |
| TEASE | 70 |
| HEAT | 100 |
| ROLEPLAY | 70 |
| DESIRE | 60 |
| CONTROL | 50 |
| CHAOS | 50 |
| AFTERGLOW | 60 |

## 3. Intensity and Heat

Four intensity levels:

`SOFT → SPICY → HOT → EXTREME`

EXTREME is a higher-intensity game state, not a requirement for graphic sexual instructions.

Heat meter:

`0–24 Warm-up | 25–49 Spicy | 50–74 Hot | 75–99 Extreme | 100 Afterglow / Endless Mode`

Both players may jointly increase Heat.

## 4. Card schema

Canonical card fields:

`id, category, intensity, type, text, duration, heat, chain, requires_both, requires_choice, afterglow, tags[], min_players, max_players`

The content model is intentionally separated from game mechanics so that future decks/packs can be added without rebuilding the engine.

## 5. Weighted card selection

Selection is not simple random sampling. Candidate scoring incorporates:

- consent state
- intensity match
- previous cards
- skipped cards/tags
- favorite categories
- Heat
- Chain level
- session duration
- Afterglow state
- player balance
- novelty

Conceptual score:

`category_preference × intensity_match × heat_multiplier × chain_bonus × novelty_bonus × recent_card_penalty × skipped_tag_penalty`

The score is a ranking/selection signal, not a guarantee of suitability. Consent filtering must precede final selection.

## 6. Consent system

Before a session, each player independently sets each category to:

`TAK / MOŻE / NIE`

Global intensity can be adjusted among:

`SOFT / SPICY / HOT / EXTREME`

During play:

- `POMIŃ` never reduces score/Heat and requires no justification.
- Consent can change at any moment.
- A player’s individual preferences remain private from the other player.

For an adult intimate product, the production design should include an explicit 18+ boundary and make consent/reversibility a first-class product invariant.

## 7. Chain Engine

Some cards continue the current round rather than ending it:

`CHAIN ×1 → ×2 → ×3 → ×4 → BONUS`

At each step the system can change category, increase Heat, reduce repetition probability and offer control transfer to the other player.

Example flow:

`CARD → CONTINUE / CHANGE CATEGORY / PARTNER CHOOSES → NEXT CARD WITH CHAIN MODIFIER`

## 8. Secret Mission Engine

Each player receives a private mission at session start.

Mission examples are behavioral/gameplay goals rather than mandatory sexual acts:

- cause three category changes
- make partner choose “JESZCZE JEDNA” twice
- collect three sincere answers
- use all three choice opportunities
- reach a specified Heat level

Completion produces:

`SECRET COMPLETE → BONUS CARD`

The supplied concept also defines `+15 HEAT` as a Secret Mission reward.

## 9. “Jeszcze jedna” mechanic

After every card:

`JESZCZE JEDNA / LOSUJ / ZMIEŃ KLIMAT`

If both choose `JESZCZE JEDNA`, Heat increases by 10 and the selector increases the probability of stronger appropriate categories.

## 10. Afterglow / Endless

At Heat 100:

`AFTERGLOW UNLOCKED`

The session continues rather than ending. Three paths become available:

- `SLOW`
- `CLOSE`
- `RANDOM`

After 10 Afterglow cards, the system offers:

`TAK / LOSOWAĆ / ZAKOŃCZ`

Endless mode removes the automatic time/session ceiling.

## 11. Adaptive personalization

The app stores locally:

- category frequency
- skipped cards
- Heat history
- favorite task types
- session duration
- Chain frequency
- each player’s preferences

The selector adapts future cards without exposing one player’s individual preference profile to the other.

## 12. Two-phone model

Phone A ↔ Phone B.

Private per-player state:

- secret cards
- secret missions
- own answers
- individual preferences

Shared state:

- Heat
- board/session state
- current card
- result
- Chain progress

This implies an explicit privacy boundary and conflict-safe shared-state protocol for any future Bluetooth/Wi-Fi Direct implementation.

## 13. Proposed Android architecture

Target stack:

- Kotlin
- Jetpack Compose
- Room
- encrypted local preferences
- no mandatory account
- later Bluetooth / Wi-Fi Direct
- later Internet mode

Game engine decomposition:

`GameState → ConsentFilter → CardSelector → HeatEngine → ChainEngine → EventEngine → NextCard`

This separation is a core architectural requirement.

## 14. MVP / v1.0 scope

- 8 categories
- 4 intensity levels
- 500+ base cards / 520 target cards
- 100+ Chain cards
- 50 Secret Missions
- Heat 0–100
- Afterglow
- Endless Mode
- two players
- one-phone offline mode
- private cards
- skip without penalty
- session history

## 15. Content architecture

The supplied concept proposes avoiding artificial duplication by combining base cards with modifiers:

`BASE CARD + ROLE + INTENSITY + TIME + CHOICE + CHAIN`

This creates a larger combinatorial content space while keeping the authored base deck manageable.

## 16. Safety and authority invariants

- `CONSENT ≠ SCORE`
- `POMIŃ ≠ FAILURE`
- `PRIVATE PREFERENCE ≠ SHARED STATE`
- `CARD ELIGIBILITY ≠ AUTHORIZATION TO PERFORM`
- `INTENSITY ≠ GRAPHIC CONTENT`
- `HEAT ≠ CONSENT`
- `JESZCZE JEDNA ≠ IRREVERSIBLE COMMITMENT`
- `RANDOMIZATION ≠ PERMISSION`
- `GAME STATE ≠ REAL-WORLD AUTHORITY`

The engine must never interpret Heat, previous participation, mission completion or past consent as permission for a future activity.

## 17. Verification model

The game engine should test at least:

- forbidden-category cards are never selected after `NIE`
- intensity never exceeds the active global/player constraints
- Skip does not decrement score/Heat or create a penalty
- private missions/cards never enter shared-state payloads
- Heat remains within 0–100
- Chain progression terminates correctly at its configured maximum
- Afterglow does not accidentally reset the session
- repeated cards respect the rolling 20-card block
- skipped-tag suppression expires according to explicit policy
- deterministic seeded simulation can reproduce selector decisions for debugging
- session persistence restores state without leaking private data

## 18. Portfolio relation

No existing CHEMIA-specific project was found in `mojealterego/Knowledge-projects`. The concept is therefore classified as a new project rather than an extension of P86 or another existing game/agent project. It can later consume shared engineering primitives from the portfolio, especially governed state machines, local memory, privacy boundaries and verification patterns.
