# P125 — Prawda czy Wyzwanie: Android Ultimate Chaos

## Status
DESIGNED / ANDROID PRODUCT SPECIFICATION

## Product definition
Native Android party game derived from the supplied React prototype. The Android edition preserves the core game loop—players, random turn selection, truth/dare choice, procedural challenge generation, no-repeat memory, intensity, timers, statistics, custom content, sound/TTS, visual cards and dice sequences—while replacing browser-specific implementation with a production Android architecture.

The supplied prototype is treated as a **product reference**, not as production-ready Android source code. Its JSX/template syntax contains malformed fragments and browser-only dependencies; the implementation must be rebuilt against a typed Android domain model and independently verified.

## Relationship to existing portfolio
- **P86 — OmniGame Text-to-Android Factory MAX:** build substrate, reproducible Android builds, APK/AAB generation, signing isolation and runtime verification.
- **P99 — OmniGame Mobile Product & LiveOps Strategy Engine MAX:** mobile product, retention, analytics and LiveOps strategy.
- **P125:** owns the actual game design, content architecture, Android UX and gameplay state machine for this title.

## Target
Android phones first; portrait orientation as default, with tablet/responsive support as a later compatibility target.

## Recommended implementation
Kotlin + Jetpack Compose + Material 3, with a local-first architecture.

Core layers:
`UI → ViewModel → Game Engine → Content Repository → Persistence → Audio/TTS → Analytics`

No web runtime is required for the core game.

## Canonical game state
```text
SETUP
→ PLAYING
→ CHOOSING
→ REVEAL
→ ACTIVE_CHALLENGE
→ COMPLETION / SKIP
→ NEXT_TURN
→ SESSION_SUMMARY
```

Additional states:
`DICE_ROLL`, `SERIES`, `CUSTOM_CONTENT`, `SETTINGS`, `SAFETY_PAUSE`.

## Core mechanics

### Players
- 2–20 players.
- Add/remove players.
- Stable player IDs, not array indexes, for persistence and statistics.
- Round-robin or configurable randomized turn order.

### Truth / Dare
Two primary actions:
- `PRAWDA`
- `WYZWANIE`

The game engine chooses content according to the selected content profile and intensity policy.

### Multi-engine architecture
Four content families are retained from the supplied concept:
- `PHYSICAL`
- `DIGITAL`
- `SOCIAL`
- `TRUTH`

For the default public-safe release, physical content is constrained to non-sexual, non-dangerous party actions. An age-gated content-pack architecture can exist independently, but it must not silently bypass platform/content policy or consent safeguards.

### Procedural generation
The generator composes typed components instead of storing one giant list:

`ACTION + TARGET + CONTEXT + STYLE + DURATION / CONDITION`

Every generated prompt receives a deterministic `promptId` from its normalized components plus content-pack version. This makes duplicate detection reliable even across app restarts.

### No-repeat deck
Persistent session history:
`usedPromptIds: Set<PromptId>`

Generation algorithm:
1. sample a valid candidate;
2. normalize it;
3. calculate PromptId;
4. reject if already used;
5. validate safety/content constraints;
6. return and persist atomically.

When the valid candidate pool is exhausted, the UI reports deck exhaustion instead of entering an uncontrolled generation loop.

### Intensity
Replace the prototype's free-form 0–100 behavior with typed levels:
`CALM`, `CLASSIC`, `PARTY`, `EXTREME`.

A numeric intensity slider may still be presented, but it maps to policy bands and never authorizes prohibited or unsafe content.

### Dice / Series
A dice roll from 1–6 creates a `SeriesState`:
`requiredTurns`, `completedTurns`, `skippedTurns`.

The current player remains locked into the series until completion or explicit termination.

### Timer
Per-challenge timer with configurable duration. Timer expiration transitions to `SKIPPED_BY_TIMEOUT` and cannot automatically force a physically unsafe action.

### Skip / Safety
Replace the punitive clothing-removal mechanism from the supplied prototype with safe forfeits configurable by the group, e.g. points penalty, humorous title, extra harmless challenge, or loss of a privilege.

A persistent `PAS / SAFETY PAUSE` control is available during every challenge.

## Scoring
Per-player statistics:
```text
completed
skipped
timeouts
points
streak
best_streak
truth_count
dare_count
series_completed
```

Leaderboard titles are generated from statistics, not humiliation or personal profiling.

## Wildcard / Royal Privilege
Optional special card with controlled capabilities:
- choose from approved challenge pool;
- nominate another player;
- modify timer within policy limits;
- trigger a harmless bonus round.

The wildcard cannot bypass content-policy, consent, or safety validation.

## Custom content
Users can add:
- custom truths;
- custom dares;
- custom categories.

Each custom item is stored with:
`author`, `createdAt`, `contentPack`, `safetyStatus`, `sourceType`.

Custom content is treated as untrusted input and passed through local validation before entering the active deck.

## Audio
Native Android audio layer:
- dice roll;
- reveal;
- success;
- skip/fail;
- UI feedback.

Prefer generated/simple local audio assets or Android audio synthesis over remote URLs.

TTS:
- Polish locale where available;
- explicit mute control;
- manual replay;
- optional automatic readout;
- graceful fallback when Polish voice data is unavailable.

## Visual system
The supplied React prototype's neon/glass/gradient direction becomes a coherent Android design system:
- dark premium base;
- dynamic category accent;
- glass-like cards implemented with Android-native surfaces;
- large one-hand controls;
- animated reveal;
- dice animation;
- progress indicators;
- reduced-motion accessibility mode.

External texture URLs are removed from the production core. Visual effects are local and deterministic.

## Android UX screens
1. Splash / title.
2. New game setup.
3. Player management.
4. Game rules / safety agreement.
5. Intensity and content-pack selection.
6. Main turn screen.
7. Truth/Dare selection.
8. Challenge reveal card.
9. Timer state.
10. Dice roll.
11. Series progress.
12. Completion / skip.
13. Leaderboard.
14. Custom content editor.
15. Settings / audio / TTS.
16. Session summary.
17. Safety pause overlay.

## Data model
```text
GameSession
Player
ContentPack
PromptTemplate
GeneratedPrompt
PromptHistory
Turn
SeriesState
ScoreState
CustomPrompt
Settings
Campaign/ReleaseMetadata
```

All persisted state is versioned for future migrations.

## Offline-first requirement
The complete core game must work without network access.

No dependency on:
- Unsplash;
- remote textures;
- external API calls;
- browser speech synthesis;
- remote prompt generation.

Optional future cloud features must degrade gracefully to offline mode.

## Content architecture
Content is separated from code:
```text
content/
  packs/
    classic.json
    party.json
    extreme.json
  schemas/
    prompt.schema.json
```

Content-pack versioning allows new question/challenge libraries without changing the game engine.

## Safety architecture
The engine uses:
`GENERATE → VALIDATE → DISPLAY`

Never:
`GENERATE → DISPLAY`

Validation rules cover:
- physical danger;
- coercion;
- illegal acts;
- self-harm;
- harassment/humiliation escalation;
- privacy violations;
- unsafe digital actions;
- sexual content according to the selected distribution policy.

The player can always choose `PAS` / `SAFETY PAUSE` without a punitive physical consequence.

## Verification contract
P86 build pipeline must verify:
`SOURCE → BUILD → SIGN → INSTALL → SMOKE TEST → READBACK → ARTIFACT EVIDENCE`

Acceptance must include:
- clean install;
- app launch;
- add/remove players;
- minimum-player validation;
- turn progression;
- truth generation;
- dare generation;
- no-repeat behavior;
- timer;
- dice series;
- scoring;
- custom content;
- TTS fallback;
- audio mute;
- process recreation/state restoration;
- portrait layout;
- offline operation;
- accessibility checks;
- safety pause;
- persistence across restart.

## Reproducible release
The Android artifact is not considered trusted merely because Gradle reports success.

Required evidence:
- source revision;
- dependency lock state;
- build environment;
- Gradle task output;
- APK/AAB checksum;
- signing metadata;
- install result;
- automated smoke-test report;
- screenshot set;
- runtime logs.

Where the P86/F-Droid-style verification infrastructure is available, an independent rebuild should be used for release verification.

## Analytics
Local session analytics first:
- rounds;
- category distribution;
- completion rate;
- skip rate;
- average challenge duration;
- deck exhaustion;
- most-used content packs.

Any future cloud analytics require explicit opt-in and privacy-preserving aggregation.

## Release strategy
### V1 — Core
Players, truth/dare, safe procedural engine, no-repeat deck, timer, scoring, audio/TTS, premium UI, offline.

### V1.1 — Chaos
Dice series, wildcard, more content packs, custom prompts, advanced statistics.

### V1.2 — Polish
Animations, haptics, accessibility, tablet layout, performance tuning.

### V2 — Live Content
Versioned downloadable content packs and optional analytics, subject to explicit consent and distribution constraints.

## Product invariants
- `REACT PROTOTYPE ≠ ANDROID PRODUCTION BUILD`
- `GENERATED PROMPT ≠ VERIFIED SAFE PROMPT`
- `CONTENT PACK ≠ AUTHORIZATION`
- `TIMER EXPIRATION ≠ CONSENT`
- `SKIP ≠ FAILURE OF USER SAFETY`
- `APK BUILD SUCCESS ≠ TRUSTED APK`
- `SIGNED APK ≠ VERIFIED RELEASE`
- `ANALYTICS ≠ USER IDENTITY`
- `CUSTOM CONTENT ≠ TRUSTED INSTRUCTION`

## Definition of Done
P125 is ready for Android implementation when:
1. the Compose navigation/state model is frozen;
2. the content schema is validated;
3. the procedural generator has deterministic duplicate detection;
4. safety validation is implemented before display;
5. all core screens have stable UI specifications;
6. the offline data layer passes migration tests;
7. P86 produces a reproducible APK/AAB;
8. emulator/device smoke tests pass;
9. runtime readback confirms the intended state transitions;
10. release evidence is stored with the artifact lineage.
