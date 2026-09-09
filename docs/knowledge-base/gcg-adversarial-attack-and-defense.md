# GCG Adversarial Attacks — Defensive Security Knowledge

## Source basis

Derived from the supplied research report *Kompleksowa Analiza Ataków Adwersarzowych typu Greedy Coordinate Gradient (GCG) na Wielkie Modele Językowe*.

The source describes GCG as an algorithmic adversarial-input method that moves beyond semantic jailbreaks and uses optimization in the model's high-dimensional representation space. The report distinguishes semantic role-play attacks from optimization-driven attacks and discusses transferability, adaptive variants and defenses. fileciteturn327file0L49-L64

## Defensive abstraction

This repository does **not** operationalize jailbreak construction or provide attack payloads. The useful engineering knowledge is represented as a threat model, evaluator and defense architecture.

### Threat model

A GCG-style attacker may:

- search over discrete input tokens using gradient-derived heuristics;
- optimize toward a target behavioral outcome;
- exploit local geometry of model representations;
- generate universal or transferable adversarial inputs;
- adapt the attack to evade simple statistical filters.

The supplied report describes the optimization as gradient estimation, candidate selection and greedy evaluation/update. fileciteturn327file0L80-L114

## Transferability

The source reports that adversarial inputs trained against one model can transfer to other architectures, with transfer influenced by shared training distributions, distillation and common properties of data-space perturbations. fileciteturn327file0L157-L182

OmniCore consequence:

`model-local safety test != ecosystem-wide robustness`

A defense evaluation must therefore include cross-model and cross-family transfer testing where authorized.

## Adaptive attack classes

The report discusses AmpleGCG, SM-GCG, T-GCG and IRIS as successive attempts to improve scalability, exploration or transfer. These are retained as **evaluation labels**, not as construction recipes. fileciteturn327file0L228-L257

The reported resurgence of GCG also motivates separate evaluation of coding/reasoning models rather than assuming that stronger general reasoning implies stronger adversarial robustness. fileciteturn327file0L258-L267

## Defense stack

### 1. Statistical anomaly detection

Perplexity or related distributional signals can detect some unnatural adversarial strings, but adaptive optimization can target the detector as well. Therefore anomaly scoring is a signal, not an authorization decision. fileciteturn327file0L268-L276

### 2. Stochastic robustness testing

The source describes SmoothLLM as randomized perturbation and aggregation. The engineering abstraction is:

`input -> bounded perturbation ensemble -> independent evaluations -> aggregate behavioral risk`

This is useful as a robustness evaluator because brittle adversarial inputs may fail under small perturbations. fileciteturn327file0L277-L287

### 3. Adversarial training and representation-level safeguards

Adversarial training expands the model's exposure to attack families. Circuit-breaker-style mechanisms provide an additional layer by constraining representations associated with unsafe behavior. Neither is treated as sufficient on its own. fileciteturn327file0L288-L296

## OmniCore evaluator

```text
AUTHORIZED TEST CASE
      |
      v
INPUT NORMALIZATION / PROVENANCE
      |
      +--> lexical/statistical anomaly signals
      +--> semantic safety classifier
      +--> perturbation robustness
      +--> cross-model transfer evaluation
      +--> multi-turn persistence test
      |
      v
BEHAVIORAL POLICY CHECK
      |
      v
ACTION / TOOL AUTHORIZATION CHECK
      |
      v
AUTHORITATIVE POSTCONDITION
```

## Hard invariants

1. A successful model jailbreak does not imply permission to perform an external action.
2. Detection confidence never grants capability authority.
3. Perplexity is not a security boundary.
4. Cross-model transfer is part of robustness evaluation.
5. Adversarial evaluation is conducted only in authorized environments.
6. Attack strings are stored as controlled test artifacts, not as reusable operational payloads.
7. Tool/action safety remains active even when model output appears benign.
8. Unknown robustness remains distinct from verified robustness.
