# Project 62 — OmniCore Data, Causal & Distributed Intelligence Fabric MAX

## Status

Research/architecture specification derived from the newly supplied corpus. It extends Projects 29, 30, 41, 49, 54, 55, 56, 57, 58, 60 and 61.

## 1. Mission

Build a governed analytical intelligence fabric that combines data-warehouse semantics, distributed data processing, statistical learning, dimensionality reduction, probabilistic inference, causal reasoning, visualization and evidence-backed communication.

The system is designed to answer three different questions without conflating them:

```text
WHAT IS IN THE DATA?
        ↓
WHAT CAN WE PREDICT?
        ↓
WHAT WOULD CHANGE IF WE INTERVENED?
```

The model proposes analyses and hypotheses; typed contracts, evidence, causal assumptions, policy and authoritative state remain decisive.

## 2. Core architecture

```text
USER / OPERATOR
      ↓
QUESTION + DECISION CONTEXT
      ↓
DATA CONTRACT + ANALYTICAL GRAIN
      ↓
SOURCE / LINEAGE / FRESHNESS INVENTORY
      ↓
WAREHOUSE / DATA MART / DISTRIBUTED COMPUTE
      ↓
QUALITY + SCHEMA + TYPE CHECKS
      ↓
TASK ROUTER
 ┌────┼───────────┐
 ↓    ↓           ↓
EDA  PREDICTIVE  CAUSAL
 ↓    ↓           ↓
PCA  REG/NN      SCM / GRAPH / INTERVENTION
GMM  CLASSIFY    COUNTERFACTUAL
 └────┼───────────┘
      ↓
UNCERTAINTY + GENERALIZATION + IDENTIFIABILITY
      ↓
VISUALIZATION / COMMUNICATION PROJECTION
      ↓
HUMAN DECISION BOUNDARY
      ↓
AUTHORIZED ACTION
      ↓
AUTHORITATIVE READBACK
      ↓
OUTCOME / DRIFT / CAUSAL RETROSPECTIVE
      ↺
MODEL + DATA + POLICY UPDATE
```

## 3. Analytical grain contract

Every fact-bearing analytical object declares:

```text
DatasetId
Grain
EntityKey
TimeKey
MeasureDefinitions
AggregationRules
NullPolicy
DuplicatePolicy
UnitSemantics
SourceRefs
Freshness
```

This prevents errors such as interpreting row counts as physical units. The Tableau case material explicitly demonstrates the problem: each row can represent a unique title, making `Number of Records` a count of unique titles rather than total units sold. fileciteturn249file0L27-L31

## 4. Warehouse / OLTP boundary

OLTP and OLAP are modeled as different workload classes. OLTP emphasizes short, isolated and detailed current transactions; OLAP performs broad and often unpredictable historical analysis. The supplied warehouse material argues that heavy analytical workloads should be separated from transaction processing. fileciteturn253file0L7-L29

Project 62 therefore enforces:

```text
transactional authority ≠ analytical read model
```

Analytical transformations may not silently become transactional writes.

## 5. Dimensional warehouse model

The warehouse fabric supports star-schema patterns with a fact table and dimension tables, plus explicit design of process, grain, dimensions and measures. fileciteturn253file1L34-L45 fileciteturn246file0L121-L137

A semantic layer normalizes business definitions before models consume the data.

## 6. ETL / data lineage

ETL is treated as a declarative transformation graph where feasible. The supplied warehouse material describes Extract, Transform and Load, including rule-driven extraction approaches. fileciteturn254file0L6-L14

Each transformed field stores:

```text
source field → transformation → output field → validation → consumer refs
```

Lineage loss is a release blocker for decision-critical datasets.

## 7. KDD lifecycle

The project adopts Knowledge Discovery as a full lifecycle of access, exploration, preparation, modeling, deployment and monitoring. The supplied course describes KDD as seeking valid, useful and understandable patterns and distinguishes predictive from descriptive tasks. fileciteturn254file2L79-L85 fileciteturn254file2L108-L116

Unknown or unsupported pattern claims are stored as hypotheses rather than promoted to facts.

## 8. Spark execution plane

Spark is integrated as a distributed compute substrate for iterative, SQL, streaming and ML workloads. The supplied material describes RDD transformations/actions, external storage integration, schema-aware DataFrames and Catalyst query optimization. fileciteturn246file4L3-L26 fileciteturn246file4L47-L60 fileciteturn250file2L11-L22 fileciteturn250file3L113-L124

Spark execution manifests therefore include:

```text
inputRefs
schema
partitionPlan
transformations
resourceBudget
optimizerHints
outputContract
executionMetrics
```

Execution metrics are evidence about the run, not proof that the business result is correct.

## 9. Representation and dimensionality reduction

PCA is treated as an unsupervised representation-compression layer that exploits correlation and redundancy to construct a lower-dimensional representation. The supplied material connects PCA with projection, eigenvalues and constrained optimization. fileciteturn246file5L17-L48

Each PCA artifact declares:

```text
center/scale policy
basis matrix
retained components
explained variance
reconstruction error
fit population
projection version
```

A downstream consumer must know whether it is operating on raw features or a projected representation.

## 10. Matrix-factorization services

The fabric exposes numerical primitives such as Cholesky, eigendecomposition and SVD as explicitly typed services. Cholesky is preferred for suitable symmetric positive-definite systems where its computational and numerical properties are advantageous; SVD supports rectangular matrices and low-rank approximation. fileciteturn238file4L250-L314 fileciteturn238file6L418-L464

No inverse-by-default rule is used when a stable factorization or solve is more appropriate.

## 11. Probabilistic state and density estimation

Probability is represented explicitly for uncertainty in data, models and predictions. fileciteturn234file5L5-L28

Gaussian mixture models provide compact multimodal density representations, while EM alternates responsibility estimation and parameter updates in latent-variable inference. fileciteturn246file8L43-L68 fileciteturn251file0L48-L73

Soft responsibilities are preserved in evidence state; ambiguous observations are not forced into a single class when the model itself indicates uncertainty. fileciteturn251file1L131-L158

## 12. Causal inference plane

Project 62 adds a distinct causal layer. The supplied causal-inference material states that causal structure contains information beyond observational probability and supports intervention and counterfactual reasoning. fileciteturn252file3L297-L321

Structural causal models are represented as mechanisms/assignments and can differ even when they induce the same observable distribution. fileciteturn252file1L78-L99

Supported causal operations include:

```text
SCM construction
DAG / graph reasoning
identifiability assessment
covariate adjustment
do-calculus
intervention distributions
counterfactual analysis
potential outcomes
causal time-series analysis
```

The system explicitly records assumptions required for each causal claim.

## 13. Independent mechanisms and invariance

The independent-mechanisms principle is represented as a structural hypothesis that causal mechanisms are autonomous modules. fileciteturn252file4L348-L397

When the observed distribution changes, Project 62 asks whether the change is better explained by:

```text
sampling variation
covariate shift
measurement change
policy/intervention
mechanism change
population change
```

A generic drift score is insufficient when the underlying mechanism changed.

## 14. Predictive vs causal routing

The task router must distinguish:

```text
DESCRIPTIVE:
  summarize, cluster, associate, visualize, reduce

PREDICTIVE:
  estimate target on unseen cases

CAUSAL:
  estimate effects under specified interventions or counterfactuals
```

Predictive performance is not causal evidence. A model may predict well while remaining unable to answer an intervention question, as emphasized by the causal source. fileciteturn252file3L105-L121

## 15. Validation hierarchy

Project 62 uses escalating evaluation:

```text
schema validation
      ↓
data quality / leakage checks
      ↓
train / validation / test separation
      ↓
cross-validation / nested CV where relevant
      ↓
uncertainty analysis
      ↓
robustness / shift tests
      ↓
causal identifiability / intervention evidence
      ↓
real-world outcome verification
```

The supplied ML material describes nested cross-validation as separating model/hyperparameter selection from estimation of generalization performance. fileciteturn237file0L31-L73

Regularization is treated as a mechanism for controlling excess model flexibility and improving generalization rather than as a universal cure. fileciteturn237file2L147-L178

## 16. Visualization integrity layer

Visualization is compiled from validated semantic measures rather than directly from arbitrary fields.

A `VisualizationSpec` contains:

```text
purpose
question
grain
measure
aggregation
filter
encoding
scale
uncertaintyDisplay
annotation
accessibility
sourceRefs
```

The Tableau workshops provide concrete examples of choosing timelines, bars, treemaps, pies, moving averages, dynamic sets and data blending. fileciteturn249file0L20-L37 fileciteturn249file2L95-L105

The system treats chart type as a communication choice, not evidence that the underlying metric is correct.

## 17. Decision-story compiler

The communication material is adapted into a non-manipulative presentation compiler:

```text
verified evidence
      ↓
key finding set
      ↓
uncertainty + caveats
      ↓
ordered narrative
      ↓
audience-specific projection
      ↓
review / approval
```

The supplied communication material recommends a small number of key messages and placing the main message early. fileciteturn253file3L54-L62

For high-impact communication, the system retains source references and caveats so concise presentation does not erase epistemic limitations.

## 18. Security and governance

The analytical fabric inherits OmniCore control-plane protections:

- semantic retrieval never grants access;
- model output never grants authorization;
- analytical datasets require provenance and freshness metadata;
- external sources remain untrusted evidence;
- high-impact decisions require explicit policy and human review;
- causal assumptions are explicit rather than hidden in prompts;
- visualization and communication cannot change truth status of claims;
- behavioral targeting is not an optimization objective.

## 19. Object model

```text
DataSource
 ├─ sourceRef
 ├─ accessScope
 └─ freshness

Dataset
 ├─ schema
 ├─ grain
 ├─ lineage
 ├─ qualityReport
 └─ distributionProfile

Representation
 ├─ transform
 ├─ parameters
 ├─ informationRetained
 └─ validation

StatisticalModel
 ├─ objective
 ├─ inputs
 ├─ outputs
 ├─ assumptions
 ├─ uncertainty
 └─ generalization

CausalModel
 ├─ graph
 ├─ mechanisms
 ├─ assumptions
 ├─ identifiability
 ├─ interventions
 └─ counterfactuals

Visualization
 ├─ semanticRefs
 ├─ encoding
 ├─ aggregation
 ├─ accessibility
 └─ evidenceRefs

Decision
 ├─ evidenceRefs
 ├─ modelRefs
 ├─ causalRefs
 ├─ policyRef
 ├─ authorizationRef
 └─ outcomeRef
```

## 20. Evaluation matrix

| Layer | Evidence gate | Failure action |
|---|---|---|
| Warehouse grain | explicit grain + measures | reject query |
| ETL | lineage + reconciliation | quarantine dataset |
| Distributed execution | schema + run manifest + metrics | block downstream use |
| Representation | transform + information-loss report | reject/flag |
| Predictive ML | generalization evidence | block promotion |
| Density estimation | convergence + stability | quarantine model |
| Causal model | identifiability + assumptions | label non-identifiable |
| Visualization | semantic consistency | reject chart |
| Communication | claim/evidence alignment | reject publication |
| Consequential decision | policy + authorization + readback | block/reconcile |

## 21. Hard runtime invariants

1. Analytical grain is explicit.
2. OLTP state is not replaced by an analytical projection.
3. Every transformation preserves lineage.
4. Distributed execution is reproducible or its non-determinism is documented.
5. Similarity, clustering and topics are not identity or intent proofs.
6. Compression and dimensionality reduction expose information-loss metrics.
7. Numerical algorithms declare their domain and stability requirements.
8. Uncertainty is retained when material to the decision.
9. Soft assignments are not silently converted to hard labels.
10. Predictive correlation is not causal effect.
11. Causal claims expose assumptions and identifiability status.
12. Distribution shift and mechanism change are distinct states.
13. Visualization cannot repair invalid semantics.
14. Concise communication cannot erase caveats needed for a correct interpretation.
15. Model output does not authorize side effects.
16. High-impact outcomes require authoritative readback.
17. Unknown and non-identifiable states never pass silently.
18. Monitorability degradation increases verification rather than reducing it.
