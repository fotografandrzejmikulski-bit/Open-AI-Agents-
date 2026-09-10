# Project 92 — Multimodal Deception Analysis & Investigative Interviewing Lab MAX

## Status
PROPOSED → RESEARCH ARCHITECTURE BASELINE → PROJECT GENESIS 2026-09-10

## Mission
Build a reproducible research and analysis laboratory for multimodal deception-related signals, investigative interviewing and forensic statement analysis.

The project does **not** claim that an AI can determine whether a person is lying from a face, gesture, word or voice. Its canonical output is an uncertainty-aware analytical assessment with alternative explanations, evidence provenance and explicit limitations.

## Why this is a new project
Projects 32 and 54 provide general evidence/OSINT and cognitive-security infrastructure. Project 75 provides Polish linguistic intelligence. None owns a dedicated laboratory combining behavioral observation, FACS-style coding, statement analysis, interview methodology and multimodal temporal evidence as a separately evaluated research domain.

## Source-derived foundation
The supplied corpus integrates FACS/microexpression analysis, Reid vs PEACE interviewing and Statement Analysis. It explicitly states that a single gesture or microexpression is not definitive proof of lying. It also documents false-confession risks in coercive interrogation and contrasts these with the information-gathering orientation of PEACE. fileciteturn522file11L472-L498 fileciteturn522file9L397-L413

## Canonical pipeline
```text
CASE / RESEARCH QUESTION
        ↓
CONSENT / LEGAL SCOPE
        ↓
BASELINE OBSERVATION
        ↓
MULTIMODAL CAPTURE
        ├── video / FACS-style events
        ├── audio / prosody
        ├── transcript / linguistic features
        └── interaction timeline
        ↓
CANDIDATE SIGNALS
        ↓
TEMPORAL CLUSTERING
        ↓
ALTERNATIVE EXPLANATIONS
        ↓
INFORMATION-GATHERING FOLLOW-UP
        ↓
EVIDENCE CORRELATION
        ↓
UNCERTAINTY-AWARE ASSESSMENT
        ↓
HUMAN REVIEW
```

## Behavioral evidence model
```yaml
BehavioralObservation:
  id:
  timestamp:
  modality: face|body|voice|text|interaction
  observed_feature:
  coding_scheme:
  baseline_reference:
  stimulus_reference:
  temporal_window:
  confidence:
  alternative_explanations: []
  source_ref:
```

The distinction between observation and interpretation is mandatory. "AU observed" is not equivalent to "person lied".

## Baseline and cluster model
The source proposes baseline observation followed by a stimulus and temporal cluster analysis. The laboratory treats this as a research protocol rather than a validated universal detector. Individual baseline, culture, disability, stress, fatigue, camera angle, language and context can affect observed behavior.

A cluster is therefore a candidate anomaly requiring follow-up, not a verdict.

## Interview methodology
The laboratory stores both Reid and PEACE as comparative methodological objects.

### Reid
Retained for historical/comparative research and risk analysis. The source describes its confession-oriented structure and significant false-confession risk. It must not become an automated coercion engine.

### PEACE
Preferred research baseline for information gathering because it emphasizes planning, rapport, free account, clarification, challenge through evidence and evaluation. fileciteturn522file12L511-L529

## Statement analysis
The system can calculate candidate linguistic features such as pronoun shifts, tense changes, narrative structure, editing/latency and distancing language. These are hypotheses whose predictive value must be evaluated on controlled datasets.

The source itself includes a scientific caution: statement-analysis indicators must not be treated as deterministic proof. fileciteturn522file0L28-L40

## Multimodal evidence graph
```text
CASE
 ├── PERSON / ENTITY
 ├── STATEMENT
 │    ├── linguistic observation
 │    └── source timestamp
 ├── VIDEO SEGMENT
 │    └── coded behavioral event
 ├── AUDIO SEGMENT
 │    └── prosodic event
 ├── STIMULUS
 ├── BASELINE
 ├── HYPOTHESIS
 └── ALTERNATIVE EXPLANATION
```

No edge may imply guilt, deception or intent unless independently established by admissible evidence outside the behavioral feature itself.

## Evaluation
1. Inter-rater agreement for behavioral coding.
2. Baseline stability across repeated sessions.
3. False-positive and false-negative rates.
4. Cross-cultural and multilingual robustness.
5. Accessibility and disability confounds.
6. Camera/audio quality sensitivity.
7. Generalization to unseen speakers and scenarios.
8. Calibration of confidence and uncertainty.
9. Ablation of individual modalities.
10. Comparison with non-behavioral evidence.

## Privacy and human-subject boundary
The laboratory requires informed consent or an appropriate lawful research basis, minimization, retention limits, access controls, redaction and explicit publication boundaries.

It must not be used to infer sensitive traits, criminal guilt or psychological diagnosis from behavioral appearance alone.

## Integration
- Project 19 — research orchestration.
- Project 32 — evidence graph, provenance and OSINT methodology.
- Project 54 — cognitive/adversarial security.
- Project 57 — multimodal sensing and interaction.
- Project 72 — assurance and runtime verification.
- Project 75 — Polish linguistic/semantic layer.
- Project 91 — synthetic persona/behavior evaluation.

## Hard invariants
1. No single cue proves deception.
2. Observation ≠ interpretation ≠ conclusion.
3. A behavioral anomaly requires alternative explanations.
4. Model confidence never becomes legal or investigative certainty.
5. Coercive interrogation is not an acceptable automated capability.
6. Human review remains mandatory for consequential assessments.
7. Evidence provenance is immutable and auditable.
8. Research results require held-out evaluation and replication.
9. Sensitive trait inference is outside scope.
10. Behavioral analysis cannot replace corroborating evidence.

## Definition of Done
- versioned multimodal observation schema;
- baseline/cluster analysis engine;
- FACS-compatible event representation;
- transcript/linguistic feature layer;
- PEACE-oriented interview workflow;
- evidence graph with provenance;
- uncertainty calibration;
- bias/confound evaluation suite;
- human-review workflow;
- reproducible research datasets and reports.
