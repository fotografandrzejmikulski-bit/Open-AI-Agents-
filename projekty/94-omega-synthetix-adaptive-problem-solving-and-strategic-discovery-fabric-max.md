# Project 94 — Omega-Synthetix Adaptive Problem-Solving & Strategic Discovery Fabric MAX

## Status

`PROPOSED` — architecture baseline derived from the 2026-09-10 source batch. The source describes OSP as a methodology; this artifact defines an engineering boundary for a reusable decision/discovery system.

## Mission

Build a governed system for solving complex and poorly specified problems by explicitly modelling uncertainty, generating competing hypotheses, deploying specialized agents, running counterfactual simulations and bounded experiments, and updating the model from verified evidence.

## Distinction from Project 67

Project 67 is centered on business-model/strategy representation, concretization, experimentation and realized business outcomes. Project 94 operates one level earlier and more broadly: **problem finding, uncertainty reduction, system modelling and strategic discovery** across domains. Business strategy is one application domain, not the system's boundary.

## Source-derived architecture

```text
REAL WORLD / DATA / OBSERVATIONS
            ↓
     EVIDENCE NORMALIZER
            ↓
   SYSTEM + BOUNDARY MODEL
            ↓
 PROBABILISTIC STATE / DIGITAL TWIN
            ↓
 UNCERTAINTY + ASSUMPTION GRAPH
            ↓
 COMPETING HYPOTHESIS GENERATOR
            ↓
 MULTI-AGENT THINK TANK (MATT)
 ├─ Researcher
 ├─ Devil's Advocate
 ├─ Futurist
 ├─ Risk Analyst
 ├─ Compliance Analyst
 └─ Domain Specialists
            ↓
 COUNTERFACTUAL / GENERATIVE SIMULATION
            ↓
 EXPERIMENT DESIGN / INFORMATION VALUE
            ↓
 BOUNDED EXECUTION
            ↓
 MEASUREMENT + INDEPENDENT VERIFICATION
            ↓
 POSTERIOR / MODEL UPDATE
            ↺
 STRATEGIC RECOMMENDATION
```

## Core objects

### ProblemSpec
- objective;
- system boundary;
- constraints;
- stakeholders;
- available actions;
- unknowns;
- consequence level.

### EvidenceRecord
- observation;
- source/provenance;
- timestamp/freshness;
- reliability assessment;
- direct vs inferred status.

### StateModel
- observable variables;
- hidden-state hypotheses;
- transition assumptions;
- uncertainty distributions;
- dependencies.

### Hypothesis
- claim;
- assumptions;
- predicted observations;
- falsification conditions;
- confidence;
- competing alternatives.

### AgentRole
- specialization;
- priors/objectives;
- tool scope;
- evidence access;
- conflict-of-interest metadata;
- output schema.

### ExperimentSpec
- hypothesis under test;
- intervention;
- comparator/control;
- expected information gain;
- budget/risk ceiling;
- success and stop rules;
- reproducibility requirements.

### DecisionRecord
- alternatives;
- evidence set;
- uncertainty;
- simulation results;
- experiment results;
- recommendation;
- authorization state;
- final human/system decision.

## Omega Loop

The project implements the source's exploration/exploitation concept as a governed controller:

```text
EXPLORE
  ↓
UNCERTAINTY HIGH?
  ├─ yes → acquire evidence / run experiment / simulate
  └─ no  → evaluate action
  ↓
EXPLOIT / EXECUTE
  ↓
OBSERVE OUTCOME
  ↓
MODEL UPDATE
  ↺
```

The controller must not optimize only for short-term reward. Exploration is justified when information can materially change the decision.

## Multi-agent deliberation

Agents exchange structured claims rather than unconstrained prose:

`claim + evidence_refs + assumptions + confidence + counterarguments + recommended_test`.

Consensus is not sufficient evidence. Persistent disagreement is an escalation signal that can trigger additional research, a stronger experiment, or human review.

## Counterfactual engine

The system maintains multiple candidate worlds/models rather than a single forecast. Simulation output is explicitly labelled as simulated evidence and cannot be promoted to real-world outcome without external verification.

## Decision policy

```text
OBSERVED FACT
   ↓
INFERENCE
   ↓
HYPOTHESIS
   ↓
SIMULATION / EXPERIMENT
   ↓
VERIFIED RESULT
   ↓
AUTHORIZED ACTION
```

No layer may silently promote an assumption, model output or simulation into a verified fact.

## Integration

Project 94 extends:
- Project 19 — research orchestration/evidence graph;
- Project 27 — compound reasoning and self-consistency;
- Project 34 — agentic venture/business-model generation;
- Project 54 — cognitive security and adversarial robustness;
- Project 61 — OmniCore convergence fabric;
- Project 63/64 — decision intelligence and Bayesian predictive BI;
- Project 66/67 — adaptive strategy and experimentation;
- Project 72 — cross-framework agent assurance;
- Project 79 — autonomous scientific discovery;
- Project 80 — self-evolving computing substrate;
- Project 90 — SOP/process knowledge compiler;
- Project 91 — synthetic persona/cognitive-style engineering.

## Runtime placement

When implemented on OmniCore, Project 94 is a **decision/discovery workload**, not a privileged authority layer. It may generate models, hypotheses, experiments and recommendations; capability authorization, policy enforcement, execution and authoritative readback remain outside the model.

## Evaluation

### Epistemic quality
- source provenance;
- calibration;
- uncertainty quality;
- alternative-hypothesis coverage;
- falsifiability.

### Reasoning quality
- disagreement handling;
- self-consistency;
- causal coherence;
- counterfactual robustness.

### Experiment quality
- information value;
- control/comparator quality;
- reproducibility;
- stopping discipline;
- risk containment.

### Decision quality
- predicted vs realized outcome;
- calibration error;
- regret/downside;
- robustness under model variation;
- post-decision learning.

## Roadmap

### G0 — schemas
Typed ProblemSpec, EvidenceRecord, StateModel, Hypothesis, AgentRole, ExperimentSpec and DecisionRecord.

### G1 — evidence graph
Connect Project 19 provenance/evidence infrastructure.

### G2 — hypothesis laboratory
Generate and rank competing hypotheses with explicit falsification conditions.

### G3 — MATT
Implement role-specialized agents and structured deliberation.

### G4 — counterfactual simulation
Run multiple candidate models and record uncertainty.

### G5 — experiment engine
Select bounded tests using expected information value and consequence-aware controls.

### G6 — verified decision loop
Connect outcomes, readback and model updates.

### G7 — OmniCore runtime
Integrate with Project 61/80 while keeping model authority separated from execution authority.

### G8 — autonomous discovery
Interface with Project 79 for scientific and technical discovery workloads.

## Governance / safety

1. AI recommendations are proposals, not authorization.
2. High-consequence decisions require explicit policy and appropriate human review.
3. Simulations are not real-world evidence.
4. Digital twins are models, not reality.
5. Synthetic personas are not evidence of real people's future behavior without validation.
6. Agent consensus does not override contradictory primary evidence.
7. Strategic priors remain explicit and auditable.
8. The system must expose uncertainty rather than manufacture confidence.
9. Active collection or consequential external actions remain capability- and authorization-gated.
10. The influence-engineering material in the source batch is retained for defensive analysis only and is not an operational persuasion subsystem.

## Final principle

**Do not ask only “What is the answer?” Ask “What is the system, what do we not know, which competing explanations fit, what evidence would discriminate them, what experiment has the highest information value, and what remains authorized after verification?”**
