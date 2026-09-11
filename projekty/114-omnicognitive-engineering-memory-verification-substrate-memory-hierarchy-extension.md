# P114 Extension — Ephemeral / Durable Memory Hierarchy

## Parent

**P114 — OmniCognitive Engineering Memory & Verification Substrate MAX**

## Trigger

RAM-vs-ROM visual reference combined with the existing TurboVec/local semantic-memory work.

## Architectural finding

The source image is useful as a conceptual distinction between volatile working state and durable state. It is not used as a literal hardware model for software storage.

```text
EPHEMERAL MEMORY
  ├─ in-flight context
  ├─ session state
  ├─ cache
  ├─ temporary tool output
  └─ working retrieval state

          ↓ promotion / persistence policy

DURABLE MEMORY
  ├─ memory objects
  ├─ provenance
  ├─ stable IDs
  ├─ learned preferences / facts
  ├─ artifact metadata
  └─ audit history
```

## Memory promotion contract

```yaml
MemoryPromotion:
  source_tier: ephemeral
  target_tier: durable
  memory_id:
  provenance:
  source_refs: []
  confidence:
  created_at:
  version:
  retention:
  supersedes: []
  authorization_scope:
  verification:
```

A cached vector, model context window or tool result must not become durable memory merely because it was retrieved or generated.

## TurboVec integration

The existing TurboVec candidate backend remains responsible for vector retrieval. Stable external IDs, provenance joins and versioned embeddings remain mandatory.

```text
EPHEMERAL QUERY
 ↓
EMBED
 ↓
LOW-BIT INDEX
 ↓
RETRIEVE
 ↓
PROVENANCE JOIN
 ↓
MEMORY OBJECT
 ↓
OPTIONAL DURABLE PROMOTION
```

## Verification requirements

- durable memory has a stable external identity;
- provenance survives compaction/index migration;
- deletion/supersession is explicit;
- embedding/model version is recorded;
- retention and privacy policy are evaluated before persistence;
- temporary credentials and secrets never become durable memory by default;
- promotion is auditable.

## Status

**ARCHITECTURE ENHANCED — IMPLEMENTATION NOT YET VERIFIED**
