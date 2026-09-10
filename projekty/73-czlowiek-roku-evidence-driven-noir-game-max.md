# Project 73 — „Człowiek Roku” — Evidence-Driven Narrative Noir Game MAX

## Status
PROPOSED → ARCHITECTURE BASELINE → PROJECT GENESIS 2026-09-09

## Mission
Create a complete interactive narrative game based on the supplied **„Człowiek Roku”** material, combining documentary-noir aesthetics, evidence-driven investigation, branching narrative state, spatial exploration, authored cinematic sequences and a defensible provenance model.

This is a **concrete product project**, not merely a knowledge artifact and not merely a generic game-design exercise.

The game is designed as an evidence-driven fictional/creative work. Source-derived real-world claims, allegations, identities and historical assertions must never silently become authoritative game facts. Every imported claim has provenance and epistemic status.

## Source-derived basis
Primary repository inputs:

- `docs/knowledge-base/chronos-czlowiek-roku-graphic-noir-production-bible-2026-09-09.md`
- `docs/knowledge-base/chronos-unreal-engine-5-time-rift-architecture-2026-09-09.md`
- `docs/knowledge-base/case-record-evidence-chronology-and-claim-separation-2026-09-09.md`
- `docs/knowledge-base/osint-agent-automation-defensive-architecture-2026-09-09.md`
- `docs/knowledge-base/2026-09-10-corpus-apeiron-casino-ccr-pornlandia-omnicore-neuroshield.md`

Portfolio integrations:

- Project 32 — Deep OSINT Agent & Zero-Trust Evidence Engine
- Project 41 — Repository Intelligence & Multimodal Action Fabric
- Project 50 — Physical Game & Phygital Experience Foundry
- Project 52 — Adaptive Game Designer & Procedural Playtest Foundry
- Project 54 — Epistemic Signal & Adversarial Control Fabric
- Project 57 — Multimodal Intelligence & Cognitive Interface Fabric
- Project 58 — Monitorability-Aware Oversight & Verification Fabric
- Project 71 — Physical Artifact Manufacturing & Symbolic Interface Factory
- Project 72 — Cross-Framework Agent Assurance & Runtime Verification Fabric
- Project 82 — CCR Transmedia Graphic-Novel Universe MAX

## CCR relationship
The newly ingested CCR adaptation establishes a larger graphic-novel/transmedia lineage in which „Ludzie Roku” is one component of the trilogy. Project 73 remains the **game-specific** implementation, while Project 82 owns the complete graphic-novel/transmedia production system.

Shared material must therefore use explicit lineage tags:

```text
CCR SOURCE
 ├── GRAPHIC-NOVEL / TRANSMEDIA → Project 82
 └── INTERACTIVE GAME / EVIDENCE NOIR → Project 73
```

This prevents the same narrative corpus from being mistaken for two unrelated source universes while preserving independent product requirements.

## Product thesis
The central gameplay loop is not simply:

`EXPLORE → SHOOT / PUZZLE → REWARD`

It is:

```text
OBSERVE
   ↓
COLLECT
   ↓
CLASSIFY
   ↓
CONNECT
   ↓
CHALLENGE
   ↓
INTERPRET
   ↓
DECIDE WHAT TO TRUST
   ↓
ACT
   ↓
OBSERVE CONSEQUENCES
   ↓
UPDATE THE CASE
```

The player is rewarded for **better reconstruction of a situation**, not for accepting the most dramatic explanation.

## 1. Game pillars

### 1.1 Evidence over exposition
Important narrative information is distributed through documents, environments, dialogue, objects, spatial clues, timelines and audiovisual traces. The game maintains an explicit distinction between:

- observation;
- source statement;
- corroborated evidence;
- inference;
- hypothesis;
- unresolved contradiction;
- fictionalized narrative fact.

### 1.2 Documentary noir
The visual language uses restrained cinematic framing, environmental storytelling, topographic specificity, controlled contrast, archival textures and deliberate pacing. Noir is a presentation system, not an instruction to sensationalize unverified claims.

### 1.3 Spatial investigation
Locations are designed as evidence-bearing spaces. The player can revisit places as new information changes the interpretation of previously observed details.

### 1.4 Consequence through epistemic state
Choices can change not only plot state but also the player's **case model**. Acting on weak evidence can close opportunities, create false leads or force later correction.

### 1.5 No omniscient player
The player never receives a magical truth channel. UI confidence is derived from evidence state and may remain unresolved.

## 2. Core state architecture

```yaml
GameState:
  world_version:
  narrative_branch:
  current_location:
  actor_states: []
  discovered_evidence: []
  evidence_links: []
  hypotheses: []
  contradictions: []
  unresolved_questions: []
  player_actions: []
  consequence_flags: []
  timeline_state:
  cinematic_state:
  save_revision:
```

Evidence is immutable once acquired; interpretation is versioned separately.

## 3. Evidence model

```yaml
EvidenceItem:
  id:
  source_type:
  source_reference:
  observed_content:
  acquisition_context:
  timestamp:
  location:
  provenance:
  epistemic_status:
  confidence:
  corroboration_refs: []
  contradiction_refs: []
  sensitivity:
  fictionalization_status:
```

Permitted epistemic statuses:

`OBSERVED | ATTRIBUTED | CORROBORATED | INFERRED | HYPOTHESIS | CONTRADICTED | UNKNOWN | FICTIONALIZED`

The system must never automatically upgrade `HYPOTHESIS` to `FACT`.

## 4. Investigation graph

```text
LOCATION
  ├── PERSON / ACTOR
  ├── OBJECT
  ├── DOCUMENT
  ├── EVENT
  ├── STATEMENT
  └── DIGITAL TRACE
        ↓
      EVIDENCE EDGE
        ↓
   SUPPORT / CONTRADICT / TEMPORAL / SPATIAL / SOURCE-DEPENDENT
```

Every relationship carries edge type, provenance and confidence.

## 5. Temporal reasoning

The case board maintains:

- event time;
- observation time;
- publication/acquisition time;
- player-discovery time;
- revision time.

This prevents the common narrative error of treating the time at which the player discovers evidence as the time at which the underlying event occurred.

## 6. Narrative state machine

```text
PROLOGUE
   ↓
CASE OPENED
   ↓
EXPLORATION
   ↓
EVIDENCE ACCUMULATION
   ↓
HYPOTHESIS FORMATION
   ↓
CONTRADICTION / NEW LEAD
   ↓
RECONSTRUCTION
   ↓
CONSEQUENTIAL DECISION
   ↓
OUTCOME
   ↓
EPILOGUE / REASSESSMENT
```

The game supports controlled branching without requiring every branch to be a completely separate game. Shared world-state variables drive divergent scenes and consequences.

## 7. Chronos / TimeRift technical lineage

The supplied Chronos implementation material provides a useful real-time architecture direction:

- Unreal Engine 5;
- temporal/environmental transitions;
- camera/state control;
- particle/memory visualization concepts;
- level streaming;
- Lumen/Nanite-oriented presentation;
- persistent narrative state.

Project 73 treats these as implementation components rather than as the product identity itself.

Recommended separation:

```text
NARRATIVE TRUTH MODEL
        ↓
GAME STATE
        ↓
EVIDENCE / TEMPORAL GRAPH
        ↓
UE5 SYSTEM ADAPTERS
        ↓
RENDER / AUDIO / INPUT
```

Rendering must never become the authoritative source of narrative state.

## 8. Investigation UI

The player receives a layered interface:

1. **Case Board** — entities, events, evidence and hypotheses.
2. **Timeline** — temporal ordering and uncertainty windows.
3. **Evidence Viewer** — source and provenance metadata.
4. **Location Map** — spatial relationships.
5. **Contradiction Panel** — unresolved conflicts.
6. **Decision Surface** — available actions and their information requirements.
7. **Journal** — player-authored interpretation, explicitly separated from system evidence.

The UI must distinguish:

`WHAT THE GAME KNOWS` from `WHAT THE PLAYER BELIEVES`.

## 9. Cinematic system

Cinematics are state-driven rather than hard-coded exclusively as linear movies.

```yaml
Cinematic:
  id:
  trigger:
  prerequisites: []
  camera_profile:
  actor_state:
  evidence_dependencies: []
  dialogue_variant:
  world_changes: []
  interruption_policy:
  resume_state:
```

A cinematic can be resumed, skipped where appropriate and deterministically reconstructed from state.

## 10. Environmental storytelling

Every major location receives an evidence budget:

```text
PRIMARY CLUES
SECONDARY CONTEXT
MISLEADING BUT FAIR SIGNALS
ATMOSPHERIC DETAIL
OPTIONAL LORE
```

Misleading evidence must be fair: it can support an incorrect hypothesis but must not fabricate impossible information or punish players for failing to guess developer intent.

## 11. Audio as evidence

Audio is not merely ambience. It can carry:

- dialogue;
- environmental sound;
- timing cues;
- source recordings;
- acoustic location clues;
- music state;
- deliberate absence/silence.

Audio evidence must use the same provenance model as visual evidence.

## 12. AI-assisted NPC architecture

NPC behavior is modeled through bounded state and authorized capabilities:

```text
NPC GOALS
   ↓
KNOWN WORLD STATE
   ↓
PERMITTED KNOWLEDGE
   ↓
DIALOGUE POLICY
   ↓
PLAYER INPUT
   ↓
STATE TRANSITION
   ↓
VERIFIED WORLD UPDATE
```

NPCs must not hallucinate authoritative case facts. If their knowledge is incomplete, that incompleteness is part of their state.

## 13. AI investigation assistant — optional

An in-game assistant may help the player organize evidence, but it must not solve the case by fiat.

Allowed outputs:

- evidence clustering;
- duplicate detection;
- timeline suggestions;
- contradiction surfacing;
- source summaries;
- alternative hypotheses.

Disallowed architecture:

`MODEL → SECRET TRUE ANSWER → PLAYER`

The assistant must expose uncertainty and source boundaries.

## 14. UE5 technical architecture

Recommended modules:

```text
UCR_GameState
UCR_EvidenceSubsystem
UCR_InvestigationGraph
UCR_TimelineSubsystem
UCR_NarrativeStateMachine
UCR_CinematicDirector
UCR_CaseBoardUI
UCR_LocationEvidenceComponent
UCR_NPCStateComponent
UCR_SaveVersionManager
UCR_ReplayRecorder
UCR_VerificationSubsystem
```

### Authoritative layers

```text
AUTHORITATIVE
  ├── GameState
  ├── EvidenceRegistry
  ├── NarrativeState
  └── SaveRevision

DERIVED
  ├── UI
  ├── camera state
  ├── visual effects
  └── audio presentation
```

Derived state cannot overwrite authoritative state.

## 15. Save/replay integrity

Every consequential decision receives:

```yaml
DecisionRecord:
  sequence:
  state_revision:
  available_evidence_hash:
  hypothesis_state_hash:
  selected_action:
  authorization:
  preconditions:
  postconditions:
  resulting_state_hash:
```

This allows a complete case reconstruction and regression testing of narrative branches.

## 16. Anti-spoiler architecture

The project must distinguish between:

- design documentation;
- production metadata;
- player-facing copy;
- marketing copy;
- spoiler-sensitive assets.

Marketing and onboarding surfaces must not expose hidden outcomes, identity reveals or late-game causal explanations.

## 17. Accessibility

Required baseline:

- subtitle customization;
- scalable UI;
- color-independent evidence states;
- readable contrast;
- reduced-motion option;
- remappable controls;
- audio descriptions where appropriate;
- non-audio evidence alternatives;
- adjustable investigation pacing.

No essential clue may depend exclusively on a single sensory modality.

## 18. Verification and playtesting

Testing is divided into:

### Narrative tests
- every required state has a reachable path;
- no impossible branch state;
- no contradictory authoritative facts;
- no soft-lock from missed optional evidence;
- endings are reachable from valid state trajectories.

### Evidence tests
- provenance survives save/load;
- evidence hashes remain stable;
- contradictions are reproducible;
- inference never silently becomes source fact.

### Technical tests
- level streaming;
- save/reload;
- state restoration;
- cinematic interruption/resume;
- UI state reconstruction;
- replay determinism.

### Player tests
- comprehension;
- time-to-first-useful-action;
- hypothesis formation;
- false-lead fairness;
- cognitive load;
- accessibility;
- spoiler leakage.

## 19. Safety and epistemic boundary

Real-person allegations, institutional accusations or sensitive claims appearing in source material remain source-attributed and unverified unless independently established. The game may fictionalize, transform or abstract such material, but must not present an unverified real-world claim as established fact merely because it appears in a source document.

OSINT mechanics are implemented for fictionalized/in-game investigation and authorized evidence analysis. No unauthorized reconnaissance, credential acquisition, covert targeting or real-world operational exploitation is part of the project.

## 20. Production pipeline

```text
SOURCE / CREATIVE INTENT
        ↓
CLAIM + FICTION BOUNDARY
        ↓
WORLD BIBLE
        ↓
EVIDENCE ONTOLOGY
        ↓
NARRATIVE STATE MODEL
        ↓
UE5 GREYBOX
        ↓
INTERACTION PROTOTYPE
        ↓
CINEMATIC / AUDIO / ART PASS
        ↓
EVIDENCE + NARRATIVE QA
        ↓
ACCESSIBILITY QA
        ↓
BLIND PLAYTEST
        ↓
SPOILER / PROVENANCE AUDIT
        ↓
RELEASE CANDIDATE
```

## 21. Definition of Done

1. A playable vertical slice exists in UE5.
2. Evidence, hypothesis and fictionalized narrative state are separate typed objects.
3. Investigation graph and timeline survive save/load.
4. At least one major narrative branch is fully state-driven.
5. Cinematics can resume from authoritative state.
6. NPC knowledge is bounded and auditable.
7. Player-facing UI distinguishes evidence from interpretation.
8. No essential clue is sensory-single-channel dependent.
9. Replay/state regression tests detect narrative-state corruption.
10. Spoiler-sensitive marketing surfaces are independently reviewed.
11. Source-derived real-world claims remain provenance-bound.
12. Blind playtesting demonstrates that the investigation is understandable without requiring a predetermined developer conclusion.
13. Release candidate has reproducible build, content manifest and evidence-state regression suite.

## Maximum-evolution target

Project 73 is intentionally a **product application of the portfolio's game, OSINT, multimodal, evidence, verification and physical-artifact capabilities**. It should become the reference narrative game implementation through which Projects 32, 50, 52, 54, 57, 58, 71 and 72 can be exercised against a complex, stateful creative workload.
