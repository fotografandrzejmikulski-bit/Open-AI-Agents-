# Project Evolution — 2026-09-12 — Iteration 78

## Input

Two supplied dense visual matrices plus the accompanying **Monety i Świnie** game-sequence specification.

## Evidence extracted

- 49-number domain (`01`–`49`).
- Chronological rows from 23.01.2025 through 06.01.2026.
- The two images overlap on 22.07.2025; unique date span = 349 dates.
- Blue cells represent source-defined highlighted states/events.
- A bottom `ONT` row supplies 49 aggregate values; their visible sum is 330.
- Source-defined stake bases and transition rules are retained without adding an interpretation not supported by the material.

## Decision

**Primary integration: Project 86 — OmniGame Text-to-Android Factory MAX.**

No new standalone project is warranted. The material is a concrete game-mechanics/data-analysis case and directly strengthens the existing game compiler and simulation lineage.

## New capability layer

`SEQUENTIAL-MATRIX-ANALYTICS`

Capabilities:

- dense visual table extraction;
- date/number normalization;
- temporal event matrix representation;
- finite-state rule compilation;
- frequency/run/gap/transition analysis;
- null-model and randomization baselines;
- time-respecting backtesting;
- effect-size and uncertainty reporting;
- provenance-preserving simulation artifacts.

## New primitives

- `sequential-matrix`
- `matrix-row-observation`
- `matrix-cell-state`
- `matrix-aggregate-vector`
- `matrix-extraction-record`
- `state-transition-rule`
- `strategy-backtest-record`
- `null-model-baseline`
- `simulation-provenance-record`

## Verification doctrine

`HIGHLIGHTED CELL ≠ PREDICTION`

`FREQUENCY ≠ PROBABILITY`

`BACKTEST ≠ GUARANTEE`

`SIMULATION ≠ EXTERNAL EVIDENCE`

`PATTERN ≠ CAUSALITY`

`MODEL OUTPUT ≠ AUTHORIZATION`

The `ONT` label is preserved as source terminology. Its semantics remain unresolved until an authoritative definition is supplied.

## Cross-project impact

- **P86**: direct extension for game mechanics compilation, simulation and testing.
- **P100**: reusable visual-data ingestion, agentic analytics and verification primitive.
- **P77**: methodological input for formal separation of observed data, inferred structure, hypothesis and verified result; no mathematical theorem is implied.

## Next verification target

If the raw source data become available, reconstruct the full 349×49 matrix, reconcile the duplicate 22.07.2025 row, verify every highlighted cell, and run out-of-sample/null-model analysis before treating any sequence as predictive.
