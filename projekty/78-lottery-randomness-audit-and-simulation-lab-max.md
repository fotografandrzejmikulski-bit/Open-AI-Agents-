# Project 78 — Lottery & Casino Randomness Audit & Simulation Lab MAX

## Status
PROPOSED → ARCHITECTURE BASELINE → PROJECT GENESIS 2026-09-09

## Mission
Build a reproducible research and audit environment for studying lottery-draw randomness, casino RNG behavior, physical-machine hypotheses and statistical anomalies. The project deliberately separates statistical analysis from gambling advice and does not promise winning predictions.

## Why this is a new project
The original project was justified by a concrete lottery-randomness artifact. The casino corpus broadens the same research boundary into online-game RNG, provably-fair protocols, house-edge mathematics and backend integrity. This is an evolution of the audit domain, not a project for exploiting gamblers.

## Architecture
```text
DRAW / GAME DATA / MACHINE OBSERVATIONS
            ↓
DATA QUALITY + PROVENANCE
            ↓
NULL MODEL / DECLARED RNG MODEL
            ↓
DISTRIBUTION + DEPENDENCE TESTS
            ↓
PHYSICAL / PRNG HYPOTHESIS MODELS
            ↓
MONTE CARLO / RESAMPLING
            ↓
BLINDED OUT-OF-SAMPLE EVALUATION
            ↓
CALIBRATION + UNCERTAINTY
            ↓
AUDIT REPORT
```

## Modules
1. Draw/Game Ingestor — versioned results with provenance.
2. Rules/RNG Schema Registry — explicit rules, RNG declarations and protocol versions.
3. Statistical Baseline — exact combinatorial probabilities and null models.
4. RNG Audit — reproducible tests for distribution, independence and implementation consistency.
5. Provably-Fair Verifier — verification of declared server/client seed, hash and nonce protocols where applicable.
6. House-Edge Analyzer — mathematical expected-value analysis, not a promise of profitable play.
7. Physical-System Model — legitimate observations such as machine, ball-set or environmental parameters.
8. Simulation Engine — reproducible seeds, Monte Carlo and bootstrap/resampling.
9. Agent Ensemble — independent analysts with disagreement reporting rather than false consensus.
10. Evaluation Harness — rolling-origin and blind holdout tests.
11. Audit UI — transparent metrics, uncertainty and protocol evidence.

## Critical source correction
Behavioral manipulation, biometric feedback and persuasive control proposals are treated as cognitive-security threat models, not project objectives. The audit system must never optimize gambling engagement, exploit vulnerability or manipulate users.

## Research questions
- Are observed sequences statistically compatible with the declared randomization mechanism?
- Does an implementation correctly follow its declared provably-fair protocol?
- Do physical observations explain any reproducible deviation from a null model?
- Are apparent “hot/cold” patterns stable out of sample?
- Does an added model beat a properly specified null baseline after correction for multiple testing?
- Can another implementation reproduce the same result independently?

## Integrity and safety gates
- No guaranteed-win claims.
- No fabricated certainty.
- No personalized gambling strategy.
- Preserve the distinction between statistical anomaly and exploitable bias.
- Require out-of-sample replication before claiming predictive signal.
- Clearly label simulations, hypotheses and observations.
- Behavioral manipulation is never an optimization target.

## Portfolio integration
Extends Projects 51, 55, 61, 72 and related probability/simulation infrastructure while absorbing casino RNG/provably-fair/house-edge audit material.

## Definition of Done
- Historical datasets are provenance-linked.
- Null models are explicit and independently reproducible.
- RNG/protocol checks are reproducible.
- All stochastic experiments have recorded seeds/configuration.
- Anomaly findings survive holdout/replication tests before promotion.
- UI never disguises uncertainty as certainty.
- The system produces an auditable statistical report rather than a betting recommendation.

## Iteration 13 — Global Lotto Engineering Model

The new global Lotto compendium is incorporated as a formal game-matrix and combinatorial-design layer.

### GameMatrix

```yaml
GameMatrix:
  game_id:
  region:
  pool_a:
    m:
    n:
  pool_b:
    m:
    n:
  player_pick_p:
  prize_categories_q:
  draw_without_replacement:
  jackpot_rule:
  paytable_version:
  rule_source:
```

For single-pool games, exact-match and k-match probabilities are evaluated against the hypergeometric baseline. For multi-pool games, independent pool probabilities are multiplied only when the independence assumption is valid and explicitly declared.

### Wheeling / combinatorial-design module

Full systems and reduced/wheeling systems are modeled as set-cover/combinatorial-design objects. A wheel may reduce the number of tickets while preserving a declared lower-tier guarantee under explicit assumptions; it does not increase the mathematical probability of a single combination beyond the tickets actually purchased.

```yaml
WheelSpec:
  universe:
  block_size:
  blocks: []
  coverage_t:
  guarantee_condition:
  omitted_combinations:
  cost:
```

The audit UI must distinguish **coverage guarantee** from **jackpot guarantee**.

### All-or-Nothing and Keno

All-or-Nothing games are represented with symmetry checks where the complement event has equivalent probability under the declared draw model. Keno receives a variable `p` parameter and operator-specific paytable versions.

### EV / variance boundary

The source material explicitly distinguishes negative expected value from variance redistribution. Project 78 now stores:

```yaml
EconomicProfile:
  ticket_cost:
  expected_payout:
  expected_value:
  variance:
  jackpot_overlay_assumption:
  paytable_version:
  sensitivity:
```

A full or reduced system is never labeled “better” without specifying whether the metric is coverage, variance, expected value, cost, or probability of a particular prize tier.

### Regional rules as versioned evidence

The source surveys Powerball, Mega Millions, EuroMillions, EuroDreams, SuperEnalotto, Polish Lotto, All-or-Nothing, Keno and other regional systems. Those figures are treated as historical/source snapshots. Live rules, prices and prize tables require current primary-source verification before operational use.

### Iteration 13 validation gates

1. Exact combinatorial baseline matches an independently implemented reference.
2. Multi-pool probability is validated against declared independence assumptions.
3. Wheel guarantees are tested exhaustively for small instances and sampled/verified for larger instances.
4. Paytable changes are versioned and never silently mixed across dates.
5. EV calculations include ticket cost and payout rules.
6. Simulation seeds and configuration are recorded.
7. Apparent patterns undergo holdout and multiple-testing correction.
8. No statistical output is converted into a personalized betting recommendation.
