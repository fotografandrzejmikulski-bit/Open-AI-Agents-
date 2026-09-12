# P114 Extension — CineMatrix Film World State / RAG

## Parent
P114 — OmniCognitive Engineering Memory & Verification Substrate MAX

## Contribution
CineMatrix provides a concrete long-form narrative-memory workload for P114: screenplay, character state, locations, prior shots and continuity constraints must be retrievable without loading the complete film into the LLM context window.

## Retrieval path

```text
FILM STATE
 ↓
EMBEDDING / INDEX
 ↓
FILTER BY PROJECT / SCENE / ENTITY / VERSION
 ↓
TOP-K RETRIEVAL
 ↓
PROVENANCE JOIN
 ↓
CONTEXT BROKER
 ↓
LLM / DIRECTOR
```

## Memory object

```yaml
memory_id:
project_id:
entity_type:
entity_id:
source_ref:
content:
embedding_model:
index_version:
created_at:
supersedes: []
confidence:
validation_state:
```

## Required invariants

- memory identity is stable and independent of vector slot;
- retrieved context carries provenance;
- stale scene state cannot silently overwrite newer state;
- project/character/location scope filters are explicit;
- embedding-version migrations are tracked;
- retrieval quality is evaluated against film-continuity tasks.

## Film-specific benchmarks

- character costume/prop recall;
- location geometry recall;
- previous-scene event recall;
- dialogue continuity recall;
- camera/lighting continuity recall;
- retrieval latency distribution;
- memory footprint;
- false-context rate;
- stale-context rejection.

## Status
`ARCHITECTURE EXTENSION — IMPLEMENTATION / LOCAL BENCHMARKS NOT VERIFIED`
