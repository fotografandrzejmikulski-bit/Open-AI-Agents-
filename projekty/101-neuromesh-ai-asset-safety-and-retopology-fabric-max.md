# Project 101 — NeuroMesh AI Asset Safety & Retopology Fabric MAX

## Status
PROPOSED → ARCHITECTURE BASELINE → PROJECT GENESIS 2026-09-10

## Mission
Build a defensive Unreal Engine asset-processing fabric that validates AI-generated 3D assets before they enter a production project, detects unsafe or malformed asset structures, and performs controlled retopology/optimization for downstream game-production pipelines.

## Boundary
P101 owns the **asset safety and geometry-processing boundary**. It does not own the general agentic IDE (P100), the general agent runtime (P40), the OmniCore substrate (P61), or the general self-evolving substrate (P80).

## Source-derived architecture

```text
AI / USER ASSET
      ↓
INGESTION + HASH + PROVENANCE
      ↓
ASSET SAFETY GATE
  ├── package/schema validation
  ├── unsafe object/path checks
  ├── T3D / serialized-data inspection
  ├── injection/payload heuristics
  └── policy + quarantine
      ↓
NEUROMESH ANALYSIS
  ├── topology inspection
  ├── polygon/triangle statistics
  ├── material/texture validation
  └── provenance ledger
      ↓
CONTROLLED RETOPOLOGY
      ↓
NORMAL / UV / MATERIAL REPAIR
      ↓
UE ASSET VALIDATION
      ↓
TEST PROJECT / SANDBOX
      ↓
PROMOTION OR QUARANTINE
```

## Core capabilities
- Unreal Engine asset ingestion;
- MCP-mediated tooling;
- Safety Gate before asset import/use;
- provenance and content hashing;
- quarantine of suspicious assets;
- topology and polygon-density analysis;
- automated retopology/optimization;
- controlled material/UV/normal repair;
- telemetry and audit trail;
- reproducible before/after geometry metrics;
- rollback to original immutable asset.

## Security invariants
- An asset is untrusted until validated.
- Generated geometry is not proof of safety.
- Safety Gate is independent from the generative model.
- Quarantined content cannot silently enter the production asset graph.
- Retopology may not overwrite the immutable source asset.
- UI status is not authoritative safety state.

## Verification
1. Malformed `.uasset` corpus.
2. Suspicious serialized/T3D input corpus.
3. Path traversal and payload tests.
4. Geometry corruption tests.
5. Retopology determinism/repeatability tests.
6. Polygon-count and visual-quality regression tests.
7. Material/UV integrity tests.
8. UE import/open/build tests.
9. Sandbox escape tests.
10. Provenance/hash continuity tests.

## Maturity
Architecture baseline only. Source-derived claims require implementation and reproducible Unreal test-project validation before production readiness is asserted.

## Derived from
P40, P54, P59, P61, P72, P80, P97, P100.

## Primary source witnesses
- `Wniosek Epic MegaGrants AI.PDF`
- prior NeuroMesh/OMEGA-X source corpus from the immediately preceding ingestion batch
