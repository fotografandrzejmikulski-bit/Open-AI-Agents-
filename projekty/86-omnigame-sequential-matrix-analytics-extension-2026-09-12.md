# Project 86 Extension — Sequential Matrix Analytics / Monety i Świnie

## Parent
Project 86 — OmniGame Text-to-Android Factory MAX

## Status
SOURCE-INGESTED → ANALYTICS EXTENSION → VALIDATION REQUIRED

## Mission
Add a reproducible sequential-data analytics layer to Project 86 for games whose mechanics are represented by chronological event matrices and finite-state stake/progression rules.

The immediate source case is the supplied **Monety i Świnie** specification and a 49-column date-indexed matrix covering 23.01.2025–06.01.2026, with an overlap on 22.07.2025 between the two supplied images.

## Architecture

```text
VISUAL / TABULAR SOURCE
        ↓
GRID + OCR EXTRACTION
        ↓
NORMALIZED EVENT MATRIX
        ↓
DATA QUALITY / PROVENANCE
        ↓
SEQUENCE ANALYZER
        ├── FREQUENCY
        ├── RUNS / GAPS
        ├── TRANSITIONS
        ├── CLUSTERING
        └── CHANGE-POINT CANDIDATES
        ↓
NULL-MODEL / RANDOMIZATION BASELINE
        ↓
BACKTEST ENGINE
        ↓
EFFECT-SIZE / UNCERTAINTY
        ↓
STRATEGY CANDIDATE
        ↓
UGDL GAME RULE / SIMULATION ARTIFACT
        ↓
RUNTIME TEST + READBACK
```

## Canonical data model

```yaml
SequentialMatrix:
  schema_version:
  matrix_id:
  source_refs: []
  date_range:
  domain_size: 49
  columns: [01..49]
  rows: []
  aggregates:
    ONT: []
  extraction:
    method:
    confidence:
    duplicate_dates: []
```

A row should preserve the original date and every column state. Aggregates such as `ONT` are stored separately from raw observations.

## Monety i Świnie state model

The supplied rules are compiled as a finite-state machine rather than embedded as informal prompt instructions.

```text
CURRENT STAKE
      ↓
SPIN
      ↓
EVENT COUNT / EVENT TYPE
      ├── THREE COINS
      ├── THREE PIGS
      └── BLUE CAPSULE CONDITION
      ↓
RULE EVALUATION
      ↓
NEXT STAKE
```

The three supplied stake bases are retained as source parameters:

- Base I: `1, 2, 3, 15, 50, 150, 500`
- Base II: `1, 3, 15, 50, 150, 500, 2500`
- Base III: `1, 15, 50, 150, 500, 2500, 8000`

The special transition rules are represented as explicit policy conditions and must be tested independently.

## Analytics controls

The extension must distinguish:

- observation from prediction;
- frequency from probability;
- correlation from causation;
- in-sample fit from out-of-sample performance;
- visual pattern from statistically supported structure;
- simulation output from real-world outcome evidence.

A strategy is not promoted merely because it reproduces historical highlighted cells or produces a favorable backtest.

## Verification gates

1. Image-to-grid extraction is reproducible.
2. Date ordering is validated.
3. The 22.07.2025 overlap is detected and deduplicated.
4. All 49 columns are present for each normalized row.
5. `ONT` values reconcile with their source transcription without assigning an unsupported semantic meaning.
6. Missing/ambiguous cells are explicitly represented rather than guessed.
7. Historical strategy evaluation uses a time-respecting train/test split.
8. Null/randomized baselines are included.
9. Multiple-testing effects are controlled when searching many candidate patterns.
10. Confidence intervals/effect sizes accompany performance claims.
11. Simulation cannot be represented as observed external evidence.
12. Game-rule changes require versioned artifacts and readback.

## Security / governance

The analytics layer is informational and simulation-oriented. It does not authorize financial or gambling transactions, alter external accounts, or infer ownership/authorization from the matrix.

If the system is later used with a real-money environment, policy, jurisdiction, age/eligibility, spending limits and explicit authorization must be separate controls. Statistical analysis does not constitute a guarantee of outcome.

## Portfolio decision

**No new standalone project.** The supplied matrix is a concrete dataset/mechanics case that materially strengthens Project 86's game compiler, procedural simulation and verification capabilities. It also provides a reusable benchmark for visual-table ingestion and temporal sequence analysis across the wider P100/P77 verification architecture.
