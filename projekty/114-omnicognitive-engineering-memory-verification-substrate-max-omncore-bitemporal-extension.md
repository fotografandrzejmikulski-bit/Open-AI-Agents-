# P114 Extension — OmniCore Bitemporal Memory / Agent History

## Parent
P114 — OmniCognitive Engineering Memory & Verification Substrate MAX

## Trigger
OCN 49.0/50.1/51.1 Agents Builder documents describing bitemporal graph memory and historical state reconstruction.

## Finding
The supplied OmniCore architecture reinforces P114's existing provenance-bearing memory model with an explicit bitemporal framing: memory records should distinguish the time a fact is valid in the modeled world from the time the system learned/recorded it.

## Canonical object

```yaml
MemoryEvent:
  memory_id: stable_external_id
  valid_from:
  valid_to:
  recorded_at:
  supersedes: []
  source_refs: []
  provenance:
  confidence:
  state_hash:
```

## Retrieval model

```text
QUERY TIME
   ↓
VALID-TIME FILTER
   ↓
TRANSACTION/RECORD-TIME FILTER
   ↓
PROVENANCE JOIN
   ↓
CURRENT OR HISTORICAL MEMORY VIEW
   ↓
CONFIDENCE / CONTRADICTION CHECK
```

Historical state is evidence about what the system recorded or modeled at a given time; it is not automatically proof that the historical model was correct.

## Integration with vector memory

The existing P114 TurboVec contract remains:

`VECTOR SLOT ≠ MEMORY IDENTITY`

The stable external `memory_id` and temporal/provenance metadata must survive index rebuilds, deletion/reinsertion and compaction.

## Evolution safety

The DGM/L-Genes/D-Genes model from the supplied OCN documents is compatible with P114 only when immutable safety invariants remain outside the mutable evolutionary state. Historical memory must make it possible to reconstruct which policy/model/genotype version produced a decision.

## Status
`ARCHITECTURE ENHANCED — BITEMPORAL MEMORY CONTRACT; IMPLEMENTATION NOT VERIFIED`
