# Project 47 — OmniCore Portfolio Integrity & Project Registry MAX

## Mission
Create a canonical machine-readable registry for the entire OmniCore project portfolio so duplicate concepts, conflicting numbers, successor/alias relationships and integration dependencies are explicit rather than implicit.

## Problem solved
The repository currently contains legitimate project artifacts that can share numerical identities or preserve historical names after architectural evolution. The registry makes identity a graph instead of relying on filenames alone.

## Canonical identity model

```yaml
ProjectIdentity:
  canonical_id:
  title:
  aliases:
  historical_ids:
  status:
  lifecycle:
  supersedes:
  derived_from:
  depends_on:
  related_to:
  canonical_artifact:
  evidence:
```

## Registry invariants

1. A numeric label is not sufficient to establish identity.
2. One canonical project may have historical aliases.
3. A renamed or superseded project must preserve lineage.
4. Two distinct artifacts with the same historical number must never silently overwrite each other.
5. Canonical links point to stable artifact paths and commit evidence.
6. Every project declares status: research, architecture, prototype, implementation, archived or superseded.

## Graph

```text
PROJECT
  ├── ALIAS
  ├── SUPERSEDES
  ├── DERIVED_FROM
  ├── DEPENDS_ON
  ├── IMPLEMENTED_BY
  ├── VALIDATED_BY
  └── DOCUMENTED_BY
```

## Portfolio compiler

```text
SCAN REPOSITORY
 ↓
IDENTIFY PROJECT ARTIFACTS
 ↓
NORMALIZE TITLES / IDS
 ↓
DETECT COLLISIONS
 ↓
CLASSIFY LINEAGE
 ↓
BUILD CANONICAL GRAPH
 ↓
GENERATE INDEX / REPORT
```

## Why this matters

As the portfolio grows, project-level architectural quality becomes dependent on portfolio-level integrity. Duplicate IDs, stale READMEs and untracked successor relationships can otherwise produce false assumptions in future agent planning.

## Integration with OmniCore control plane

The registry becomes a read-only capability for planners:

```text
USER REQUEST
 ↓
PROJECT SEARCH
 ↓
CANONICAL ID RESOLUTION
 ↓
DEPENDENCY / LINEAGE GRAPH
 ↓
RELEVANT PROJECT CONTEXT
```

Agents must resolve canonical identity before modifying or extending an existing project.

## Evaluation

- zero silent ID collisions;
- 100% canonical artifacts resolvable;
- lineage coverage;
- stale-reference detection;
- README/index consistency;
- dependency graph completeness.

## Definition of Done

Project 47 is complete when the repository can answer deterministically: which project is canonical, which names are aliases, what changed, what it superseded, what depends on it and which file is authoritative.
