# Project 43 — Influence Literacy & Human Agency Lab MAX

## Mission
Build a defensive intelligence layer that detects coercive, deceptive, manipulative and dependency-forming interaction patterns across text, voice, interfaces and multimodal campaigns while preserving informed user choice.

## Scope
The source project is retained as a defensive research/product artifact. The upgrade adds trajectory analysis, provenance, counterfactual explanations, campaign-level correlation and measurable human-agency protections. fileciteturn159file0L2-L2

## Architecture

```text
MESSAGE / UI / AUDIO / VIDEO / CAMPAIGN
                 ↓
          NORMALIZE + PROVENANCE
                 ↓
          CONTEXT / TRAJECTORY GRAPH
                 ↓
        INFLUENCE-SIGNAL EXTRACTOR
                 ↓
     ┌───────────┼────────────┐
     ↓           ↓            ↓
 LINGUISTIC   VISUAL       BEHAVIORAL
     ↓           ↓            ↓
     └───────────┼────────────┘
                 ↓
       COUNTER-EVIDENCE ENGINE
                 ↓
       RISK + UNCERTAINTY MODEL
                 ↓
        EXPLAINABLE USER REPORT
                 ↓
      USER-CONTROLLED MITIGATION
```

## Signal model

```yaml
InfluenceSignal:
  id:
  category:
  observation:
  source:
  timestamp:
  confidence:
  alternative_explanations:
  corroboration:
  provenance:
```

Categories can include:

- urgency/scarcity pressure;
- authority framing;
- social proof;
- commitment escalation;
- emotional pressure;
- dependency/reward loops;
- hidden directives;
- asymmetric disclosure;
- dark-pattern friction.

Signals are not treated as proof of intent.

## Trajectory-aware analysis

A single message can be benign while a sequence is coercive. Therefore:

```text
TURN 1 → TURN 2 → TURN 3 → ... → TURN N
                  ↓
          PATTERN / ESCALATION
                  ↓
          HUMAN-AGENCY RISK
```

Track repetition, escalation, pressure accumulation, reduced reversibility and changes in user choice architecture.

## Human Agency Score

The system computes a multidimensional score rather than a binary label:

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
```

A high-risk score triggers explanation and mitigation options, not hidden intervention.

## Counterfactual engine

For every high-risk finding, generate a neutral alternative:

```text
OBSERVED EXPERIENCE
        ↓
WHAT CREATES PRESSURE?
        ↓
MINIMAL CHANGE
        ↓
LOW-INFLUENCE ALTERNATIVE
```

This turns detection into literacy and gives the user an actionable comparison.

## Campaign graph

Correlate repeated patterns across assets without assuming common intent:

```text
SOURCE → ASSET → ACCOUNT → MESSAGE → PATTERN → AUDIENCE RESPONSE
```

Every graph edge requires provenance and confidence.

## Multimodal evidence

Voice, visual cues and interface behavior are treated as probabilistic evidence. The system must explicitly distinguish:

`observation ≠ inferred intent ≠ established fact`.

## Defensive boundaries

The implementation must not:

- target inferred vulnerabilities for persuasion;
- engineer covert dependency;
- manipulate users without disclosure;
- infer sensitive traits for influence optimization;
- use hidden reward schedules to shape behavior;
- deploy invisible interventions that remove informed choice.

## Evaluation

### Detection
- recall on known patterns;
- precision on benign persuasive material;
- trajectory-level detection rate;
- false-positive burden.

### Explainability
- evidence coverage;
- provenance coverage;
- alternative-explanation quality;
- user comprehension.

### Agency
- choice visibility improvement;
- reduced opt-out friction;
- reversibility gain;
- reduction in pressure indicators.

### Robustness
- paraphrase robustness;
- multimodal consistency;
- adversarial evasion rate;
- model disagreement rate.

## Definition of Done

Project 43 is complete when it can detect and explain influence risks across content and interaction trajectories, preserve uncertainty, provide non-coercive alternatives and measurably improve user agency without becoming an influence engine itself.
