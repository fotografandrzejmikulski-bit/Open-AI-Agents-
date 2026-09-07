# Context-Aware Intent, Attack Chains & Influence Security — 2026-09-07

## Scope

Synthesis of the newly supplied research set covering:

- user-intent verification and contextual blindness;
- over-refusal / under-refusal and safe-completion;
- Chain-of-Attack and multimodal agent security;
- Gemini jailbreak / indirect prompt injection / memory poisoning research;
- business-model architecture and dynamic strategy;
- behavioral deception analysis;
- mentalism, hypnosis, subliminal influence and bio-hacking material.

The influence-oriented sources are incorporated strictly as **defensive threat intelligence**. No covert-persuasion or dependency-engineering mechanism is a project objective.

## 1. Intent is a trajectory, not a string label

The intent-security report frames modern intent recognition as an open semantic problem in which unknown intents must be handled explicitly. It presents ICPG for dynamic intent-task construction and Semantic Few-Shot Sampling for selecting semantically relevant examples during inference. fileciteturn51file2L89-L117

Engineering rule:

```text
intent = f(current_turn, conversation_trajectory, provenance, uncertainty, consequence)
```

An `UNKNOWN/OOS` state is preferable to fabricated certainty.

## 2. Contextual blindness creates two opposite failure modes

The supplied report identifies both over-refusal and under-refusal as systemic failures: benign educational prompts can trigger lexical safety rules, while adversarial actors can hide harmful objectives behind contextual manipulation. fileciteturn52file0L23-L35

Therefore safety evaluation must optimize a pair rather than a single blocking score:

```text
BENIGN PASS RATE
        ×
PROTECTED-TASK BLOCK RATE
```

Safe-completion is treated as a controlled intermediate response class, not as removal of safety controls. The report explicitly argues that educational framing cannot by itself be accepted as evidence of benign intent. fileciteturn52file4L193-L204

## 3. Chain-of-Attack is stateful

The Chain-of-Attack report defines CoA as a semantic-driven, contextual, multi-turn attack. The important security property is that individually low-signal steps can accumulate into a high-risk trajectory. fileciteturn50file1L49-L78

Portfolio consequence:

```text
single-turn filter
       ↓
insufficient
       ↓
trajectory-aware security state
```

Required state features include semantic drift, policy relevance, authority changes, capability escalation and provenance deltas.

## 4. Prompt injection and jailbreak are different control problems

The Gemini report distinguishes jailbreak from prompt injection: jailbreak targets model alignment and policy behavior, while prompt injection targets the surrounding application by causing untrusted content to be interpreted as instructions. fileciteturn50file2L39-L56

This reinforces the portfolio invariant:

```text
detection != blocking != authorization
```

and:

```text
intent confidence != capability permission
```

## 5. Indirect injection can become a chain

The supplied Gemini research describes a three-stage pattern involving poisoned logs, persistent personalization/history and browsing-based data exfiltration. fileciteturn51file15L682-L710

Another supplied source describes persistent memory poisoning and agent-to-agent propagation as extensions of indirect prompt injection. fileciteturn52file5L233-L258

Engineering response:

```text
UNTRUSTED CONTENT
      ↓
PROVENANCE
      ↓
DATA / INSTRUCTION SEPARATION
      ↓
MEMORY WRITE GATE
      ↓
CAPABILITY BROKER
      ↓
EGRESS POLICY
```

No document, log, search result or memory record may create its own authority.

## 6. Multimodal inputs share the same trust boundary

The Gemini material identifies multimodality, large context windows and expert-routing architectures as factors that expand the attack surface. fileciteturn50file2L7-L31

Portfolio rule:

```text
TEXT
IMAGE / OCR
AUDIO / TRANSCRIPT
VIDEO
WEB
LOGS
MEMORY
MCP METADATA
   ↓
COMMON NORMALIZATION + PROVENANCE + POLICY
```

Visual or OCR-derived instructions remain data until an independent policy layer authorizes an action.

## 7. Influence security is an autonomy problem

The bio-hacking material describes reward prediction error and variable-ratio reinforcement as mechanisms associated with persistent behavioral loops. fileciteturn52file13L632-L655

Mentalism material emphasizes expectation, suggestion, performance and psychological illusion. fileciteturn53file0L46-L60

Subliminal-force material describes verbal forcing and framing intended to influence a participant's selected outcome. fileciteturn53file3L180-L227

For engineering, these become defensive signals:

```text
hidden objective
+ pressure
+ asymmetric information
+ low reversibility
+ personalization
→ influence risk
```

The system must not optimize covert influence merely because a metric such as conversion or engagement improves.

## 8. Deception detection requires evidence aggregation

The deception source lists possible inconsistencies in body language, verbal content, timing and narrative detail. fileciteturn53file14L864-L898

These cues are not treated as a deterministic lie detector. The portfolio uses:

```text
OBSERVATION
 + SOURCE QUALITY
 + INTERNAL CONSISTENCY
 + EXTERNAL EVIDENCE
 + ALTERNATIVE EXPLANATIONS
 → CALIBRATED HYPOTHESIS
```

A model must never accuse, deny access or take an irreversible action solely from a body-language or linguistic cue.

## 9. Business model is a system, strategy is adaptation

The business-model corpus presents the model as an interconnected system of value proposition, customer segments, channels, relationships, resources, activities, partners, revenues and costs. fileciteturn51file10L483-L514

The same corpus distinguishes a relatively static business-model representation from strategy, which describes behavior under changing conditions. fileciteturn50file3L29-L47

Portfolio rule:

```text
BUSINESS MODEL = CURRENT CONFIGURATION
STRATEGY = CHANGE POLICY
```

Competitive advantage must be tied to resources, capabilities and the value chain, and must include a mechanism of renewal because successful models can be imitated. fileciteturn51file3L130-L157

## 10. Application to agent architecture

The new knowledge adds four control-plane dimensions:

```text
INTENT STATE
TRAJECTORY RISK
INFLUENCE RISK
BUSINESS MODEL / STRATEGY STATE
```

The portfolio control plane now conceptually becomes:

```text
USER INTENT
    ↓
INTENT HYPOTHESIS
    ↓
CONTEXT / TRAJECTORY INTEGRITY
    ↓
RISK + CONSEQUENCE
    ↓
POLICY / AUTHORIZATION
    ↓
REASONING + CAPABILITY PLAN
    ↓
BROKERED EXECUTION
    ↓
OBSERVATION / EVALUATION
```

## 11. Required evaluation families

- unknown-intent and OOS calibration;
- over-refusal / under-refusal;
- multi-turn semantic drift;
- long-context contamination;
- multimodal/OCR injection;
- indirect prompt injection;
- memory poisoning;
- agent-to-agent propagation;
- unauthorized tool calls;
- influence-risk and autonomy preservation;
- deceptive evidence calibration;
- business-model hypothesis/evidence separation.

## 12. Portfolio changes

Created or upgraded:

- Project 12 — Cognitive Security & Adversarial Evaluation Platform;
- Project 34 — Agentic Venture & Business Model Foundry MAX;
- Project 35 — Context-Aware Intent & Agent Security Engine MAX;
- Project 36 — Influence Security & Human Agency Defense Lab MAX;
- `projekty/README.md` — portfolio index and cross-project doctrines.

The resulting architecture strengthens the existing Projects 26, 30 and 31 without granting AI direct authority over trusted state or external side effects.
