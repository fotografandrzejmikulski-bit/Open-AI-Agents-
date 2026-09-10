# Knowledge Ingestion — Prompt Intelligence, Lotto Systems, PUI/3DGS, Tarot Taxonomy, Apeiron 78 and Consent/Privacy

## Source batch

1. `Promp3.pdf`
2. `Prompt Deepsearch 1.pdf`
3. `Prompt6.pdf`
4. `Promt 5.pdf`
5. `Promt4.pdf`
6. `Przegląd Systemów Gier Lotto(1).pdf`
7. `PUI Launcher z Godot i 3DGS (1).pdf`
8. `Rodzaje Kart Tarota_ Kompleksowy Przegląd(1).pdf`
9. `Rozbudowa Systemu Apeiron do 78 Kart(1).pdf`
10. `souhlas_marketing_sk.pdf`

## Executive synthesis

The batch contains four distinct engineering knowledge domains plus a repeated OSINT/personal-profiling prompt family:

- investigative/OSINT dossier prompts;
- mathematical and structural analysis of global lottery systems;
- Android PUI launcher architecture using Godot 4.x and 3D Gaussian Splatting;
- historical/structural taxonomy of Tarot systems;
- Apeiron 2.0 expansion from a limited deck to 78 cards with layered overlays and hexadecimal/checksum semantics;
- a concrete marketing-consent document exposing data categories, processors, purpose and retention as a privacy/governance pattern.

No genuinely new product/runtime is required by this batch. The dominant effect is **capability deepening of existing evidence, cognitive-safety, symbolic-artifact, probability and OmniCore/PUI lineages**.

## 1. Prompt corpus: deduplication and safe transformation

`Prompt6.pdf` and `Promt 5.pdf` are effectively duplicates: both request behavioral and predictive profiling, motives, communication style and scenario prediction. `Promt3.pdf` requests reconstruction of a person's digital footprint and ideological profile from public activity. `Prompt Deepsearch 1.pdf` requests a comprehensive dossier covering identity, career, business/political/organizational links, public assets, media/ideology and controversies. `Promt4.pdf` requests an influence/power map including people, companies, political/public roles, family links, criticism and business failures.

Repository decision: **do not create a new profiling/targeting project**. The capability already belongs to Projects 30/32/36/43/49/54/57. The new material is ingested as a defensive OSINT/evidence-design corpus.

Required architectural boundary:

```text
PUBLIC SOURCE
  -> OBSERVED CLAIM
  -> SOURCE / DATE / CONTEXT
  -> ENTITY-RESOLUTION HYPOTHESIS
  -> CORROBORATION / CONTRADICTION
  -> BOUNDED INFERENCE
  -> REPORT
```

A public source does not by itself prove identity, motive, ideology, family relation, conflict of interest, criminality or future behavior. Psychological diagnosis and personalized behavioral targeting are out of scope. Scenario analysis may be used for defensive risk assessment only and must be labeled as inference, not fact.

## 2. Global Lotto systems — mathematical knowledge

The Lotto report models a lottery as a parameter tuple `(m,n,p,q)` and uses combinations/hypergeometric reasoning for single-pool games. For 6/49 it states a jackpot probability of 1 in 13,983,816. Multi-matrix games multiply independent pool probabilities; examples include Powerball-style 5/69 + 1/26 structures. The report surveys North American, European, Asian/Pacific and South American formats, including annuity games, All-or-Nothing and Keno.

The report also analyzes full systems and reduced/wheeling systems. Full systems enumerate combinations; reduced systems are combinatorial designs that trade ticket count against explicit lower-tier guarantees. The report explicitly notes that betting systems do not change negative expected value in ordinary play; they redistribute variance, while rare jackpot overlays are a separate condition.

Engineering extraction for Project 78/51/55:

- canonical `GameMatrix(m,n,p,q)` schema;
- exact combinatorial baseline;
- multi-pool probability model;
- paytable and expected-value model;
- wheeling as combinatorial-design object rather than predictive magic;
- Keno variable-`p` model;
- All-or-Nothing symmetry test;
- regional rules/version registry;
- simulation with declared seed and out-of-sample evaluation;
- anomaly != exploitable bias.

The report's current game figures are treated as **source snapshots**, not timeless live rules. Current rules and prices require primary-source verification before operational use.

## 3. PUI Launcher — Android + Godot + 3DGS

The PUI report proposes a system launcher for Android using Godot 4.x and 3D Gaussian Splatting. The intended research loop is:

```text
USER EXPRESSION
 -> SENSOR / TOUCH OBSERVATION
 -> CONTEXT + SENSOR FUSION
 -> STATE ESTIMATE
 -> VISUAL ADAPTATION
 -> NEW OBSERVATION
```

Modalities include IMU/kinematics, touch behavior and application context. The report proposes ground-truth labeling and discusses Android HOME intent, package enumeration, dedicated Kotlin plugins, `QUERY_ALL_PACKAGES`, 3DGS memory bandwidth, SOGS/quantized representations, spherical-harmonic reduction and Compute Shaders.

A key engineering conclusion is that raw 3DGS is too heavy for always-on mobile operation without aggressive compression and lifecycle control. The proposed architecture therefore favors a hybrid Kotlin + Godot/GDScript/Compute Shader split and render freezing when the launcher is obscured.

Safety transformation: affective sensing/adaptation is restricted to transparent UX/accessibility/research contexts. No covert emotional exploitation, vulnerability targeting, hidden persuasion or permission changes based on affective signals.

## 4. Tarot taxonomy

The Tarot study establishes that “Tarot” is not one immutable schema. It describes historical and modern families with different card counts, court structures, iconography and correspondence systems. Examples include Visconti-Sforza, Sola Busca, Minchiate (97 cards), Tarocchino (62 cards), Marseille, Rider-Waite-Smith, Thoth, Osho Zen, Motherpeace, Transparent and other experimental forms.

The core engineering consequence is already represented in Project 53: a deck is a versioned `DeckSchema`, not a universal ontology. The taxonomy adds stronger support for:

- phylogenetic/deck-lineage metadata;
- structural comparison;
- card-count and court-schema variation;
- correspondence-system versioning;
- transparent, round, double-sided and multi-suit variants;
- explicit distinction between historical game use and later divinatory/occult interpretations.

The report's historical interpretations remain source-derived and should not be promoted to universal historical fact without independent scholarship.

## 5. Apeiron 2.0 — 78-card layered system

The Apeiron document expands a limited system to 78 cards and treats transparency/overlay as the core semantic mechanic. The supplied architecture maps four Minor Arcana domains to technological metaphors and defines court roles. It adds hexadecimal values at card corners, checksum-style overlay arithmetic, overflow/remainder semantics, ASCII/steganographic visual layers and a `Stack Trace` protocol for layered reading.

Repository transformation:

- keep the 78-card structure as a configurable artifact schema;
- keep HEX/checksum as deterministic game/symbolic mechanics;
- treat checksum/overflow as encoding, never as evidence of truth;
- preserve stack geometry, reveal states and protocol order as explicit rules;
- keep hidden messages/reveal layers user-observable and rule-defined;
- connect deck semantics to Project 53 and physical production to Project 71.

The mathematical mechanisms in the source are part of the designed symbolic system; they do not establish empirical predictive power.

## 6. Marketing consent / privacy governance

The Slovak consent document is a concrete example of a marketing-consent flow. It identifies categories including name, email, phone, address, image/identity-related recordings and purchase information, and describes marketing use, multiple processing parties and a stated retention period. It therefore contributes a useful **data-governance test fixture**, not a generic legal template.

Engineering extraction:

```yaml
ConsentRecord:
  purpose:
  data_categories: []
  controllers: []
  processors: []
  recipients:
  retention:
  voluntary:
  notice_version:
  consent_timestamp:
  withdrawal_path:
  scope:
```

The source document is a historical/example artifact. It must not be treated as current legal advice or as proof of present GDPR compliance. Any production system needs current jurisdiction-specific legal review.

## 7. Cross-portfolio impact

### Project 53 — Symbolic Interface & Artifact Compiler
Add Tarot lineage taxonomy, expanded `DeckSchema`, Apeiron 78-card semantics, HEX/checksum overlays and protocolized stack interpretation.

### Project 54 — Epistemic Signal & Adversarial Control Fabric
Add defensive handling of dossier/profiling prompts: source attribution, identity-resolution hypotheses, behavioral-signal limits, prediction uncertainty, consent/disclosure and anti-targeting boundaries.

### Project 57 — Multimodal Intelligence & Cognitive Interface Fabric
Add PUI Android sensor-fusion architecture, public-profile evidence normalization, consent metadata and a dedicated PUI privacy/cognitive-sovereignty evaluation profile.

### Project 61 — OmniCore Convergence Fabric
Add concrete Android/Godot/3DGS launcher constraints, lifecycle/performance gates, sensor-fusion state separation and explicit PUI consent/disable/revert controls.

### Project 71 — Physical Artifact Manufacturing & Symbolic Interface Factory
Add Tarot structural variants and Apeiron 78-card/HEX/overlay production requirements while preserving batch QC and rule-defined reveal states.

### Project 78 — Lottery & Casino Randomness Audit & Simulation Lab
Add `GameMatrix`, multi-pool probability, wheeling/combinatorial-design representation, paytable/EV analysis and explicit separation between variance redistribution and prediction.

## 8. New-project decision

**No new canonical project.**

Reasons:

- profiling prompts duplicate existing OSINT/evidence and influence-security infrastructure;
- Lotto material extends Project 78 rather than creating a separate prediction product;
- PUI/3DGS is already a first-class lineage in Projects 61/57/04/09;
- Tarot/Apeiron belongs to Projects 53/71/50/01;
- consent/privacy is a cross-cutting governance capability, not a standalone product in this batch.

## 9. Epistemic and safety boundaries

- OSINT identity/motive/relationship claims remain source-attributed and confidence-bounded.
- No psychological diagnosis or covert behavioral targeting is created from the profiling prompts.
- No gambling system is presented as a guaranteed winning strategy.
- Lottery anomalies require statistical characterization and replication.
- Symbolic/tarot interpretation is not empirical prediction or diagnosis.
- Affective sensing is transparent and agency-preserving.
- Personal-data processing requires explicit purpose, scope, retention and current legal review.
- Production claims about Android performance or 3DGS mobile viability require real-device benchmarks.
