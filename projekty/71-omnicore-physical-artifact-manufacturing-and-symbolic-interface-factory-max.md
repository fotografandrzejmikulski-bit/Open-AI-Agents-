# Project 71 — OmniCore Physical Artifact Manufacturing & Symbolic Interface Factory MAX

## Mission
Create a production-grade compiler from symbolic/game semantics to reproducible physical artifacts and their digital companions, using the Apeiron 2.0 / Black Apeiron 2.2 material and game-production corpus.

## Architecture
```text
SEMANTIC / GAME STATE
        ↓
SYMBOLIC PROJECTION
        ↓
CARD / BOARD / TOKEN SPEC
        ↓
VISUAL + PHYSICAL PROFILE
        ↓
PREPRESS / MANUFACTURING PLAN
        ↓
PROTOTYPE
        ↓
PHYSICAL QC + PLAYTEST
        ↓
BATCH RELEASE
        ↓
DIGITAL COMPANION / REGISTRY
```

## Physical artifact schema
```yaml
ArtifactSpec:
  artifact_id:
  design_version:
  semantic_hash:
  ruleset_hash:
  substrate:
  thickness:
  optical_profile:
  ink_profile:
  tactile_profile:
  registration_tolerance:
  accessibility_profile:
  batch_id:
  qc_profile:
```

## Apeiron-derived manufacturing layer
The supplied Apeiron 2.0 report proposes transparent optical-grade PVC around 0.30 mm, high light transmission, controlled surface friction and multi-card overlay behavior. It also specifies hybrid opaque/translucent/transparent print layers, white-underprint levels, digital metallic effects, tactile finishing and a physical Light Matrix Board. These are treated as **engineering hypotheses/specification targets** until supplier-batch measurements establish actual transmission, haze, registration, friction, durability and overlay readability.

The supplied design defines a 78-card system whose meaning emerges through stacked layers rather than from isolated cards. It also proposes a server-rack-style box, a light-matrix board and a System Kernel Manual. These become first-class ArtifactSpec components rather than informal decoration.

## Black Apeiron 2.2 / reveal-state layer
Black Apeiron 2.2 extends the same artifact lineage with dark/glitch aesthetics, thermochromic and UV reveal states, black-polymer presentation and a Codex-style manual. Project 71 formalizes these as **rule-defined reveal states**:

```text
VISIBLE STATE
     ↓ defined interaction
REVEAL EVENT
     ↓
SECOND INFORMATION LAYER
     ↓
RESTORE / RESET
```

A hidden layer must never silently function as a behavioral-control channel. Any puzzle, UV, thermal, QR or overlay reveal is part of the declared game/artifact rules.

## Cyberpunk / Neon & Glitch design profile
The supplied 60-card Cyberpunk Tarot specification contributes a separate visual profile: System Core / Subroutines, Neon / Chrome / Data / Wires, glitch, datamoshing and pixel-sorting aesthetics. Project 71 treats this as a reusable **visual manufacturing profile**, not a new canonical project. It can coexist with the 78-card Apeiron lineage when a future edition explicitly declares the mapping.

## Symbolic semantics
```text
SYMBOL → INTERPRETATION
OBSERVATION → EVIDENCE
RULE → GAME STATE
REVEAL → DECLARED INFORMATION STATE
```

These are different channels. A symbolic interpretation does not become factual state, diagnosis or guaranteed prediction.

## Manufacturing verification
```text
DIMENSION
→ THICKNESS
→ TRANSMISSION / HAZE
→ PRINT REGISTRATION
→ SURFACE FRICTION
→ REVEAL RELIABILITY
→ STACK ALIGNMENT
→ DURABILITY
→ ACCESSIBILITY
→ PLAYER TEST
→ BATCH REPLICATION
```

No supplier specification is promoted to verified physical fact without measurement. Single-prototype success does not establish batch reliability.

## Phygital continuity
Physical event detection must carry artifact identity, event sequence and version metadata. Out-of-order, duplicate or stale events are explicitly rejected or reconciled.

## Safety and cognitive-integrity boundary
Several supplied Apeiron documents deliberately use terms such as neuro-trap, subconscious commands, sensory addiction, hidden commands and compulsive collection. Project 71 preserves these as source-derived design history but does **not** treat covert manipulation, eye strain, sensory overload, subliminal instruction or compulsive monetization as production requirements.

Allowed design direction:

```text
OPTICAL ILLUSION → DISCLOSED EXPERIENCE
HIDDEN LAYER → RULE-DEFINED PUZZLE
TACTILE EFFECT → ACCESSIBILITY-TESTED INTERACTION
COLLECTION → OPTIONAL COMPLETION LOOP
QR / DIGITAL REVEAL → EXPLICIT USER ACTION
```

## Novel contribution
Project 71 upgrades the earlier card compiler into a **manufacturing-aware artifact factory**, joining semantic identity, rules, physical process control, optical layering, reveal-state engineering, QC, accessibility and digital state without making the physical artifact a hidden control channel.
