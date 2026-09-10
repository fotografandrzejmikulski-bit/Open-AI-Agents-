# Project 78 — Lottery & Casino Randomness Audit & Simulation Lab MAX

## Status
PROPOSED → ARCHITECTURE BASELINE → PROJECT GENESIS 2026-09-09

## Mission
Build a reproducible research and audit environment for studying lottery-draw randomness, casino RNG behavior, physical-machine hypotheses and statistical anomalies. The project deliberately separates statistical analysis from gambling advice and does not promise winning predictions.

## Why this is a new project
The original project was justified by a concrete lottery-randomness artifact. The newly supplied casino report broadens the same research boundary into online-game RNG, provably-fair protocols, house-edge mathematics and backend integrity. This is an evolution of the audit domain, not a project for exploiting gamblers.

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
1. **Draw/Game Ingestor** — versioned results with provenance.
2. **Rules/RNG Schema Registry** — explicit rules, RNG declarations and protocol versions.
3. **Statistical Baseline** — exact combinatorial probabilities and null models.
4. **RNG Audit** — reproducible tests for distribution, independence and implementation consistency.
5. **Provably-Fair Verifier** — verification of declared server/client seed, hash and nonce protocols where applicable.
6. **House-Edge Analyzer** — mathematical expected-value analysis, not a promise of profitable play.
7. **Physical-System Model** — optional observations such as machine, ball-set or environmental parameters when legitimately available.
8. **Simulation Engine** — reproducible seeds, Monte Carlo and bootstrap/resampling.
9. **Agent Ensemble** — independent analysts with disagreement reporting rather than false consensus.
10. **Evaluation Harness** — rolling-origin and blind holdout tests.
11. **Audit UI** — transparent metrics, uncertainty and protocol evidence.

## Critical source correction
The supplied casino material contains sections proposing “Neuro-Casino” behavioral manipulation, biometric feedback and persuasive control. Those mechanisms are treated as **cognitive-security threat models**, not as project objectives. The audit system must never optimize gambling engagement, exploit vulnerability or manipulate users.

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
Extends Projects 51, 55, 61, 72 and related probability/simulation infrastructure while absorbing the casino RNG/provably-fair/house-edge audit material from Iteration 12.

## Definition of Done
- Historical datasets are provenance-linked.
- Null models are explicit and independently reproducible.
- RNG/protocol checks are reproducible.
- All stochastic experiments have recorded seeds/configuration.
- Anomaly findings survive holdout/replication tests before promotion.
- UI never disguises uncertainty as certainty.
- The system produces an auditable statistical report rather than a betting recommendation.
