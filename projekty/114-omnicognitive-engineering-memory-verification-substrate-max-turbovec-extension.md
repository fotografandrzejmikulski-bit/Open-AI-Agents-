# P114 Extension — TurboVec / Low-Bit Local Semantic Memory

## Parent
P114 — OmniCognitive Engineering Memory & Verification Substrate MAX

## Trigger
10-image corpus, specifically the TurboVec/TurboQuant reference.

## Architectural finding
TurboVec is a candidate local vector-index backend for semantic memory. Current external documentation describes TurboQuant compression at 2–4 bits per coordinate, online ingestion without a separate training phase, local execution and filtered search. The repository also documents SIMD implementations and incremental persistence.

## Candidate memory path

```text
EMBEDDING
 ↓
LOW-BIT VECTOR INDEX
 ↓
FILTER / ALLOWLIST
 ↓
TOP-K RETRIEVAL
 ↓
PROVENANCE JOIN
 ↓
MEMORY OBJECT
 ↓
CONTEXT BROKER
```

## Identity requirement
Raw vector slots must never be treated as durable memory identity. Current TurboVec documentation notes that positional slots can change after removal operations. P114 therefore requires a stable external memory ID mapped to the vector index slot.

```yaml
MemoryVector:
  memory_id: stable_external_id
  vector_slot: backend_specific
  embedding_model:
  dimensions:
  index_version:
  source_refs: []
  created_at:
  supersedes: []
  confidence:
```

## Verification backlog
- recall/latency comparison against existing HNSW/pgvector baselines;
- memory-footprint benchmark;
- filtered retrieval correctness;
- crash/recovery and incremental-save tests;
- stable-ID integrity under deletion/reinsertion;
- provenance preservation after compaction;
- embedding-version migration tests.

## Status
`CANDIDATE BACKEND — NOT IMPLEMENTED / NOT BENCHMARKED LOCALLY`
