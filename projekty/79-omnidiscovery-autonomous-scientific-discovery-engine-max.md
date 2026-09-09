# Project 79 — OmniDiscovery Autonomous Scientific Discovery Engine MAX

## Status
PROPOSED → ARCHITECTURE BASELINE → PROJECT GENESIS 2026-09-09

## Mission

Build a governed **closed-loop scientific discovery engine** that does not merely answer research questions, summarize literature or generate hypotheses, but systematically converts unknowns into experimentally discriminating programs and then learns from the resulting evidence.

The intended breakthrough is architectural:

> **Move from AI that produces research outputs to an AI system that manages the complete epistemic loop: unknown → hypothesis → model → discriminating experiment → observation → causal update → formalization → replication → knowledge.**

This project does **not** claim that the system will automatically solve open scientific problems. "World-changing" is the target scale of the research program, not an assertion of an achieved discovery.

## Why this is a new project

The portfolio already contains powerful pieces:

- Project 19 — research orchestration and evidence graphs;
- Project 48 — Grand Challenge / all-source intelligence and unknowns mapping;
- Project 61 — probabilistic learning, optimization and data intelligence;
- Project 62 — causal/data/distributed intelligence;
- Project 72 — cross-framework assurance and runtime verification;
- Project 77 — formalization and falsification of proposed mathematics;
- Projects 58/60 — monitorability and adversarial resilience;
- Projects 65/68 — AI-native runtime, Omnis, AI Foundry and constitutional execution;
- Projects 50/70/78 — stochastic and physical integrity;
- Projects 71/74/76 — physical, device and interactive experimental substrates.

None of these alone owns the **closed-loop discovery controller** whose primary output is not an answer, model or application, but a sequence of increasingly informative experiments selected to distinguish competing explanations.

Project 19 is a research orchestrator. Project 48 is a grand-challenge/evidence foundry. Project 61 is a learning/optimization foundry. Project 72 is an assurance fabric. Project 77 is a mathematical formalization laboratory.

Project 79 sits above and between them as a **discovery compiler and experiment-selection operating layer**.

## Core hypothesis

Scientific progress can be accelerated when the system optimizes not merely for prediction accuracy or answer quality, but for **expected information gained per unit of experimental cost, risk and ambiguity**.

The central research object becomes:

```text
COMPETING HYPOTHESES
        ↓
PREDICTION DIFFERENCES
        ↓
CANDIDATE OBSERVATIONS / INTERVENTIONS
        ↓
EXPECTED INFORMATION GAIN
        ↓
COST / RISK / FEASIBILITY
        ↓
DISCRIMINATING EXPERIMENT
        ↓
OBSERVATION
        ↓
BAYES / CAUSAL / FORMAL UPDATE
        ↓
REPLICATION
```

The exact objective function must be empirically evaluated; it is not assumed that information gain alone is the correct scientific utility function.

## 1. The Discovery Loop

```text
                 ┌──────────────────────────────┐
                 │        KNOWLEDGE UNIVERSE    │
                 │ literature / data / models  │
                 │ experiments / observations  │
                 └──────────────┬───────────────┘
                                ↓
                         UNKNOWN DETECTOR
                                ↓
                       HYPOTHESIS GENERATOR
                                ↓
                     INDEPENDENT SOLVERS
                                ↓
                    CONTRADICTION ENGINE
                                ↓
                      FORMAL MODEL BUILDER
                                ↓
                  PREDICTION DIFFERENTIATOR
                                ↓
                  EXPERIMENT DESIGN COMPILER
                                ↓
                 ┌──────────────┴──────────────┐
                 ↓                             ↓
           DIGITAL TEST                 PHYSICAL TEST
          simulation / proof             instrument / HIL
                 ↓                             ↓
                 └──────────────┬──────────────┘
                                ↓
                      AUTHORITATIVE OBSERVATION
                                ↓
                    CAUSAL / PROBABILISTIC UPDATE
                                ↓
                       INDEPENDENT REPLICATION
                                ↓
                        KNOWLEDGE PROMOTION
                                ↓
                   NEW UNKNOWN / NEW QUESTION
                                ↺
```

## 2. Discovery Object Model

Every scientific investigation becomes a versioned object.

```yaml
DiscoveryCase:
  discovery_id:
  question:
  domain:
  subdomains: []
  problem_lineage: []
  knowns: []
  unknowns: []
  assumptions: []
  hypotheses: []
  models: []
  observables: []
  interventions: []
  candidate_experiments: []
  evidence_refs: []
  counterevidence_refs: []
  causal_graph_ref:
  formal_model_refs: []
  simulation_refs: []
  physical_test_refs: []
  replication_refs: []
  uncertainty:
  resource_budget:
  risk_class:
  status:
```

The object is deliberately broader than a research report. It contains the state necessary to continue experimentation.

## 3. Epistemic Type System

The engine enforces a hard type system:

```text
SOURCE_ASSERTION
OBSERVATION
MEASUREMENT
DERIVED_RESULT
MODEL_ASSUMPTION
HYPOTHESIS
PREDICTION
SIMULATION_RESULT
CAUSAL_ESTIMATE
FORMAL_PROOF
REPLICATION_RESULT
ESTABLISHED_RESULT
```

Illegal implicit casts include:

```text
simulation → established result
LLM agreement → evidence
citation count → truth
correlation → causation
plausibility → proof
single experiment → universal law
absence of evidence → evidence of absence
```

This extends the repository's existing distinction between evidence, inference, hypothesis and verified fact. The scientific frontier corpus explicitly requires open problems, competing hypotheses, evidence, counterevidence, tests and status to remain separate. fileciteturn263file0L2-L6

## 4. Unknowns Graph

Project 48 already models unresolved problems as a cross-domain unknowns graph. Project 79 makes the graph operational.

```text
UNKNOWN
 ├─ depends_on → UNKNOWN
 ├─ constrained_by → OBSERVATION
 ├─ explained_by → HYPOTHESIS
 ├─ contradicted_by → EVIDENCE
 ├─ predicts → OBSERVABLE
 ├─ discriminated_by → EXPERIMENT
 └─ resolved_by → REPLICATED_RESULT
```

Every edge carries:

```yaml
Edge:
  relation:
  confidence:
  provenance:
  temporal_scope:
  source_scope:
  independence_class:
```

The graph becomes a machine-readable map of where additional information can actually change the state of knowledge.

## 5. Hypothesis Competition

The engine must resist single-hypothesis lock-in.

For every nontrivial problem:

```text
H1
H2
H3
...
Hn
```

are maintained simultaneously when supported by the evidence.

Each hypothesis contains:

```yaml
Hypothesis:
  id:
  statement:
  assumptions: []
  mechanism:
  predicted_observables: []
  forbidden_observables: []
  supporting_evidence: []
  contradicting_evidence: []
  alternative_explanations: []
  prior:
  posterior:
  falsification_conditions: []
  status:
```

The system is rewarded for identifying **decisive disagreement**, not for producing consensus.

## 6. Prediction-Difference Engine

The most important new component is the Prediction-Difference Engine.

Given competing models:

```text
M1 → P(y | x)
M2 → P(y | x)
M3 → P(y | x)
```

compute where their predictions materially diverge.

```text
MODEL SPACE
    ↓
PREDICTION SPACE
    ↓
DIVERGENCE MAP
    ↓
OBSERVABLES WITH HIGH DISCRIMINATIVE POWER
```

A beautiful experiment that all hypotheses predict equally well is low-value for discrimination.

A modest experiment on which hypotheses make sharply different predictions can be scientifically decisive.

Candidate metrics may include:

- predictive distribution divergence;
- expected information gain;
- expected reduction in posterior entropy;
- expected model discrimination;
- causal effect contrast;
- robustness across nuisance assumptions.

No metric is promoted as universally optimal before benchmark validation.

## 7. Experiment Design Compiler

The Experiment Design Compiler converts a research state into a typed experimental specification.

```text
DISCOVERY STATE
     ↓
HYPOTHESIS DIFFERENCES
     ↓
AVAILABLE OBSERVABLES
     ↓
CONSTRAINTS
     ↓
RESOURCE / TIME / SAFETY BUDGET
     ↓
CANDIDATE EXPERIMENTS
     ↓
EXPECTED INFORMATION / COST / RISK
     ↓
EXPERIMENT SPEC
```

```yaml
ExperimentSpec:
  experiment_id:
  objective:
  hypotheses_to_discriminate: []
  independent_variables: []
  dependent_variables: []
  controls: []
  confounders: []
  randomization:
  sample_plan:
  measurement_protocol:
  stopping_rule:
  expected_outcomes: []
  falsification_conditions: []
  safety_constraints: []
  resource_budget:
  preregistration_hash:
```

An experiment is not executed because an agent generated plausible instructions. It must pass policy, feasibility and safety validation first.

## 8. Digital Experimental Universe

The first execution layer is computational.

It integrates:

- symbolic algebra;
- numerical solvers;
- probabilistic simulation;
- optimization;
- Monte Carlo;
- causal models;
- agent/model ensembles;
- formal theorem provers;
- digital twins;
- synthetic environments.

The digital layer is explicitly classified as simulation.

```text
SIMULATION
≠
PHYSICAL OBSERVATION
```

Project 61 supplies the probabilistic/optimization substrate. Project 77 supplies formal mathematical verification. Project 78 supplies stochastic integrity and reproducibility.

## 9. Physical-in-the-Loop Discovery

Where a question cannot be resolved computationally, the system can compile a validated experiment for an authorized physical substrate.

Potential substrates include:

```text
SENSOR
LAB INSTRUMENT
ROBOTIC TEST RIG
ELECTRONICS SIMULATOR / HIL
VEHICLE DIAGNOSTIC DEVICE
EDGE DEVICE
MANUFACTURING TEST FIXTURE
```

The physical layer is always mediated through a capability broker.

```text
MODEL PROPOSAL
     ↓
EXPERIMENT SPEC
     ↓
SAFETY / AUTHORIZATION
     ↓
DEVICE CAPABILITY
     ↓
CONTROLLED EXECUTION
     ↓
SENSOR READBACK
     ↓
CALIBRATION / QC
     ↓
OBSERVATION
```

Projects 71 and 74 provide concrete physical/device patterns; Project 72 supplies the assurance boundary.

## 10. Causal Discovery Layer

Correlation is insufficient when the discovery depends on intervention.

```text
OBSERVATIONAL DATA
       ↓
ASSOCIATIONAL STRUCTURE
       ↓
CAUSAL HYPOTHESES
       ↓
IDENTIFIABILITY
       ↓
INTERVENTION DESIGN
       ↓
COUNTERFACTUAL PREDICTION
       ↓
OBSERVED EFFECT
```

The causal corpus explicitly distinguishes statistical association from structural causal models and notes that different causal structures can induce the same observational distribution. fileciteturn242file0L7-L12

Therefore the discovery engine must ask:

> **What observation would distinguish the competing mechanisms?**

not merely:

> **Which model predicts the existing data best?**

## 11. Formal Science Bridge

Project 77 becomes the formal mathematics backend.

For a mathematical discovery:

```text
CONJECTURE
 ↓
FORMAL DEFINITION
 ↓
DEPENDENCY GRAPH
 ↓
CONSISTENCY CHECK
 ↓
COUNTEREXAMPLE SEARCH
 ↓
LEMMA GENERATION
 ↓
FORMAL PROOF ATTEMPT
 ↓
MACHINE CHECK
 ↓
INDEPENDENT REPRODUCTION
```

For a physical theory:

```text
THEORY
 ↓
FORMAL MODEL
 ↓
DERIVED PREDICTION
 ↓
OBSERVABLE
 ↓
EXPERIMENT
 ↓
REPLICATION
```

A theorem prover cannot validate an incorrect translation of the physical problem. Conversely, a physical experiment cannot by itself establish a mathematical theorem. The bridges therefore retain separate evidence types.

## 12. Active Learning and Search

The engine treats discovery as sequential decision-making.

At time t:

```text
Knowledge_t
   ↓
Candidate experiments E₁...Eₙ
   ↓
Expected utility U(E)
   ↓
Select E*
   ↓
Observe O
   ↓
Knowledge_{t+1}
```

A general utility decomposition is:

```text
U(E) = information_value
       − experimental_cost
       − risk_penalty
       − ambiguity_penalty
       − irreversibility_penalty
```

The weights are project-specific and must be calibrated. In high-consequence domains, safety constraints dominate optimization.

## 13. Scientific Reproducibility Fabric

Every discovery step receives an immutable manifest.

```yaml
DiscoveryManifest:
  discovery_id:
  source_snapshot:
  code_snapshot:
  model_versions: []
  prompt_or_task_spec:
  dataset_hashes: []
  environment:
  hardware:
  random_seeds: []
  solver_versions: []
  experiment_spec_hash:
  raw_observation_refs: []
  transformed_data_refs: []
  analysis_refs: []
  reviewer_refs: []
  replication_refs: []
```

This extends the repository's existing experiment manifests, replay cases and provenance records.

## 14. Independent Replication Controller

The system cannot validate its own discovery through the same reasoning path that generated it.

```text
PRIMARY DISCOVERY AGENT
        ↓
CANDIDATE RESULT
        ↓
INDEPENDENT RECONSTRUCTION
        ↓
DIFFERENT MODEL / SOLVER / IMPLEMENTATION
        ↓
BLIND OR PARTIALLY BLIND TEST
        ↓
REPLICATION RESULT
```

Independence must be explicit. Ten agents sharing the same prompt, model family and evidence source are not ten independent confirmations.

## 15. Surprise Detector

A discovery candidate should be flagged when the observation is materially inconsistent with the currently accepted model family.

```text
PREDICTIVE DISTRIBUTION
        ↓
OBSERVATION
        ↓
SURPRISE / RESIDUAL
        ↓
Nuisance / measurement check
        ↓
REPLICATION
        ↓
MODEL REVISION OR DATA ERROR
```

A surprising result is a lead, not automatically a new law.

The detector must explicitly test mundane explanations:

- measurement error;
- calibration drift;
- data leakage;
- selection bias;
- software defects;
- numerical instability;
- hidden confounding;
- multiple-testing artifacts;
- source contamination.

## 16. Cross-Domain Isomorphism Engine

The repository contains recurring structural analogies across domains: stability landscapes in MHD, molecular conformational modeling and non-convex optimization; graph structures across OSINT, software and causal reasoning; and state/transition contracts across agents, devices, games and physical artifacts. fileciteturn260file0L2-L6

Project 79 turns such analogies into explicit candidate mappings:

```yaml
AnalogyCandidate:
  source_domain:
  target_domain:
  shared_structure:
  mapping:
  invariants:
  non_equivalences:
  predictions:
  falsification_test:
```

The system must prove the mapping's useful consequences rather than treating metaphor as scientific identity.

## 17. Knowledge Promotion Ladder

```text
RAW SOURCE
   ↓
EXTRACTED CLAIM
   ↓
NORMALIZED OBSERVATION
   ↓
REPRODUCIBLE COMPUTATION
   ↓
CANDIDATE HYPOTHESIS
   ↓
DISCRIMINATING TEST
   ↓
INDEPENDENT REPLICATION
   ↓
DOMAIN REVIEW
   ↓
ESTABLISHED RESULT
```

The ladder is intentionally conservative.

A failed experiment is not deleted. It becomes a bounded negative result with the exact conditions under which it failed.

## 18. Discovery Portfolio

The system maintains a global frontier table:

| Field | Meaning |
|---|---|
| Discovery value | potential scientific/engineering importance |
| Evidence maturity | current evidence state |
| Discriminability | how well candidate tests distinguish hypotheses |
| Feasibility | cost/technical accessibility |
| Replicability | expected ease of independent reproduction |
| Risk | safety/ethical/operational consequence |
| Cross-domain leverage | usefulness beyond one domain |
| Novelty | distance from known solution families |
| Uncertainty | residual epistemic uncertainty |
| Status | active / stalled / refuted / replicated / established |

This prevents the system from spending all compute on easy questions merely because they are easy to score.

## 19. Resource Allocation

Discovery compute is allocated by scientific value rather than raw benchmark performance.

```text
DISCOVERY QUEUE
   ↓
VALUE / INFORMATION / FEASIBILITY SCORE
   ↓
RESOURCE ALLOCATION
   ├─ LLM inference
   ├─ symbolic compute
   ├─ distributed data processing
   ├─ GPU simulation
   ├─ formal proving
   └─ physical experiment budget
```

Project 61 supplies probabilistic optimization; Project 65 supplies compute/runtime infrastructure; Project 72 supplies control and assurance.

## 20. Agent Architecture

Use heterogeneous specialists with non-overlapping failure modes:

```text
DISCOVERY ORCHESTRATOR
├── Literature Agent
├── Data Agent
├── Formal Mathematics Agent
├── Causal Inference Agent
├── Simulation Agent
├── Experimental Design Agent
├── Falsifier
├── Reproduction Agent
├── Domain Specialist(s)
└── Assurance Agent
```

No specialist can promote its own output to `ESTABLISHED_RESULT`.

Roles are capability partitions, not authorization grants.

## 21. Runtime Architecture

```text
                         OMNIDISCOVERY
                              │
             ┌────────────────┼─────────────────┐
             ↓                ↓                 ↓
       KNOWLEDGE PLANE   HYPOTHESIS PLANE   EXPERIMENT PLANE
             │                │                 │
       evidence graph     model registry    experiment registry
       source registry    prediction engine  digital/physical tests
             │                │                 │
             └────────────────┼─────────────────┘
                              ↓
                     DISCOVERY CONTROLLER
                              │
                ┌─────────────┼─────────────┐
                ↓             ↓             ↓
             CAUSAL        FORMAL       SIMULATION
             ENGINE        ENGINE         ENGINE
                │             │             │
                └─────────────┼─────────────┘
                              ↓
                    REPLICATION CONTROLLER
                              ↓
                       PROMOTION GATE
                              ↓
                     KNOWLEDGE GRAPH
                              ↺
```

Everything consequential passes through Project 72 assurance.

## 22. API Contracts

### Discovery API

```text
create_discovery()
add_hypothesis()
add_observation()
compare_models()
propose_experiment()
validate_experiment()
run_simulation()
request_physical_execution()
register_observation()
update_belief()
request_replication()
promote_result()
refute_hypothesis()
```

### Hard contract

```text
promote_result()
```

must fail unless the required evidence class for that domain is present.

## 23. Domain-specific promotion rules

### Mathematics
Required:

- exact formal statement;
- assumptions;
- dependency graph;
- counterexample search;
- formal proof where the claim is theorem-like;
- independent checking.

### Physics / engineering
Required:

- model;
- derived observable;
- calibrated measurement;
- uncertainty analysis;
- controls;
- replication where feasible.

### Biology / medicine
Required:

- domain-specific experimental design;
- appropriate biological controls;
- uncertainty and confounding analysis;
- independent replication;
- ethics/regulatory review where applicable.

### Social science / economics
Required:

- sampling/provenance;
- causal identification where causal claims are made;
- robustness / sensitivity analysis;
- temporal validation;
- replication.

### Software / AI
Required:

- reproducible environment;
- benchmark/evaluation protocol;
- adversarial tests;
- regression evidence;
- runtime/postcondition verification.

These are engineering gates, not claims that one universal methodology exists across disciplines.

## 24. Safety Architecture

The system must be powerful in reasoning while conservative in action.

```text
MODEL / AGENT
      ↓
PROPOSE
      ↓
EXPERIMENT COMPILER
      ↓
SAFETY CLASSIFICATION
      ↓
CAPABILITY BROKER
      ↓
AUTHORIZATION
      ↓
HUMAN / DOMAIN REVIEW WHEN REQUIRED
      ↓
CONTROLLED EXECUTION
      ↓
READBACK
```

No generated research objective can expand its own permissions.

High-risk physical, biological, chemical, medical, financial or security experiments require domain-specific controls and are not executable merely because they are scientifically interesting.

## 25. Adversarial Discovery Defense

A discovery system is itself vulnerable to epistemic attacks:

- poisoned sources;
- synthetic citations;
- manipulated datasets;
- adversarial examples;
- memory poisoning;
- false replication;
- correlated model consensus;
- benchmark gaming;
- selection bias;
- malicious or accidental sensor corruption.

The defense is not another LLM prompt. It is:

```text
PROVENANCE
+
INDEPENDENT SOURCES
+
SOURCE DIVERSITY
+
BLIND REPLICATION
+
AUTHORITATIVE READBACK
+
FORMAL / STATISTICAL CHECKS
+
TRAJECTORY ASSURANCE
```

Project 58's monitorability principle applies directly: reduced observability must increase independent verification rather than lower scrutiny. fileciteturn239file0L1-L2

## 26. Memory Architecture

Research memory is divided into:

```text
CONVERSATION STATE
RUN STATE
DISCOVERY STATE
EVIDENCE STATE
MODEL STATE
EXPERIMENT STATE
KNOWLEDGE STATE
AUTHORITATIVE DOMAIN STATE
```

Memory is guidance and historical state, not authorization. The repository's sandbox-memory model explicitly separates conversation history, sandbox state and distilled memory and warns that memory can become stale. fileciteturn290file0L2-L6

## 27. Communication Compiler

Once a result has passed its promotion gate, the system can generate:

- scientific report;
- reproducibility package;
- technical specification;
- visualization;
- public explanation;
- patent-oriented disclosure draft;
- business/engineering opportunity analysis.

The artifact compiler inherits the evidence ledger. It may simplify expression, but cannot upgrade epistemic status. This extends the repository's professional-artifact compiler, where generated writing remains an output artifact rather than an evidence source. fileciteturn256file0L2-L6

## 28. First Grand Research Programs

Project 79 should begin with problems that have:

1. high cross-domain leverage;
2. measurable observables;
3. meaningful competing hypotheses;
4. feasible digital experiments;
5. an identifiable path to physical validation;
6. strong falsification criteria.

Candidate program classes:

```text
A. MATHEMATICS
   TRS / structural mathematics / complexity questions

B. FUNDAMENTAL PHYSICS
   stability / quantum-gravity constraints / anomaly discrimination

C. COMPLEX SYSTEMS
   common stability structures across physical, computational and biological systems

D. AI SCIENCE
   capability, monitorability, learning and agentic-runtime behavior

E. LANGUAGE
   temporal semantic change and machine reasoning over historical language

F. ENGINEERING
   vehicle/device diagnostics and physical-system anomaly detection
```

These are candidate programs, not claims that the underlying theories are correct.

## 29. The Potential World-Changing Discovery Mechanism

The project deliberately targets a capability that is more fundamental than one individual scientific answer:

> **A machine-readable system for selecting the next most informative experiment across heterogeneous scientific hypotheses, while preserving provenance, causality, formal correctness, reproducibility and authorization.**

If validated, this would create a new research-production loop:

```text
HUMAN QUESTION
      ↓
MACHINE MAPS UNKNOWN SPACE
      ↓
MACHINE GENERATES COMPETING MODELS
      ↓
MACHINE FINDS WHERE MODELS DISAGREE
      ↓
MACHINE SELECTS MOST DISCRIMINATING SAFE TEST
      ↓
TEST PRODUCES OBSERVATION
      ↓
SYSTEM UPDATES KNOWLEDGE
      ↓
INDEPENDENT SYSTEM REPRODUCES RESULT
      ↓
NEW KNOWLEDGE BECOMES MACHINE-READABLE
      ↓
NEXT EXPERIMENT IS CHOSEN
      ↺
```

The novelty claim is therefore about the **integrated discovery architecture**, not about inventing active learning, Bayesian inference, causal inference, formal methods or automated experimentation individually. Those are existing disciplines/components; the project combines them under one governed discovery state machine.

## 30. Verification Plan

### V0 — Corpus reconstruction

Reconstruct the complete repository knowledge graph and map every knowledge artifact to:

- domain;
- concepts;
- project lineage;
- evidence class;
- unresolved questions;
- reusable computational primitive.

### V1 — Synthetic benchmark

Construct benchmark worlds with known hidden mechanisms. Measure whether the system selects experiments that recover the known mechanism more efficiently than:

- random experiment selection;
- uncertainty sampling alone;
- prediction-accuracy optimization alone;
- single-agent research;
- static literature retrieval.

### V2 — Simulation benchmark

Run the controller against synthetic and established computational models with blinded ground truth.

### V3 — Cross-solver replication

Require independent model families, symbolic solvers or implementations to reproduce promoted computational discoveries.

### V4 — Real-data retrospective validation

Use historical datasets where the eventual answer is known, but hide the answer during discovery planning.

### V5 — Prospective low-risk experiment

Select a bounded real-world experiment with measurable outcome, low consequence and independent measurement.

### V6 — Domain replication

Repeat using an independent team, implementation or instrumentation path.

### V7 — Scientific promotion

Only after the evidence ladder is satisfied may a result enter the `ESTABLISHED_RESULT` class.

## 31. Metrics

### Discovery efficiency

```text
information_gain / cost
useful_discoveries / compute
hypothesis_elimination / experiment
```

### Scientific quality

```text
replication_rate
false_discovery_rate
calibration
prediction_accuracy
causal_identification_success
formal_verification_rate
```

### Search quality

```text
hypothesis_diversity
novelty
disagreement_coverage
experiment_discriminability
```

### Operational quality

```text
recovery_rate
execution_failures
postcondition_failures
resource_cost
latency
human_review_burden
```

No target threshold is assumed before baseline experiments.

## 32. Definition of Done

Project 79 reaches **Architecture Validated** when:

- a versioned unknowns/hypotheses/evidence graph exists;
- competing hypotheses can be represented without forced consensus;
- models generate explicit observable predictions;
- the Prediction-Difference Engine identifies discriminating observations;
- the Experiment Design Compiler produces typed experiment specifications;
- digital simulations execute reproducibly;
- causal and formal backends can validate applicable claims;
- independent replication is enforced;
- discovery manifests preserve complete provenance;
- promotion gates prevent epistemic type confusion;
- Project 72 verifies consequential execution;
- the system demonstrates measurable advantage over at least two baseline experiment-selection strategies on blinded benchmarks.

## 33. Non-goals

- No claim of artificial general intelligence.
- No claim of machine consciousness.
- No claim of automatic scientific authority.
- No automatic execution of high-risk experiments.
- No replacement of domain scientists or ethics/regulatory authorities.
- No conversion of speculative theories into facts.
- No use of model consensus as proof.
- No claim that one universal discovery objective works for every scientific domain.

## 34. Portfolio Integration

| Existing project | Project 79 role |
|---|---|
| 15 | general research orchestration |
| 19 | evidence/hypothesis research runtime |
| 26 | capability firewall and trustworthy-kernel controls |
| 27 | solver diversity / disagreement |
| 28 | generator → verifier → repair → test |
| 31 | sovereign execution fabric |
| 32 | evidence/OSINT graph discipline |
| 38 | scientific stability verification |
| 41 | world/repository state |
| 48 | grand-challenge and unknowns registry |
| 50 | physical/phygital experiment substrate |
| 54 | epistemic control |
| 55 | stochastic integrity |
| 58 | monitorability-aware oversight |
| 60 | adversarial multimodal evaluation |
| 61 | probabilistic learning and optimization |
| 62 | causal/distributed intelligence |
| 65 | AI-native compute / agent factory |
| 68 | constitutional runtime |
| 69 | adversarial continuity |
| 70 | auditable stochastic systems |
| 71 | physical artifact / HIL substrate |
| 72 | universal runtime assurance |
| 73–76 | concrete narrative, device, language and sensory application testbeds |
| 77 | formal mathematics |
| 78 | stochastic audit / simulation |

## 35. Fundamental invariant

```text
THE SYSTEM MAY SEARCH THE SPACE OF POSSIBILITIES.
IT MAY NOT DECLARE REALITY WITHOUT EVIDENCE.
```

And operationally:

```text
DISCOVERY POWER ↑
        ↓
EVIDENCE REQUIREMENTS ↑
        ↓
INDEPENDENCE ↑
        ↓
VERIFICATION DEPTH ↑
```

## Evidence classification

**SOURCE_DERIVED:** The repository's knowledge base contains research orchestration, unknowns mapping, probabilistic learning, causal inference, formalization, simulation, agent assurance, physical/digital execution, multimodal evidence and adaptive runtime patterns. The knowledge-base README explicitly identifies these as durable research/engineering domains. fileciteturn292file0L2-L6

**INFERRED:** These capabilities form a natural stack for a closed-loop discovery controller whose missing abstraction is experiment selection and knowledge-state evolution rather than another general-purpose research assistant. Existing Project 19 already performs evidence/hypothesis orchestration, while Project 72 provides the assurance boundary. fileciteturn237file0L2-L6 fileciteturn233file0L2-L6

**PROPOSED:** The integrated architecture could materially accelerate discovery if it demonstrates superior experiment selection, lower false-discovery rates and reproducible gains against blinded baselines. Those claims must be established experimentally.
