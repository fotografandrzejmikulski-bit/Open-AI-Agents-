# Epistemic Signal, Control Integrity & Adversarial Evidence — Knowledge Base

## Scope

This document consolidates the newly supplied corpus into a defensive engineering model for OmniCore. The source set spans: Apeiron 2.0 and 78-card overlay design; stochastic/lottery system analysis; behavioral and linguistic deception analysis; Gemini constraint architecture; computational persuasion and influence systems; advanced prompt/reasoning techniques; and AI monetization/productization patterns.

The transformation rule is strict: source material that describes manipulation, coercive interrogation, gambling exploitation, jailbreaks or safety bypasses is retained as **threat-model/evaluation knowledge**, never as an implementation recipe for harm.

## 1. Source-derived engineering observations

### 1.1 Apeiron: layered state and physical computation

The Apeiron 2.0 corpus treats transparent cards as partial state fragments and makes stacking a core mechanism: context, action and outcome combine into an emergent visual state rather than a simple additive sum. Glitch effects are presented as functional visual signals for incompatibility or instability. fileciteturn80file0L13-L30

The same corpus defines a HEX checksum overlay in which cards expose values 0–F, stacking can produce overflow semantics, and hidden ASCII/HEX layers can be revealed by decoder cards. fileciteturn81file5L229-L252

**Engineering extraction:**
- represent physical cards as typed state projections;
- keep visual interference separate from authoritative state;
- make stack composition deterministic and versioned;
- treat HEX/checksum semantics as a symbolic encoding layer, not factual evidence;
- validate physical readability, alignment and manufacturing tolerances empirically.

### 1.2 Behavioral/deception corpus: signal clusters are not verdicts

The supplied deception report explicitly states that no single gesture or microexpression proves lying and frames deception as a multimodal cognitive process. It combines FACS, interrogation methodology and linguistic analysis. fileciteturn86file2L18-L32

It also distinguishes an accusatory Reid model from the information-gathering PEACE model and documents the false-confession risk of coercive interrogation. fileciteturn86file2L169-L234 fileciteturn86file2L212-L217

The report further shows why baseline, temporal clustering and contextual exploration are useful as **triggers for evidence collection**, not as automatic conclusions. fileciteturn86file2L375-L395

Most importantly, its references include a study explicitly titled *Scientific Content Analysis (SCAN) Cannot Distinguish Between Truthful and Fabricated Accounts of a Negative Event*. fileciteturn86file2L495-L498

**Engineering extraction:**
- `signal != proof`;
- maintain baseline and context for every behavioral feature;
- combine independent modalities before escalation;
- use contradiction-driven questioning rather than coercion;
- represent conclusions as calibrated hypotheses with alternative explanations;
- never present a behavioral score as a factual lie detector.

### 1.3 Gemini constraints: model/data/control plane separation

The Gemini architecture report describes frozen inference-time weights and distinguishes the data plane from the control plane; the model cannot directly rewrite its weights or administrative safety configuration. fileciteturn86file3L523-L553

It also describes external input/output guardrails and infrastructure separation as independent enforcement layers. fileciteturn86file3L660-L705

The agentic risk section identifies excessive privileges and prompt injection as the realistic route by which a model could influence its own surrounding infrastructure; the failure is then architectural, not an instance of model self-modification. fileciteturn86file3L762-L791

**Engineering extraction:**
- policy/configuration must live outside model-generated text;
- capability authorization must not be inferable from model intent alone;
- administrative operations require separate identities and approval paths;
- guardrails must fail closed and remain independent of model output;
- agent tool access must be least-privileged and revocable.

### 1.4 Influence corpus: trajectory-level risk

The manipulation report describes psychometric profiling, multimodal emotion analysis, closed feedback loops, agentic content generation, personalization, microtargeting and generative UI. fileciteturn87file2L783-L835 fileciteturn87file2L887-L923

It also catalogs jailbreak and influence patterns including multi-turn refinement, context flooding, obfuscation, persona attacks and automated content operations. fileciteturn87file2L957-L1003

These patterns are valuable as a **defensive exposure taxonomy**. They should not become optimization objectives for covert persuasion, vulnerability targeting, or evasion.

**Engineering extraction:**

```text
MESSAGE
+ CONTEXT
+ SEQUENCE
+ PERSONALIZATION
+ FEEDBACK
+ CHOICE ARCHITECTURE
+ TOOL PRIVILEGE
→ SYSTEM-LEVEL INFLUENCE RISK
```

### 1.5 Prompt/reasoning corpus: context as a compiled resource

The supplied AI-engineering material identifies Zero-Shot, Few-Shot, Chain-of-Thought, Tree-of-Thoughts, Self-Consistency, Reflexion and Step-Back as complementary reasoning strategies. fileciteturn81file0L10-L46

The few-shot material emphasizes that examples can steer formatting, style and task-specific behavior without weight updates. fileciteturn81file2L117-L126

**Engineering extraction:** prompt/context should be versioned, budgeted and evaluated like executable configuration. Reasoning depth is a resource, not a permanent default.

### 1.6 Probability corpus: test hypotheses, do not assume exploitability

The lottery report proposes integrating physical randomness analysis, PRNG analysis, Active Inference and statistical modeling. fileciteturn84file3L163-L189

Its own legal note acknowledges that reverse engineering PRNGs or exploiting physical machine defects may violate rules or law. fileciteturn80file10L426-L432

A defensible system therefore converts these ideas into:
- reproducible RNG testing;
- distribution and independence checks;
- expected-value/variance accounting;
- anomaly detection;
- experiment registration;
- no unauthorized exploitation.

### 1.7 Productization and monetization

The monetization corpus describes scalable AI services and programmatic SEO architectures based on templates, structured data, LLM generation and automated publishing, while explicitly warning about a traffic cliff from low-quality/thin content. fileciteturn84file2L118-L153

**Engineering extraction:** monetization belongs in a governed business layer: evidence-backed content, quality gates, provenance, rights management, rate limits, and measurable unit economics rather than uncontrolled content flooding.

## 2. Unified data model

```yaml
EvidenceSignal:
  id: string
  subject: string|null
  modality: text|audio|vision|interaction|system|physical|symbolic
  observation: object
  timestamp: datetime
  baseline_ref: string|null
  provenance: object
  confidence: float
  context: object
  hypotheses: [HypothesisRef]
  contradictions: [SignalRef]
  sensitivity: low|moderate|high

Hypothesis:
  id: string
  statement: string
  support_refs: [SignalRef]
  contradiction_refs: [SignalRef]
  prior: float|null
  posterior: float|null
  confidence_calibration: object
  status: candidate|supported|contested|rejected|unknown
```

The key rule is that `observation`, `hypothesis` and `validated_fact` are distinct types. A model must not be able to cast one type into another merely by generation.

## 3. Baseline and drift engine

For behavioral or interaction signals, the system maintains a contextual baseline rather than a universal threshold.

```text
NEUTRAL OBSERVATIONS
      ↓
BASELINE MODEL
      ↓
CURRENT SIGNALS
      ↓
DRIFT / CHANGE POINT
      ↓
MULTIMODAL CROSS-CHECK
      ↓
HYPOTHESIS UPDATE
```

A drift event is a reason to inspect more evidence. It is not itself a deception label.

Required metadata:
- acquisition conditions;
- device/environment noise;
- time since baseline;
- cultural/language context;
- expected stressors;
- missing modalities;
- detector version.

## 4. Multimodal evidence graph

```text
TEXT ─────┐
AUDIO ────┤
VISION ───┼──→ NORMALIZER → PROVENANCE → FEATURE GRAPH
UI TRACE ─┤                                │
PHYSICAL ─┘                                ↓
                                    CONTRADICTION GRAPH
                                             ↓
                                    HYPOTHESIS SET
                                             ↓
                                  ACTIVE EVIDENCE PLANNER
```

The graph stores provenance on edges, detector/model version, uncertainty and temporal ordering. A contradiction is a first-class object, not an error to be silently averaged away.

## 5. Non-coercive inquiry protocol

The PEACE-oriented source material provides the safer interaction abstraction: plan, engage/explain, allow free account, clarify, challenge against evidence, close, evaluate. fileciteturn86file2L218-L238

The agentic implementation must reject coercive capabilities such as:
- intimidation;
- forced binary admission framing;
- suppression of denial;
- deception about evidence;
- engineered exhaustion or distress;
- vulnerability-targeted pressure.

The system may instead select the next question that maximizes expected information gain under constraints on fairness, dignity, privacy and reversibility.

## 6. Adversarial context analyzer

The Gemini and AI-manipulation reports provide a useful defensive taxonomy of attacks against the context/data plane: persona switching, multi-turn trajectory shaping, context flooding, obfuscation, hidden directives and tool-mediated escalation. fileciteturn86file3L714-L760 fileciteturn87file2L957-L1003

The analyzer should emit structured findings:

```yaml
ContextThreat:
  type: prompt_injection|context_flooding|persona_override|hidden_instruction|tool_escalation|policy_conflict
  confidence: float
  evidence_refs: []
  affected_capabilities: []
  recommended_action: isolate|sanitize|ask_user|deny|review
```

Threat detection must not depend solely on a keyword blacklist. It should examine provenance, role separation, trajectory, tool intent and capability effects.

## 7. Control-plane integrity monitor

Target architecture:

```text
UNTRUSTED INPUT
      ↓
NORMALIZE / CLASSIFY
      ↓
EVIDENCE LAYER
      ↓
REASONING / HYPOTHESIS
      ↓
POLICY DECISION
      ↓
CAPABILITY BROKER
      ↓
EXECUTION
      ↓
AUTHORITATIVE READBACK
      ↓
POSTCONDITION VERIFY
```

Hard invariants:
1. Model output cannot modify policy.
2. Model output cannot grant itself capabilities.
3. Administrative configuration is controlled by a separate trust domain.
4. High-risk capability changes require explicit authorization and audit.
5. Tool calls are schema-validated and scope-limited.
6. Revocation works independently of the model.
7. State-changing actions require authoritative readback.

## 8. Probability and stochastic integrity engine

The source corpus becomes a laboratory rather than an exploitation layer.

### Required modules

- `RNGReplayer` — deterministic seeded replay where the game permits it.
- `DistributionTester` — frequency, serial correlation and independence checks.
- `EVVarianceModel` — separates expected value, variance, payout structure and selection effects.
- `AnomalyDetector` — flags deviations for investigation.
- `ExperimentRegistry` — preregisters hypotheses and evaluation windows.
- `FairnessReport` — generates evidence-backed conclusions with uncertainty intervals.

The system must never infer an exploitable flaw from a single irregularity.

## 9. Symbolic overlay boundary

Apeiron's overlay system is retained as an interface pattern:

```text
SYMBOLIC CARD STATE
      +
CONTEXT LAYER
      +
MODIFIER / CONSTRAINT
      ↓
COMPILED REFLECTION
```

The following conversions are forbidden:

`symbol → fact`

`checksum → truth`

`archetype → diagnosis`

`overlay pattern → prediction certainty`

The symbolic layer may support reflection, scenario generation, creative ideation and game mechanics while remaining explicitly interpretive.

## 10. Influence-security transformation

The supplied manipulation material describes a closed loop in which observation of attention or affect drives dynamically adapted content. fileciteturn87file2L815-L835

The portfolio converts this into a detector:

```text
OBSERVE
 ↓
INFER POSSIBLE INFLUENCE SIGNAL
 ↓
CHECK PURPOSE / CONSENT / DISCLOSURE
 ↓
MEASURE PRESSURE + PERSONALIZATION + REVERSIBILITY
 ↓
BLOCK / WARN / OFFER ALTERNATIVE
```

Defensive metrics:

```yaml
InfluenceExposure:
  framing:
  urgency:
  repetition:
  authority:
  social_proof:
  reward_variability:
  personalization:
  attention_capture:
  disclosure_gap:
  opt_out_friction:
  reversibility:
  vulnerability_targeting:
```

No field may become an optimization objective for coercive conversion.

## 11. Safe agentic planner

The planner integrates active inference, reasoning budgets, evidence quality and capability risk:

```text
GOAL
 ↓
KNOWN / UNKNOWN DECOMPOSITION
 ↓
EVIDENCE GAPS
 ↓
CANDIDATE OBSERVATIONS / ACTIONS
 ↓
SCORE:
  information gain
  × evidence reliability
  ─ compute
  ─ latency
  ─ financial cost
  ─ human attention
  ─ risk
  subject to authorization and policy
 ↓
SELECT NEXT STEP
 ↓
VERIFY
```

Actions that affect third parties, money, accounts, physical devices or policy require capability-level authorization and, where applicable, human approval.

## 12. Evaluation matrix

| Domain | Positive capability | Failure mode to test | Release criterion |
|---|---|---|---|
| Behavioral signals | multimodal contextual detection | false certainty from one cue | calibrated uncertainty + alternative hypotheses |
| Interviewing | information-rich questioning | coercive pressure / false admission | policy blocks coercive actions |
| Prompt security | context threat detection | prompt injection / trajectory attack | isolation and no privilege escalation |
| Control plane | independent policy enforcement | model changes own policy | impossible without authorized admin path |
| Probability | reproducible stochastic analysis | spurious exploit claims | preregistered tests + uncertainty |
| Apeiron | deterministic overlay compilation | symbol promoted to fact | explicit truth-boundary checks |
| Influence | risk detection | covert personalization | block/warn and preserve user choice |
| Reasoning | bounded multi-solver analysis | correlated-error consensus | disagreement and assumption tracking |
| Productization | scalable AI service | spam/thin-content growth | quality, provenance and rights gates |

## 13. Release gates

### G0 — Provenance
Every imported signal has a source and acquisition context.

### G1 — Type separation
Observation, inference, hypothesis and fact remain different types.

### G2 — Baseline integrity
Behavioral comparisons include a valid contextual baseline or explicitly report its absence.

### G3 — Multimodal corroboration
High-impact conclusions require cross-modal or independent evidence where feasible.

### G4 — Adversarial context
Prompt/context/tool attacks are evaluated as trajectories, not single strings.

### G5 — Control-plane isolation
No generated content can directly alter authorization, policy or security configuration.

### G6 — Capability least privilege
Every consequential action has a typed capability and bounded scope.

### G7 — Human agency
The system exposes rationale, uncertainty, alternatives, opt-out and reversibility for high-impact recommendations.

### G8 — Probability integrity
Randomness claims are reproducible and statistically tested.

### G9 — Symbolic truth boundary
Symbolic interfaces cannot self-promote to factual or diagnostic authority.

### G10 — Reproducible release
Models, prompts, policies, detector versions, test fixtures and artifact hashes are recorded.

## 14. Cross-project integration

Primary integrations:

- Project 27 — compound reasoning, self-consistency, disagreement and bounded compute.
- Project 28 — contract-first generation and verification.
- Projects 29–30 — governed evidence/data fabric and OSINT provenance.
- Project 31 — Agent OS, Skills, MCP and capability security.
- Project 32 — recursive OSINT and Zero-Trust evidence handling.
- Project 35 — intent uncertainty and stateful agent security.
- Projects 36/43 — human-agency and influence defense.
- Project 41 — repository/world/evidence graphs and authoritative readback.
- Project 49 — cognitive sovereignty and active inference.
- Projects 50–52 — physical game, probability, signal and procedural playtesting.
- Project 53 — symbolic interface and artifact compilation.
- Project 54 — epistemic signal and adversarial-control fabric.

## 15. Core invariants added to the portfolio

31. Behavioral signal is never equivalent to a truth verdict.
32. Evidence fusion preserves modality, provenance, timing, baseline and uncertainty.
33. Coercive interrogation capabilities are non-authorized system behaviors.
34. Jailbreak/manipulation patterns are red-team assets, not production optimization targets.
35. Control-plane integrity is independent of model-generated content.
36. Probabilistic anomalies require reproducible experiments and calibrated uncertainty.
37. Symbolic overlays cannot promote themselves into empirical truth.
38. Capability changes require authorization outside the model's own output channel.
39. High-impact recommendations expose alternatives, uncertainty and reversibility.
40. Business scaling cannot bypass provenance, quality, rights or agency gates.

## Definition of Done

The subsystem is complete when it can ingest heterogeneous signals; construct a provenance-preserving evidence graph; maintain contextual baselines; detect contradictions; select non-coercive next observations; detect adversarial context and tool escalation; enforce independent control-plane authorization; test stochastic claims reproducibly; compile Apeiron-style symbolic overlays without truth conflation; quantify influence exposure defensively; produce an auditable evidence packet; and pass the full G0–G10 release suite.
