# Project 43 — Influence Literacy & Human Agency Lab MAX

## Mission
Build a **defensive influence-intelligence and human-agency protection layer** that detects coercive, deceptive, manipulative or dependency-forming patterns across text, voice, interfaces, advertising and multimodal campaigns while preserving informed user choice.

The supplied NLP/advertising material describes Future Pacing, presuppositions, embedded commands, sensory/VAK language and deliberately ambiguous phrasing as influence techniques. fileciteturn175file2L5-L25 These mechanisms are treated here as detection features and research hypotheses, not as instructions for covert persuasion.

## Scientific boundary

The supplied report makes strong causal claims about unconscious purchasing and neurochemical responses. Those claims are **source-derived hypotheses**, not assumed scientific ground truth. The system therefore labels each finding as:

`OBSERVED | SOURCE_CLAIM | INFERRED | HYPOTHESIS | VALIDATED | REJECTED`

No detector may infer a person's mental state as fact from linguistic or visual cues alone.

## Architecture

```text
MESSAGE / UI / AD / AUDIO / VIDEO / CAMPAIGN
                 ↓
          NORMALIZE + PROVENANCE
                 ↓
          CONTEXT / TRAJECTORY GRAPH
                 ↓
        INFLUENCE-SIGNAL EXTRACTOR
       ↙            ↓             ↘
 LANGUAGE         VISUAL        INTERACTION
   SIGNALS         SIGNALS        SIGNALS
       ↘            ↓             ↙
          COUNTER-EVIDENCE ENGINE
                 ↓
       RISK + UNCERTAINTY MODEL
                 ↓
       EXPLAINABLE USER REPORT
                 ↓
        USER-CONTROLLED MITIGATION
```

## Signal taxonomy

```yaml
InfluenceSignal:
  id:
  category:
  observation:
  exact_span_or_region:
  source:
  timestamp:
  confidence:
  alternative_explanations:
  corroboration:
  provenance:
```

Categories include:

- urgency/scarcity pressure;
- authority framing;
- social proof;
- commitment escalation;
- emotional pressure;
- dependency/reward loops;
- hidden or embedded directives;
- presupposition / assumption loading;
- future-pacing claims;
- vague or underspecified language;
- sensory/VAK framing;
- asymmetric disclosure;
- dark-pattern friction.

A signal is never equivalent to malicious intent.

## Linguistic Transparency Compiler

A supplied pattern such as:

`artful vagueness → presupposition → embedded directive → urgency`

is transformed into a **transparency test**:

```text
INPUT
 ↓
LINGUISTIC PARSE
 ↓
EXPLICIT CLAIMS
 ↓
PRESUPPOSITIONS
 ↓
IMPERATIVE / DIRECTIVE SPANS
 ↓
MISSING INFORMATION
 ↓
USER-CHOICE IMPACT
 ↓
TRANSPARENT REWRITE
```

The transparent rewrite must state assumptions openly and preserve the ability to decline.

## NLP / VAK defensive analysis

The source presents Visual, Auditory and Kinesthetic language categories. fileciteturn55file10L574-L594

The defensive detector may identify sensory framing, but it must not:

- infer personality from VAK wording;
- infer susceptibility from a sensory preference;
- optimize a message against an inferred vulnerability;
- claim neurochemical effects that were not experimentally established.

Instead it asks:

`What is explicitly said? What is implied? What is omitted? What choice architecture does this create?`

## Human Agency Score

```yaml
AgencyProfile:
  choice_visibility:
  reversibility:
  pressure_level:
  personalization_intensity:
  disclosure_quality:
  opt_out_friction:
  repetition:
  uncertainty:
  provenance_coverage:
```

A high-risk result triggers **explanation and user-controlled mitigation**, not hidden intervention.

## Trajectory-aware analysis

A single message may be benign while the sequence creates pressure:

```text
TURN 1 → TURN 2 → TURN 3 → ... → TURN N
                 ↓
       ESCALATION / REPETITION
                 ↓
        AGENCY-RISK ASSESSMENT
```

Track:

`repetition + urgency accumulation + commitment escalation + reversibility loss + disclosure asymmetry`.

## Counterfactual engine

For each material finding:

```text
OBSERVED EXPERIENCE
        ↓
PRESSURE MECHANISM
        ↓
MINIMAL DESIGN CHANGE
        ↓
LOW-INFLUENCE ALTERNATIVE
        ↓
USER CHOICE PRESERVED
```

Example output categories are structural rather than manipulative: make price visibility clearer, expose assumptions, remove false urgency, reduce opt-out friction, or separate recommendation from action.

## Campaign graph

```text
SOURCE
  ↓
ASSET
  ↓
ACCOUNT / CHANNEL
  ↓
MESSAGE / UI
  ↓
INFLUENCE SIGNAL
  ↓
AUDIENCE RESPONSE
```

Every edge requires provenance, confidence and timestamp. Correlation does not establish common intent.

## Defensive threat model

The system is explicitly resistant to:

- hidden directives in content;
- adversarial paraphrase;
- multilingual obfuscation;
- multimodal reinforcement;
- pressure distributed over multiple turns;
- conflicting explanations;
- detector gaming;
- provenance stripping;
- misleading engagement metrics.

## Metric integrity

Engagement is not a sufficient success metric. The system reports:

```text
ENGAGEMENT
+ CHOICE VISIBILITY
+ REVERSIBILITY
+ DISCLOSURE
+ USER COMPREHENSION
+ FALSE-POSITIVE BURDEN
```

A system that increases conversion by reducing informed choice is classified as a failed safety outcome even when revenue rises.

## Evaluation

### Detection
- recall on annotated influence patterns;
- precision on benign persuasive content;
- trajectory-level detection rate;
- false-positive burden;
- multilingual/paraphrase robustness.

### Explanation
- evidence coverage;
- exact-span attribution;
- provenance coverage;
- alternative-explanation quality;
- user comprehension.

### Agency
- choice visibility improvement;
- opt-out friction reduction;
- reversibility improvement;
- pressure-indicator reduction;
- disclosure improvement.

### Robustness
- adversarial evasion rate;
- multimodal consistency;
- model disagreement;
- calibration error;
- drift across campaigns.

## Integration with OmniCore

```text
CONTENT / INTERACTION
        ↓
OBSERVATION GRAPH
        ↓
PROJECT 43 SIGNALS
        ↓
PROJECT 35 INTENT / TRAJECTORY SECURITY
        ↓
PROJECT 26 CAPABILITY / TRUST BOUNDARY
        ↓
PROJECT 34 BUSINESS / VALUE REVIEW
        ↓
USER-CONTROLLED DECISION
```

Projects 34 and 45 may use the output as a **policy and ethical-economics gate**, never as a targeting engine.

## Definition of Done

- multimodal influence-signal schema;
- linguistic transparency compiler;
- trajectory-level risk model;
- provenance and evidence chain;
- counter-evidence and counterfactual explanations;
- human-agency score;
- campaign graph;
- adversarial robustness suite;
- calibrated uncertainty;
- explicit no-covert-manipulation policy;
- measurable user-agency outcomes.
