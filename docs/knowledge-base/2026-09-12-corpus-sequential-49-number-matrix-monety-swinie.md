# Knowledge Corpus — Sequential 49-Number Matrix / Monety i Świnie

## Source

Two supplied image tables plus the accompanying textual specification.

The tables are daily/chronological matrices with 49 numbered columns (`01`–`49`) and blue-highlighted cells. The visible date range is **23.01.2025–06.01.2026**. The two images overlap on **22.07.2025**, so the unique chronological range contains **349 dates**.

## Source-derived observations

- The matrix has a fixed 49-column numerical domain.
- Each row is keyed by a calendar date.
- Blue cells encode selected events/states for the corresponding date/number pair.
- The first supplied image covers 23.01.2025 through 22.07.2025.
- The second supplied image covers 22.07.2025 through 06.01.2026.
- The bottom `ONT` row provides one numeric summary value for each of the 49 columns.
- The supplied visible `ONT` values are:

```text
01 02 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25
03 12 06 07 11 03 01 19 00 00 07 22 21 00 03 07 09 23 05 05 01 01 14 07 02

26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47 48 49
00 09 00 03 03 04 02 08 26 25 06 08 02 02 04 07 01 06 13 01 02 00 04 05
```

- Sum of the visible `ONT` row is **330**; this is a transcription-derived arithmetic property, not an interpretation of what `ONT` means.
- The accompanying game specification describes a sequence system called **Monety i Świnie**: rotation at multiplier x1 until three coins appear; after three coins the stake is raised; reaching three pigs returns the stake to 1.
- Three stake bases are supplied:
  - Base I: `1, 2, 3, 15, 50, 150, 500`
  - Base II: `1, 3, 15, 50, 150, 500, 2500`
  - Base III: `1, 15, 50, 150, 500, 2500, 8000`
- Special rules supplied by the source: if three coins occur faster than after three spins at a stake, the stake is not raised; blue capsules at the beginning of a high stake can cause a downward stake transition.

## Data-model interpretation for engineering

The matrix can be represented as a time-indexed binary/event tensor:

```text
(date, number_01..49) → state/event
```

with a separate per-number aggregate vector `ONT[01..49]`.

The game rules can be represented as a finite-state transition system:

```text
STAKE LEVEL
   ↓
SPIN / EVENT OBSERVATION
   ↓
COIN COUNT / PIG COUNT / CAPSULE CONDITION
   ↓
TRANSITION RULE
   ↓
NEXT STAKE LEVEL
```

The matrix and the game-state machine should remain separate artifacts. Historical observations must not be silently converted into causal rules.

## Verification boundary

The images alone do **not** establish:

- what `ONT` semantically means;
- whether blue cells are independent observations, predictions, recommendations or generated selections;
- whether the sequence has predictive power;
- whether any apparent numerical pattern is statistically significant;
- whether the stake bases produce a positive expected value;
- whether the game is random, deterministic, or externally constrained.

Therefore the corpus is classified as **SOURCE_DERIVED / DATASET_CANDIDATE**, not as a validated prediction model.

## Required analytical pipeline

```text
IMAGE TABLES
  ↓
OCR / GRID EXTRACTION
  ↓
DATE + NUMBER NORMALIZATION
  ↓
BLUE-CELL EVENT MATRIX
  ↓
DATA QUALITY / DUPLICATE-DATE CHECK
  ↓
ONT RECONCILIATION
  ↓
DESCRIPTIVE STATISTICS
  ↓
SEQUENCE / RUN / TRANSITION ANALYSIS
  ↓
OUT-OF-SAMPLE TEST
  ↓
NULL-MODEL / RANDOMIZATION BASELINE
  ↓
EFFECT-SIZE + UNCERTAINTY
  ↓
ONLY THEN: STRATEGY CANDIDATE
```

Critical rule: in-sample pattern discovery must never be presented as out-of-sample predictive validation.

## Engineering value

This corpus strengthens the existing game-production and agentic analytics architecture by supplying a concrete test case for:

- structured extraction from dense visual tables;
- temporal matrix normalization;
- finite-state game-rule compilation;
- sequence analytics;
- reproducible simulation;
- strategy backtesting;
- adversarial/null-model testing;
- provenance-preserving visual-data ingestion.

No standalone predictive claim is created from the corpus.
