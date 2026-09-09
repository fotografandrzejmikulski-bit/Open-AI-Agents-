# Project 63 — OmniCore Decision Intelligence, Causal Classification & Communication Fabric MAX

## 1. Mission

Build a governed decision-intelligence layer that connects structured data, distributed computation, machine-learning classification, unsupervised structure discovery, causal-text extraction, visualization and evidence-preserving communication without collapsing probabilistic evidence into authorization or factual truth.

The system is designed as a bridge between Projects 61–62 and the higher-level research, evidence and commercialization layers of OmniCore.

## 2. Core problem

A modern analytical system can fail even when individual components work correctly:

- a clean classifier can be trained on contaminated data;
- a good cluster can be given an unjustified semantic meaning;
- a linguistic causal relation can be mistaken for a validated causal mechanism;
- a dashboard can hide aggregation errors or missingness;
- a concise executive statement can omit a material qualifier;
- a commercial idea can be mistaken for market evidence;
- a model score can be silently converted into an adverse action.

Project 63 makes these transitions explicit and verifiable.

## 3. System boundary

```text
DATA SOURCES
   ↓
DATA CONTRACT / LINEAGE / QUALITY
   ↓
ETL / WAREHOUSE / DISTRIBUTED COMPUTE
   ↓
REPRESENTATION + FEATURE PIPELINE
   ↓
ANALYTICAL ENGINES
   ├── Classification / SVM
   ├── Regression / prediction
   ├── Clustering / latent structure
   ├── Density / probabilistic models
   ├── Causal-text extraction
   └── Exploratory analysis
   ↓
EVALUATION / UNCERTAINTY / DRIFT
   ↓
EVIDENCE GRAPH
   ↓
VISUALIZATION / EXPLANATION
   ↓
COMMUNICATION COMPILER
   ↓
DECISION SUPPORT
   ↓
POLICY / AUTHORIZATION / HUMAN BOUNDARY
   ↓
EXECUTION WHERE AUTHORIZED
   ↓
AUTHORITATIVE READBACK
   ↓
AUDIT / MONITOR / ADAPT
```

## 4. Typed analytical state

Every analytical object receives a typed record:

```text
AnalyticalArtifact {
  artifact_id
  source_refs[]
  dataset_version
  schema_version
  grain
  time_window
  transformations[]
  assumptions[]
  method
  parameters
  uncertainty
  evaluation
  causal_status
  policy_status
  provenance
  freshness
  created_at
  supersedes
}
```

No downstream stage may silently erase `grain`, `assumptions`, `uncertainty`, `provenance` or `causal_status`.

## 5. Classification engine

Project 63 supports binary and multiclass classification pipelines, with SVM as one explicit implementation family.

### SVM contract

```text
FeatureVector → ClassifierModel → Score → Calibration → Threshold Policy → Decision Candidate
```

The classifier layer records:

- feature space and preprocessing;
- model family;
- hard/soft-margin configuration where applicable;
- support-vector diagnostics;
- kernel configuration where applicable;
- hyperparameter provenance;
- training/test split provenance;
- class balance;
- threshold-selection method;
- confusion matrix;
- calibration and uncertainty.

Kernelized models are treated as a representation/classifier composition rather than an opaque monolith, preserving the modularity described in the supplied SVM material.

## 6. Unsupervised structure engine

Clustering is used to discover structure, not to assign unquestionable semantics.

```text
DATA
 ↓
STANDARDIZATION / REPRESENTATION
 ↓
CLUSTER SEARCH
 ↓
STRUCTURE QUALITY
 ↓
STABILITY / SENSITIVITY
 ↓
OVERLAP / MEMBERSHIP UNCERTAINTY
 ↓
HUMAN INTERPRETATION
```

Possible outputs include hard cluster IDs, soft membership vectors, overlapping memberships and dendrogram-like structures. Cluster labels remain analytical hypotheses until independently validated.

## 7. Causal-text intelligence

The causal extraction subsystem converts unstructured text into candidate causal relations:

```text
DOCUMENT
 ↓
SEGMENTATION / PARSING
 ↓
CAUSAL-NONCAUSAL FILTER
 ↓
CAUSE / VERB / EFFECT / POLARITY
 ↓
NEGATION / MODALITY / TEMPORAL SCOPE
 ↓
TUPLE SCORE
 ↓
CAUSAL EVIDENCE EDGE
```

Each candidate edge carries:

```text
CausalEvidenceEdge {
  cause
  mechanism_phrase
  effect
  polarity
  scope
  source
  passage
  extraction_method
  confidence
  causal_status
}
```

Allowed causal statuses:

`ASSERTED | EXTRACTED | HYPOTHESIS | INTERVENTIONALLY_SUPPORTED | FALSIFIED | UNKNOWN`

Extraction from language never upgrades an edge directly to `INTERVENTIONALLY_SUPPORTED`.

## 8. Causal validation bridge

Project 63 links linguistic evidence with the structural-causal layer from Project 62 and related causal-inference research.

```text
OBSERVATIONAL TEXT
        ↓
LINGUISTIC CAUSAL HYPOTHESIS
        ↓
OBSERVATIONAL DATA CHECK
        ↓
CONFOUNDER ANALYSIS
        ↓
CAUSAL GRAPH HYPOTHESIS
        ↓
INTERVENTION / QUASI-EXPERIMENT / NATURAL EXPERIMENT
        ↓
COUNTERFACTUAL TEST WHERE JUSTIFIED
        ↓
CAUSAL STATUS UPDATE
```

Correlation, predictive usefulness and linguistic assertion remain separate from interventional effect.

## 9. Data-platform integration

Project 63 treats the data warehouse as an analytical boundary rather than a generic database replica.

### Required metadata

- source system;
- extraction timestamp;
- data version;
- business/analytical grain;
- dimensional keys;
- aggregation semantics;
- transformation history;
- retention/deletion status;
- data quality findings;
- freshness.

Star-schema and dimensional-model patterns are supported as implementation strategies; they are not treated as mandatory for every workload.

## 10. Distributed execution

Apache Spark/PySpark and similar engines can execute scale-heavy transformations, SQL, feature generation and model preparation.

Project 63 preserves a strict separation:

```text
DISTRIBUTED DATA PLANE ≠ POLICY PLANE
MODEL COMPUTE ≠ AUTHORIZATION
QUERY OPTIMIZATION ≠ TRUST
```

Schema-aware DataFrame/Spark SQL workloads may be preferred when structured transformations and optimizer support provide material benefits; low-level distributed primitives remain available where they are genuinely useful.

## 11. Visualization compiler

Visualization is compiled from typed analytical state rather than hand-authored as an uncontrolled presentation layer.

```text
MetricSpec
DimensionSpec
TimeSpec
FilterSpec
UncertaintySpec
MissingnessSpec
DisplayGoal
        ↓
VISUALIZATION PLAN
        ↓
CHART / TABLE / MAP / NETWORK
        ↓
SEMANTIC VALIDATOR
```

The validator checks:

- numerator/denominator correctness;
- aggregation grain;
- unique-count vs row-count semantics;
- filter and exclusion visibility;
- missing periods;
- scale and axis integrity;
- derived calculations;
- color/label semantic conflicts;
- source lineage.

Dashboard interactions are treated as state transitions, not just UI decoration.

## 12. Visualization patterns retained from the supplied case material

The system supports patterns demonstrated in the supplied exercises, including:

- timelines for temporal change;
- bar charts for categorical comparison;
- treemaps for hierarchical composition;
- parameterized Top-N sets;
- moving averages;
- dashboard filter actions;
- Level-of-Detail calculations;
- dual-axis views;
- animation through time where analytically justified;
- area charts for exposing temporal gaps;
- Likert-scale-oriented survey views.

These are implementation patterns, not universal rules. The visualization compiler selects a chart based on the analytical question and data semantics.

## 13. Communication compiler

The communication subsystem converts verified analytical state into audience-specific summaries without removing epistemic qualifiers.

```text
EVIDENCE
 ↓
CLAIM GRAPH
 ↓
AUDIENCE MODEL
 ↓
MESSAGE PRIORITIZATION
 ↓
COMPRESSION
 ↓
SOURCE / UNCERTAINTY PRESERVATION
 ↓
FINAL COMMUNICATION ARTIFACT
```

A message may be shortened, but the compiler must preserve material distinctions such as:

- observation vs inference;
- correlation vs causation;
- model prediction vs verified fact;
- historical result vs forecast;
- estimate vs measured quantity;
- hypothesis vs established finding.

## 14. Language robustness layer

The supplied colloquial Polish lexicon is incorporated only as a language-processing robustness resource.

Capabilities:

- register detection;
- slang normalization;
- offensive-language detection;
- lexical-variation handling;
- sentiment/polarity context support;
- adversarial spelling-variant detection.

The lexicon never independently determines a person’s intent, character or factual state.

## 15. Opportunity discovery layer

The supplied AI-monetization corpus becomes a candidate-opportunity generator rather than a truth source.

```text
IDEA CORPUS
   ↓
PROBLEM NORMALIZATION
   ↓
ICP / BUYER / USER IDENTIFICATION
   ↓
DATA + CAPABILITY FEASIBILITY
   ↓
UNIT ECONOMICS HYPOTHESIS
   ↓
COMPETITION / DEFENSIBILITY
   ↓
REGULATORY / SAFETY RISK
   ↓
EVIDENCE OF DEMAND
   ↓
EXPERIMENT
   ↓
MEASURED OUTCOME
```

Opportunity scoring must distinguish:

`idea attractiveness ≠ market demand ≠ product-market fit ≠ realized revenue`.

## 16. High-impact domain safeguards

The supplied case corpus contains crime-prediction and election-result exercises. Project 63 treats these strictly as model-evaluation material.

Forbidden architecture:

```text
MODEL SCORE → AUTOMATED POLICING / POLITICAL TARGETING / ADVERSE ACTION
```

Required architecture:

```text
MODEL SCORE
 ↓
UNCERTAINTY + CALIBRATION
 ↓
FAIRNESS / ERROR ANALYSIS
 ↓
HUMAN REVIEW
 ↓
EXPLICIT POLICY
 ↓
AUTHORIZED ACTION
 ↓
APPEAL / CORRECTION
```

Political inference must not become covert persuasion or voter manipulation. Crime-related models must not be treated as proof of individual criminality.

## 17. Evaluation framework

### Model level

- train/test integrity;
- cross-validation where appropriate;
- sensitivity/specificity;
- ROC/AUC where meaningful;
- threshold robustness;
- calibration;
- confusion-matrix analysis;
- outlier sensitivity;
- drift;
- subgroup error analysis where justified.

### Causal level

- causal-status completeness;
- confounder register;
- intervention support;
- alternative explanations;
- reproducibility;
- counterfactual consistency where identifiable.

### Visualization level

- metric semantic correctness;
- aggregation correctness;
- hidden-filter detection;
- missingness visibility;
- interaction-state correctness.

### Communication level

- claim traceability;
- qualifier retention;
- unsupported causal language detection;
- source-reference preservation;
- compression loss audit.

### Commercial level

- evidence of demand;
- willingness-to-pay evidence;
- acquisition economics;
- retention/realized value;
- operational cost;
- compliance and safety risk.

## 18. Multi-model disagreement

When multiple analytical methods disagree, the system preserves the disagreement.

```text
SVM ─────┐
Cluster ─┤
GMM ─────┼──→ COMPARISON MATRIX → DISAGREEMENT ANALYSIS → ESCALATION
Causal ──┤
Rules ───┘
```

Agreement is not proof when models share training data, feature engineering or assumptions. The evidence graph stores correlation between methods and shared failure modes.

## 19. Monitorability-aware integration

Project 63 inherits the monitorability doctrine of Project 58:

- reasoning traces are evidence, not authority;
- reduced CoT monitorability never lowers mandatory controls;
- action-level and authoritative-state verification remain independent;
- uncertainty and disagreement are preserved;
- consequential actions require stronger external verification as observability decreases.

A model that outputs an apparently plausible analytical narrative without exposing useful reasoning must still be checked against data, calculations, source lineage and authoritative state.

## 20. Security boundary

```text
MODEL OUTPUT
   ↓
UNTRUSTED ANALYTICAL PROPOSAL
   ↓
SCHEMA VALIDATION
   ↓
EVIDENCE / PROVENANCE CHECK
   ↓
POLICY CHECK
   ↓
HUMAN REVIEW WHERE REQUIRED
   ↓
CAPABILITY BROKER
   ↓
EXECUTION
```

Neither a classification score, cluster assignment, causal phrase, chart, executive summary nor generated business idea can grant authority by itself.

## 21. Implementation phases

### Phase 1 — Analytical contracts

Define schemas for datasets, metrics, features, model artifacts, causal edges, visual specs and communication claims.

### Phase 2 — Compute adapters

Implement provider-neutral adapters for warehouse SQL, Python/R analytics and Spark/PySpark execution.

### Phase 3 — Learning engines

Add classification, clustering, density-estimation and evaluation modules with deterministic replay where feasible.

### Phase 4 — Causal evidence

Add causal-text extraction, provenance, causal-status lifecycle and validation bridges to structural causal models.

### Phase 5 — Visualization compiler

Compile analytical specifications into validated dashboards, reports and interactive views.

### Phase 6 — Communication compiler

Generate executive, technical and public-facing summaries with source and qualifier retention.

### Phase 7 — Decision boundary

Add policy evaluation, human-review queues, authorization and authoritative postcondition verification.

### Phase 8 — Opportunity engine

Rank commercial ideas using evidence-backed experimentation instead of idea counts.

## 22. Success criteria

Project 63 is successful only when an analytical conclusion can answer:

1. What data produced it?
2. At what grain?
3. Which transformations were applied?
4. Which model or method generated it?
5. How was it evaluated?
6. What uncertainty remains?
7. Is the statement predictive, descriptive or causal?
8. What evidence supports the causal interpretation?
9. How was the visualization constructed?
10. Which qualifiers survive the final communication?
11. Who or what is authorized to act on it?
12. Can the complete result be reproduced and audited?

## 23. Relationship to the portfolio

```text
Project 61
Probabilistic Learning / Optimization
        ↓
Project 62
Data / Causal Analytics / Distributed Compute
        ↓
Project 63
Decision Intelligence / Classification / Causal Text / Visualization / Communication
        ↓
Projects 34, 45, 48, 49
Business / Evidence / Cognitive Sovereignty
        ↓
Projects 54–58
Epistemic Control / Stochastic Integrity / Multimodal Evidence / Monitorability
```

Project 63 is therefore a **decision-intelligence integration layer**, not a replacement for the underlying data, model, causal, security or governance subsystems.

## 24. Hard invariants

1. A model score never becomes authorization by implication.
2. Cluster membership never becomes factual identity without independent evidence.
3. Linguistic causal extraction never equals validated intervention effect.
4. Predictive accuracy never establishes causality.
5. A visualization never changes the underlying analytical grain.
6. Row counts and unique-entity counts are distinct metrics unless explicitly defined otherwise.
7. Missing data remains visible or is explicitly documented as suppressed.
8. Training/test separation and leakage controls are mandatory for model evaluation.
9. Threshold selection must be tied to the task's error/cost semantics.
10. Model disagreement is retained rather than silently averaged away.
11. Causal edges retain source passage and extraction provenance.
12. Communication compression cannot remove material uncertainty or causal qualifiers.
13. Commercial idea lists are candidate generators, not evidence of demand.
14. High-impact-domain models require explicit policy and human-review boundaries.
15. Sensitive behavioral or political inference cannot become covert targeting.
16. Dynamic visualization interactions cannot silently mutate authoritative policy state.
17. Analytical copies are not authoritative operational state.
18. Distributed compute does not bypass governance or authorization.
19. Reduced model monitorability increases, never decreases, external verification.
20. Shutdown, revocation and audit remain effective without model cooperation.
