# P114 Extension — TurboVec / Low-Bit Local Semantic Memory

## Parent
P114 — OmniCognitive Engineering Memory & Verification Substrate MAX

## Trigger
The earlier TurboVec corpus established a candidate low-bit vector backend. The 2026-09-12 database-indexing corpus adds relational indexing/query-plan principles that sharpen the selection and verification contract.

## Architectural finding
TurboVec remains a candidate local vector-index backend for semantic memory. The database corpus reinforces that vector indexing must be evaluated as a workload-specific indexing strategy rather than treated as a universal database optimization.

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

## Database verification layer

P114 now requires retrieval experiments to capture:

- query plan / execution diagnostics where the backend exposes them;
- latency distribution rather than a single timing;
- recall/precision or task-retrieval success;
- memory footprint;
- ingest/update/delete cost;
- filter selectivity;
- index build/compaction cost;
- stale/bloated index behavior;
- embedding-model/version compatibility.

The generic relational rules from the supplied cheatsheet — cardinality, selectivity, composite-index order and EXPLAIN/ANALYZE — are transferred as **verification concepts**, not blindly as vector-index implementation rules.

## Identity requirement

Raw vector slots must never be treated as durable memory identity. Positional slots can change after removal operations. P114 therefore requires a stable external memory ID mapped to the vector index slot.

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
- embedding-version migration tests;
- workload-shaped selectivity experiments;
- query-plan/IO evidence where supported;
- write-amplification measurement.

## Status
`CANDIDATE BACKEND — NOT IMPLEMENTED / NOT BENCHMARKED LOCALLY`
