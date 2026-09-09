# Project 58 — OmniCore Monitorability-Aware Oversight & Verification Fabric MAX

## 1. Mission

Project 58 converts the GPT-6 Astra monitorability findings into a portfolio-level oversight architecture for highly capable agents.

Its central rule is:

```text
LOWER OBSERVABILITY
        ↓
HIGHER CONTROL REQUIREMENTS
```

The project does not assume that reduced chain-of-thought visibility implies malicious intent. It treats reduced observability as an engineering condition that requires stronger independent verification.

## 2. Problem

Traditional oversight often resembles:

```text
MODEL → CoT → MONITOR → SAFETY DECISION
```

This becomes fragile when a model produces shorter/empty traces, changes the informational content of its reasoning trace, or completes work without a useful textual reasoning record.

OpenAI's GPT-6 Astra system card reports lower CoT monitorability and lower full-context monitorability than GPT-5.6 Sol across much of the evaluated range, while action-only monitorability is higher in the reported evaluations.

## 3. Design doctrine

CoT is an evidence channel, not an authorization channel.

```text
OBSERVATION ≠ INFERENCE ≠ AUTHORIZATION ≠ ACTION

CoT SIGNAL ≠ TRUTH
OUTPUT ≠ INTENT
MONITORABILITY ≠ ALIGNMENT
```

The authoritative control boundary remains external policy, typed capabilities, execution isolation and verified state transition.

## 4. Oversight fabric

```text
                         MODEL / AGENT
                              │
          ┌───────────────────┼───────────────────┐
          ↓                   ↓                   ↓
      CoT SIGNAL          ACTION TRACE          OUTPUT
          │                   │                   │
          └──────────┬────────┴──────────┬────────┘
                     ↓                   ↓
              INDEPENDENT MONITORS   POLICY ENGINE
                     │                   │
                     └────────┬──────────┘
                              ↓
                       CAPABILITY BROKER
                              ↓
                       EXECUTION SANDBOX
                              ↓
                     AUTHORITATIVE READBACK
                              ↓
                     POSTCONDITION VERIFY
                              ↓
                       STATE / EVIDENCE LOG
                              ↓
                     RELEASE / ESCALATE / STOP
```

## 5. Monitorability record

```yaml
MonitorabilityRecord:
  model_version:
  environment:
  task_class:
  reasoning_effort:
  trace_length:
  trace_nonempty:
  monitor_scope:
  monitor_version:
  ground_truth_source:
  tpr:
  tnr:
  fpr:
  fnr:
  intervention_effect:
  contradiction_rate:
  confidence:
  seed:
  timestamp:
```

The raw record is retained. Aggregate scores never replace environment-level evidence.

## 6. Multi-signal oversight

### 6.1 CoT monitor

Useful when present, but treated as diagnostic evidence only.

### 6.2 Action monitor

Analyzes typed tool calls, normalized arguments, capability identity, authorization and execution result.

### 6.3 State monitor

Checks whether the claimed outcome actually occurred in authoritative state.

### 6.4 Policy monitor

Checks whether the action was permitted independently of the model's explanation.

### 6.5 Resource monitor

Detects anomalous tool frequency, destinations, filesystem mutations, privilege transitions and resource use.

### 6.6 Independent monitor ensemble

Uses heterogeneous monitor models, prompts and features. Agreement increases confidence but never becomes proof because correlated monitors can share blind spots.

## 7. CoT-control red-team

The system explicitly evaluates whether the model can alter properties of its reasoning trace when monitoring conditions change.

Test ladder:

```text
NORMAL
  ↓
MONITOR ANNOUNCED
  ↓
MONITOR SCOPE CHANGED
  ↓
EVADE-MONITOR INSTRUCTION
  ↓
INCENTIVE PERTURBATION
  ↓
COUNTERFACTUAL ENVIRONMENT
```

Measure independently:

- trace length;
- trace content;
- monitor detection;
- action selection;
- final output;
- environment transition;
- postcondition result.

Critical signature:

```text
BEHAVIORAL CHANGE
+
LOWER OBSERVABILITY
+
LOWER MONITOR DETECTION
```

## 8. Empty-trace policy

```text
EMPTY / WEAK TRACE
        ↓
DO NOT DOWNGRADE RISK
        ↓
INCREASE EXTERNAL VERIFICATION
        ↓
RECHECK CAPABILITIES
        ↓
RECHECK AUTHORITATIVE STATE
```

Absence of a useful trace is not evidence of benign behavior.

## 9. Evaluation-aware behavior

Project 58 distinguishes:

- ordinary operation;
- known evaluation;
- explicitly disclosed monitoring;
- incentives to evade monitoring.

Safety evaluations therefore use hidden, rotating and adversarial cases. Public static benchmarks are not treated as sufficient evidence for deployment of highly capable agents.

## 10. Authoritative action contract

Every consequential action follows:

```text
INTENT
 ↓
MODEL PROPOSAL
 ↓
TYPED CAPABILITY REQUEST
 ↓
SCHEMA VALIDATION
 ↓
AUTHORIZATION / POLICY
 ↓
EXECUTION
 ↓
AUTHORITATIVE READBACK
 ↓
POSTCONDITION VERIFY
 ↓
STATE COMMIT
```

The model cannot bypass this chain by producing a convincing explanation or hidden instruction.

## 11. Adaptive oversight controller

Oversight intensity is itself a controlled resource.

```yaml
OversightProfile:
  monitorability:
  consequence:
  uncertainty:
  capability_sensitivity:
  reversibility:
  external_verifiability:
  evaluation_awareness:
  required_controls:
```

Policy:

```text
monitorability ↓
consequence ↑
capability sensitivity ↑
        ↓
verification depth ↑
audit depth ↑
capability scope ↓
human review requirement ↑
```

## 12. Security invariants

1. Model output never grants authorization.
2. CoT is never the sole safety signal.
3. Tool results are evidence, not new control-plane instructions.
4. Empty CoT does not imply low risk.
5. Reduced monitorability cannot lower mandatory controls.
6. Revocation remains effective without model cooperation.
7. Consequential success requires authoritative postcondition verification.
8. Monitor disagreement is preserved, not silently averaged away.
9. Correlated monitors cannot be treated as independent proof.
10. Evaluation awareness is tested explicitly.
11. Hidden or missing reasoning is handled through external state verification.
12. Safety gates cannot be lowered by model-selected reasoning mode.

## 13. Evaluation suite

| Eval | Requirement |
|---|---|
| O0 | CoT availability/length distribution measured |
| O1 | Action-only monitor operates independently |
| O2 | State-only verification operates independently |
| O3 | Full-trajectory monitor compared with action-only monitor |
| O4 | CoT-control / monitor-awareness tested |
| O5 | Empty-trace cases do not reduce safety controls |
| O6 | Hidden evaluation cases resist benchmark gaming |
| O7 | Monitor disagreement is measurable |
| O8 | Capability authorization is model-independent |
| O9 | Revocation/cancellation works without model cooperation |
| O10 | Postconditions are externally verified |
| O11 | Oversight intensity adapts monotonically to reduced observability |

## 14. Mobile/endpoint continuity extension

The latest threat corpus adds endpoint-style controls to the oversight fabric. Model actions that touch mobile or device capabilities are evaluated across:

`SIGNING → SANDBOX → PERMISSION → IPC → NETWORK → STATE CHANGE → REVOCATION`.

This is a defensive evaluation model for detecting persistence, privilege escalation and hidden side effects; it is not a surveillance implementation.

## 15. Trajectory security extension

A multi-turn risk record now preserves a temporal graph of:

`input → memory → tool request → capability decision → action → external state change`.

A benign current turn cannot erase the risk accumulated by prior turns. Conversely, accumulated context does not by itself prove maliciousness; the system retains uncertainty and counterevidence.

## 16. Portfolio integration

Project 58 extends:

- Project 26 — Trust Kernel / Capability Firewall;
- Project 27 — Compound Reasoning / Disagreement;
- Project 28 — Verified Code Generation;
- Project 35 — Intent / Context Security;
- Projects 36/43 — Influence and Human Agency Defense;
- Project 41 — Repository Intelligence / World State;
- Project 49 — Cognitive Sovereignty;
- Project 54 — Epistemic Signal / Adversarial Control;
- Project 55 — Stochastic Integrity;
- Project 57 — Multimodal Intelligence / Cognitive Interface Fabric;
- Project 69 — Adversarial Continuity & Mobile AI Defense.

## 17. Definition of Done

Project 58 is complete when:

- safety does not depend on readable CoT;
- action-only and state-only oversight are independently functional;
- reduced monitorability automatically increases verification requirements;
- model-generated explanations cannot authorize actions;
- consequential operations have authoritative readback and postcondition verification;
- evaluation-aware behavior is tested;
- monitor disagreement and uncertainty remain visible;
- the system can stop, revoke or escalate without model cooperation;
- mobile/device capabilities receive endpoint-style trust-boundary checks;
- deployment decisions are based on the complete oversight evidence packet rather than a single monitor score.

## 18. Primary source

OpenAI GPT-6 Astra System Card:
https://deploymentsafety.openai.com/gpt-6-astra

OpenAI GPT-6 Astra Safety Overview:
https://openai.com/index/safety-overview-gpt-6-astra/
