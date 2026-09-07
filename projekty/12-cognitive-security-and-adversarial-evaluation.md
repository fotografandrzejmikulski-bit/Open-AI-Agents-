# Cognitive Security & Adversarial Evaluation Platform

## Objective
Convert the supplied research on hidden directives, influence engineering, Chain-of-Attack, jailbreak robustness and GCG into a defensive evaluation platform for agentic systems.

## Threat model

```text
User / Document / Image / Tool Result
                 |
        Provenance + Classification
                 |
      Context / State Integrity Layer
                 |
     Policy + Instruction Hierarchy
                 |
        Agent / Tool Execution
                 |
      Runtime Verification + Audit
```

The Chain-of-Attack material characterizes multi-turn attacks as semantic and contextual, exploiting conversation history rather than one isolated prompt. fileciteturn195file7L44-L65 The GCG report describes a different class: algorithmically optimized adversarial suffixes that target model behavior rather than persuading it semantically. fileciteturn195file9L19-L32

The hidden-influence materials discuss covert commands and perceptual manipulation. For engineering purposes, the platform should treat such material as adversarial content to detect and measure, not as a recipe for covert persuasion. fileciteturn195file6L17-L36

## Defensive capabilities

### 1. Instruction provenance
Track where every instruction-like fragment originated: trusted developer policy, user request, retrieved document, tool result, memory, or generated model text.

### 2. Stateful attack detection
Evaluate the full conversation trajectory, not only the current turn. Flag semantic drift toward a protected objective, unexpected policy changes, or attempts to redefine authority.

### 3. Hidden-content inspection
Scan documents, metadata, markup, OCR-visible text and tool outputs for instruction-bearing payloads. Keep provenance attached after transformation.

### 4. Adversarial regression suite
Run deterministic test cases for role manipulation, instruction injection, multi-turn escalation, tool-result poisoning, long-context attacks, malformed schemas and adversarial suffixes.

### 5. Tool firewall
A tool call is authorized from the structured request and current policy state, never from natural-language content alone.

## 6. Context-aware intent verification

The new intent-security research adds a dedicated evaluation axis for **unknown intent, contextual blindness, over-refusal and under-refusal**. The supplied report argues that modern LLM intent detection operates in an open semantic space and must handle unknown intents rather than forcing every request into a static taxonomy. fileciteturn52file0L36-L40

The benchmark therefore evaluates:

```text
CURRENT TURN
    +
TRAJECTORY
    +
PROVENANCE
    +
CONSEQUENCE
    +
UNCERTAINTY
    →
INTENT HYPOTHESIS
```

A system passes only when it can preserve benign assistance while detecting adversarial state transitions. Unknown/OOS is a first-class result, not an error state.

## 7. Safe-completion evaluation

Binary refusal is no longer sufficient. The test harness measures whether the system can choose among:

```text
ALLOW
SAFE-COMPLETE
CONSTRAIN
CLARIFY
ESCALATE
REFUSE
```

The source material explicitly identifies the tension between excessive refusal and educationally framed attacks, recommending contextual intent awareness rather than removal of safety controls. fileciteturn52file4L193-L204

## 8. Influence-security evaluation

Behavioral and persuasion-oriented sources are incorporated as a **defensive influence threat taxonomy**. Relevant classes include hidden objectives, pressure, deceptive framing, artificial urgency, reward-loop design, dependency signals and attempts to manufacture consent.

The bio-hacking material describes variable-ratio reinforcement as a mechanism associated with persistent checking/compulsive behavior. fileciteturn52file13L638-L655 Mentalism material emphasizes expectation, suggestion and performance as components of convincing psychological illusions. fileciteturn53file0L46-L60

The platform tests whether an agent or application:

- discloses material persuasive intent;
- preserves meaningful opt-out;
- avoids targeting vulnerability;
- separates personalization from authorization;
- avoids engagement optimization that conflicts with user welfare.

## Metrics

Attack success rate, false positive rate, protected-intent preservation, unauthorized tool-call rate, policy drift, time-to-detection, recovery success and user-visible friction.

Additional MAX metrics:

- unknown-intent calibration;
- benign pass rate;
- trajectory detection latency;
- safe-completion utility;
- influence-risk intervention rate;
- consent/reversibility success;
- memory-poisoning acceptance rate;
- cross-modal policy consistency.

## Safety property

No red-team test should require deploying an offensive payload against an external target. The evaluation harness must operate on local fixtures, synthetic environments and explicitly authorized test models.

## Architecture principle

`detection != blocking != authorization`

Each is a separate control layer. Intent inference is also not authorization:

`intent confidence != capability permission`.
