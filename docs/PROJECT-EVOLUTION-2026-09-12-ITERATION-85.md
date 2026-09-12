# Project Evolution — 2026-09-12 — Iteration 85

## P125 — Prawda czy Wyzwanie: Android Ultimate Chaos

The supplied React prototype and its successive feature descriptions were formalized as a dedicated Android game project.

### Architectural decision
P125 owns title-specific gameplay, Android UX, content architecture and session state. P86 remains the implementation/build/verification substrate for reproducible Android artifacts; P99 supplies mobile product and LiveOps strategy.

### Main retained mechanics
- 2–20 players
- Truth / Dare
- procedural multi-engine generation
- no-repeat persistent deck
- intensity levels
- timer
- dice series
- scoring and leaderboard
- wildcard
- custom content
- sound effects and Polish TTS
- dynamic visual cards
- offline-first operation

### Android migration
The React prototype is a functional reference only. Browser APIs and remote assets are removed from the core. Target implementation is Kotlin + Jetpack Compose with typed domain state, local persistence and deterministic prompt IDs.

### Safety redesign
The supplied punitive clothing-removal forfeits and explicit sexual generator are not carried into the default Android release. The architecture instead uses safe forfeits, a persistent PAS/SAFETY PAUSE action, pre-display content validation and policy-controlled content packs.

### Verification
P86 must verify source → build → sign → install → smoke test → readback → evidence. Build success alone does not establish release trust.
