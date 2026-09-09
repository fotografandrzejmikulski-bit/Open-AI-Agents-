# Lottery Randomness Audit and Simulation — 2026-09-09

## Source
Nowy system Lotto.

## Source-derived architecture
The document presents an “Integrated Meta-Deterministic Protocol (IMDP)” intended to model lottery draws as physical and algorithmic systems rather than pure luck. Its early pages propose CDM/Dirichlet analysis, a “Strong Law” hypothesis, chaos analysis of physical machines and a multi-agent decision layer. fileciteturn212file0L13-L20

The supplied HTML prototype supports several game configurations and implements a visible protocol flow. Pages 20–22 show the UI/game selector; later pages show protocol phases, Monte Carlo-style simulation and number generation heuristics. fileciteturn212file1L43-L45 fileciteturn212file2L59-L67

## Integrity assessment
The document also contains claims of very high certainty and code that uses ordinary `Math.random()` plus heuristic preferences. Those implementation details do **not** establish predictive power. The displayed “probability” is generated from the program's own heuristic calculation, not validated out-of-sample forecasting. fileciteturn212file3L82-L88

## Safe reusable capability
The useful engineering product is therefore a **Lottery Randomness Audit & Simulation Lab**:
- ingest historical draws;
- characterize distributions and dependencies;
- test independence and stationarity assumptions;
- simulate null models;
- detect anomalies in supplied datasets;
- compare physical-machine hypotheses against observations;
- run blinded/out-of-sample evaluation;
- report uncertainty and calibration.

It must not claim guaranteed winning combinations or present gambling predictions as reliable. The source's own Android deployment is simply a PWA-style HTML packaging route, not evidence of model validity. fileciteturn212file3L89-L91

## Portfolio impact
The stochastic methods overlap Projects 51, 55 and 61, but the combination of lottery-domain audit, physical-draw modeling and a runnable research artifact is sufficiently self-contained to justify Project 78 as a bounded research/simulation product.
