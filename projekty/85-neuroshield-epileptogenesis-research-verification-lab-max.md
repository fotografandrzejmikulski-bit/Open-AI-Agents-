# Project 85 — NeuroShield Epileptogenesis Research & Verification Lab MAX

## Status
PROPOSED → RESEARCH ARCHITECTURE BASELINE → PROJECT GENESIS 2026-09-10

## Mission
Create a rigorous research program for evaluating disease-modifying approaches to epileptogenesis, inspired by the supplied NeuroShield-GeneBlock concept, with emphasis on target validation, biomarker discovery, delivery feasibility, safety, translational evidence and falsification.

## Scope boundary
This is a **research and verification architecture**, not a clinical protocol, prescription, gene-therapy manufacturing procedure or treatment recommendation. The supplied document presents a theoretical multi-target strategy; the repository does not treat its efficacy or safety as established.

## Source-derived research thesis
The source argues that controlling seizures does not necessarily interrupt the underlying process of epileptogenesis and proposes a multi-level strategy spanning molecular/genetic, synaptic and inflammatory mechanisms, together with early diagnosis and targeted delivery.

## Research architecture
```text
CLINICAL / PRECLINICAL QUESTION
        ↓
MECHANISTIC HYPOTHESES
        ↓
TARGET / BIOMARKER VALIDATION
        ↓
COMPETING MODELS
        ↓
PRECLINICAL EVIDENCE
        ↓
SAFETY / DELIVERY ASSESSMENT
        ↓
INDEPENDENT REPLICATION
        ↓
TRANSLATIONAL REVIEW
        ↓
GO / NO-GO DECISION
```

## Diagnostic layer
The source identifies early epileptogenesis as a key research window and discusses electrophysiological, molecular and imaging biomarkers. Project 85 treats these as candidate evidence channels whose predictive value must be independently measured rather than assumed.

## Therapeutic hypothesis layer
The supplied concept is explicitly multitarget. Project 85 evaluates target combinations as competing hypotheses and asks whether each component provides incremental benefit, whether interactions are reproducible and whether safety costs outweigh potential efficacy.

Specific molecular constructs from the source are retained as source lineage but are **not promoted here into operational wet-lab instructions**.

## Delivery / translational layer
The source discusses engineered viral-vector delivery and focused-ultrasound approaches to access the brain. Project 85 treats delivery as a separate risk domain covering biodistribution, immunogenicity, off-target effects, durability, reversibility, manufacturing quality and regulatory feasibility.

## Verification framework
Every major claim must carry:

```yaml
EvidenceRecord:
  claim:
  model_system:
  endpoint:
  comparator:
  sample_design:
  uncertainty:
  replication_status:
  safety_signal:
  provenance:
  decision:
```

## Falsification criteria
A candidate is downgraded or rejected if:
- the proposed biomarker fails prospective validation;
- efficacy disappears under independent replication;
- benefit is limited to a narrow model without translational justification;
- delivery creates unacceptable safety signals;
- mechanistic assumptions are contradicted by evidence;
- long-term effects cannot be characterized sufficiently for the proposed use.

## Integration with Project 79
Project 79 supplies the governed discovery loop. Project 85 supplies a domain-specific biomedical research track:

```text
UNKNOWN
 ↓
HYPOTHESIS
 ↓
DISCRIMINATING EXPERIMENT
 ↓
OBSERVATION
 ↓
REPLICATION
 ↓
EVIDENCE
 ↓
TRANSLATIONAL DECISION
```

## Safety and governance
Human or clinical use requires qualified biomedical researchers, institutional oversight, ethics review, regulatory compliance and appropriately designed clinical studies. No repository artifact is evidence that a person should receive the proposed therapy.

## Definition of done
The project reaches a meaningful milestone only when a clearly scoped mechanistic hypothesis has reproducible evidence, an independently validated biomarker or endpoint, characterized safety signals and a documented translational decision. A theoretical design alone is never counted as a therapeutic success.
