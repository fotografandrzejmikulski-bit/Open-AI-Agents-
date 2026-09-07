# Project 47 — OmniCore Portfolio Integrity & Project Registry MAX

## Mission
Create a canonical machine-readable registry for the entire OmniCore project portfolio so duplicate concepts, conflicting numbers, successor/alias relationships, evidence lineage and integration dependencies are explicit rather than implicit.

## Problem solved
The portfolio contains legitimate artifacts that evolved over time. Numeric labels alone are therefore insufficient. Project 47 makes identity a **versioned graph with deterministic reconciliation rules**.

## Canonical identity model

```yaml
ProjectIdentity:
  canonical_id:
  title:
  aliases: []
  historical_ids: []
  status:
  lifecycle:
  supersedes: []
  superseded_by: []
  derived_from: []
  depends_on: []
  related_to: []
  canonical_artifact:
  content_sha:
  last_verified_commit:
  evidence_refs: []
  owner_scope:
```

## Reconciliation algorithm

```text
REPOSITORY INVENTORY
        ↓
PROJECT CANDIDATE EXTRACTION
        ↓
TITLE / ID NORMALIZATION
        ↓
SEMANTIC SIMILARITY
        ↓
CONTENT / LINEAGE COMPARISON
        ↓
CANONICAL CANDIDATE
        ↓
EXPLICIT COLLISION RESOLUTION
        ↓
REGISTRY UPDATE
        ↓
REFERENCE INTEGRITY CHECK
```

Semantic similarity is a discovery signal, not authority. Canonicalization requires explicit lineage evidence.

## Identity invariants

1. A numeric label is not sufficient to establish identity.
2. One canonical project may have historical aliases.
3. Renamed or superseded projects retain lineage.
4. Two distinct artifacts with the same historical number never silently overwrite each other.
5. A canonical artifact has a stable path and verifiable content identity.
6. Every project declares lifecycle status.
7. References to a project resolve through `canonical_id` before mutation.
8. Historical artifacts remain distinguishable from current authority.
9. Registry updates themselves are versioned and auditable.
10. A failed or ambiguous reconciliation blocks destructive rename/delete decisions.

## Current canonical family

```text
37  CogniSync Professional
38  Sovereign Edge AI
39  OmniCore Alibaba Cloud Agent Runtime & Cloud Fabric
40  OmniCore Agentic Development & Visual Intelligence Fabric
41  OmniCore Repository Intelligence & Multimodal Action Fabric
42  Open Creator Layer
43  Influence Literacy & Human Agency Lab
44  AI Content Product Studio
45  OmniCore Agentic Content & Commerce Factory
46  CogniSync Open Creator Influence & Content Nexus
47  OmniCore Portfolio Integrity & Project Registry
48  OmniCore Grand Challenge & All-Source Intelligence Foundry
```

This family is the current canonical sequence. Historical duplicate numeric names are retained only as lineage artifacts.

## Machine-readable registry record

```yaml
ProjectRecord:
  canonical_id: 48
  title: OmniCore Grand Challenge & All-Source Intelligence Foundry MAX
  status: architecture
  canonical_artifact: projekty/48-omnicore-grand-challenge-all-source-intelligence-foundry-max.md
  aliases: []
  historical_ids: []
  derived_from:
    - 15
    - 19
    - 26
    - 27
    - 30
    - 32
    - 34
  depends_on:
    - 47
  validates:
    - evidence lineage
    - strategy concretization
    - grand challenge research loop
```

## Project graph

```text
PROJECT
  ├── ALIAS
  ├── SUPERSEDES
  ├── DERIVED_FROM
  ├── DEPENDS_ON
  ├── RELATED_TO
  ├── IMPLEMENTED_BY
  ├── VALIDATED_BY
  ├── DOCUMENTED_BY
  └── EVIDENCED_BY
```

Every edge has:

`source_ref + observed_at + confidence + registry_version`.

## Portfolio compiler

```text
SCAN
 ↓
EXTRACT
 ↓
NORMALIZE
 ↓
COLLISION DETECTION
 ↓
LINEAGE CLASSIFICATION
 ↓
CANONICALIZATION
 ↓
REFERENCE REWRITE
 ↓
INTEGRITY REPORT
```

The compiler should produce:

- canonical registry;
- collision report;
- orphan-reference report;
- stale-reference report;
- lineage graph;
- dependency graph;
- unresolved-ambiguity queue.

## Agent-safe project resolution

Before an agent modifies a project:

```text
USER INTENT
 ↓
PROJECT LOOKUP
 ↓
CANONICAL ID RESOLUTION
 ↓
CURRENT ARTIFACT FETCH
 ↓
DEPENDENCY / LINEAGE CHECK
 ↓
PATCH PLAN
 ↓
AUTHORIZATION
 ↓
MODIFY
 ↓
TEST
 ↓
VERIFY
 ↓
REGISTRY UPDATE
```

No agent may infer canonical identity from a filename alone when a collision or historical alias exists.

## Stale reference protection

Each dependency reference stores the expected artifact identity:

```yaml
Reference:
  canonical_id:
  artifact_path:
  expected_content_sha:
  observed_commit:
  relation:
```

A changed SHA does not automatically mean a project changed identity; it triggers content verification and lineage review.

## Portfolio consistency checks

The registry should continuously test:

```text
PROJECT TABLE ↔ PROJECT FILES
PROJECT LINKS ↔ TARGET ARTIFACTS
ALIASES ↔ CANONICAL IDS
DEPENDENCIES ↔ EXISTING PROJECTS
README ↔ REGISTRY
KNOWLEDGE BASE ↔ PROJECT REFERENCES
```

## Evidence integrity

A registry can store claims about projects, but it must distinguish:

`repository observation ≠ inferred relationship ≠ architectural judgment`.

The registry itself therefore has an evidence ledger.

## Integration with the OmniCore control plane

Project 47 becomes a governance service:

```text
TASK
 ↓
PROJECT / CAPABILITY SEARCH
 ↓
CANONICAL ID RESOLUTION
 ↓
DEPENDENCY CONTEXT
 ↓
RELEVANT KNOWLEDGE
 ↓
SAFE MODIFICATION PLAN
```

## Definition of Done

- canonical IDs resolvable deterministically;
- zero silent numeric-collision overwrites;
- aliases and historical IDs represented explicitly;
- stable artifact/content identity;
- dependency and lineage graphs;
- stale-reference detection;
- orphan-reference detection;
- registry/index consistency checks;
- ambiguity queue;
- auditable registry revisions;
- agent mutation blocked until canonical identity is resolved.
