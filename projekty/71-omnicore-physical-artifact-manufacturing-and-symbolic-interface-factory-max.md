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
The supplied Apeiron RC document proposes optical-grade PVC, approximately 0.30 mm thickness, high light transmission and controlled surface friction for multi-card overlays. Project 71 treats these as design requirements until supplier-batch tests confirm them.

## Black-box / void design layer
Black Apeiron 2.2 explores concealment, black-on-black treatment, thermochromic/UV effects and glitch aesthetics. Project 71 translates the useful design principle into **explicit information-layer rendering**: some content may be intentionally hidden until a rule-defined reveal event, but concealment cannot become an undisclosed behavioral-control mechanism.

## Symbolic semantics
```text
SYMBOL → INTERPRETATION
OBSERVATION → EVIDENCE
RULE → GAME STATE
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
```

## Phygital continuity
Physical event detection must carry artifact identity, event sequence and version metadata. Out-of-order, duplicate or stale events are explicitly rejected or reconciled.

## Novel contribution
Project 71 upgrades the earlier card compiler into a **manufacturing-aware artifact factory**, joining semantic identity, rules, physical process control, QC, accessibility and digital state without making the physical artifact a hidden control channel.
