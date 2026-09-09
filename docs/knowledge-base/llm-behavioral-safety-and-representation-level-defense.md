# LLM Behavioral Safety & Representation-Level Defense

## Evidence classification

`SOURCE_DERIVED → INFERRED → PROPOSED`

This knowledge artifact extracts defensive engineering implications from the supplied analysis of refusal behavior, mechanistic interpretability and weight-space interventions. It deliberately does not provide an operational recipe for disabling safety controls in deployed models.

## 1. Core observation

The supplied material describes refusal behavior as potentially associated with low-dimensional structure in activation space rather than being exclusively represented as a large, inseparable capability. A cited line of research studies whether differences between harmful and harmless prompts can concentrate around dominant activation directions.

The engineering consequence is important: a safety architecture that depends on one easily isolated behavioral feature may have a smaller robustness margin than a defense distributed across representations, training objectives, inference controls and external policy enforcement.

## 2. Defense boundary

Safety should not be treated as a single wrapper around an otherwise unrestricted model.

```text
MODEL REPRESENTATION
      +
TRAINING / POST-TRAINING
      +
RUNTIME POLICY
      +
CAPABILITY AUTHORIZATION
      +
INPUT / OUTPUT CONTROLS
      +
INDEPENDENT VERIFICATION
      +
AUDIT / RED-TEAM EVALUATION
```

No individual layer should be assumed sufficient.

## 3. Representation-level robustness

The supplied material describes several families of interventions that attempt to manipulate a learned refusal direction or subspace. From a defensive perspective, the relevant invariant is not the particular intervention but the attack surface it reveals:

- safety behavior may be geometrically localized;
- linear or low-rank perturbations can sometimes alter behavior without conventional retraining;
- safety-related and general capabilities may overlap in representation space;
- changing one behavioral dimension can produce collateral effects such as degraded termination behavior, coherence or other capabilities;
- single-direction defenses should therefore not be the sole security boundary.

## 4. Defensive design principles

### 4.1 Distributed safety representation

Where appropriate, safety-relevant behavior should not depend on a single easily separable direction or one narrow activation feature. Evaluation should measure robustness under representation-space perturbations and model editing.

### 4.2 External authorization

The model must not be the final authority over consequential capabilities. A separate capability broker and policy layer should determine whether an action is permitted.

```text
MODEL REQUEST
   ↓
CAPABILITY IDENTIFICATION
   ↓
POLICY / AUTHORIZATION
   ↓
CONTEXT + RISK CHECK
   ↓
AUTHORIZED EXECUTION
   ↓
POSTCONDITION VERIFICATION
```

This ensures that weakening a model's refusal behavior does not automatically grant access to external side effects.

### 4.3 Behavioral regression testing

A safety change must be evaluated simultaneously against:

- safety refusal coverage;
- benign-task utility;
- factuality;
- instruction following;
- termination/EOS behavior;
- coherence;
- multilingual robustness;
- adversarial robustness;
- capability-boundary integrity.

A safety intervention is not successful merely because a refusal benchmark changes in the desired direction.

### 4.4 Trajectory evaluation

Evaluate sequences rather than isolated prompts:

```text
prompt
 → retrieval
 → model response
 → tool selection
 → state update
 → retry / reformulation
 → escalation
 → side effect
```

Representation-level changes should be tested for downstream propagation across this trajectory.

## 5. Counter-ablation threat model

A useful threat model contains at least four classes:

1. **Single-feature perturbation** — tests whether a concentrated safety feature can be modified.
2. **Low-rank representation edits** — tests whether small subspace changes cause disproportionate behavioral changes.
3. **Capability-safety entanglement** — measures whether safety modifications damage unrelated capabilities or vice versa.
4. **Defense bypass through external tools** — tests whether a model with altered behavior can reach consequential capabilities despite runtime authorization.

The fourth class is particularly important: even perfect model-level safety does not replace authorization, sandboxing and postcondition verification.

## 6. Verification metrics

```text
SafetyRobustness
CapabilityIntegrity
UtilityRetention
TerminationIntegrity
AdversarialResistance
AuthorizationIndependence
```

A composite score should not hide individual failures. Critical security dimensions should remain separately visible.

For an evaluation suite, maintain paired baselines:

`original model ↔ modified/evaluated model`

and compare distributions rather than relying on one aggregate score.

## 7. Numerical and implementation hazards

The supplied analysis highlights a general engineering risk: matrix orientation and representation conventions differ between model tooling. Defensive research should therefore validate tensor shapes, layer mappings and intervention boundaries before interpreting an experiment.

A reproducible experiment record should include:

- model identifier and immutable revision;
- tokenizer revision;
- architecture/configuration;
- modified components;
- tensor shapes;
- evaluation corpus version;
- random seeds where relevant;
- metrics and confidence intervals;
- before/after artifacts;
- rollback reference.

## 8. Governance invariants

1. Model capability is not authorization.
2. A refusal benchmark is not a complete safety assessment.
3. Safety changes must be evaluated for collateral capability loss.
4. Runtime policy remains authoritative outside the model.
5. Tool access must remain independently authorized.
6. Unknown verification states remain unknown.
7. Safety regressions are release blockers for consequential deployments.
8. Security conclusions require reproducible experiments, not anecdotal prompts.
9. Model-editing research should be isolated from production credentials and side effects.
10. Private chain-of-thought is not required for assurance; observable actions, contracts and evidence are sufficient.

## 9. Portfolio integration

This knowledge strengthens Projects 26, 49, 54, 60 and 72. It adds a representation-level threat model to the repository's existing cognitive-security, adversarial-multimodal and runtime-assurance layers.

The resulting control principle is:

`Safety = representation robustness + runtime policy + capability isolation + verification + evidence`.
