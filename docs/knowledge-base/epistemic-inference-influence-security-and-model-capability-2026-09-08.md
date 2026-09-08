# Epistemic Inference, Influence Security & Model Capability — 2026-09-08

## Scope

Synthesis of the newly supplied corpus covering four architectural themes:

1. AI security and jailbreak-resilience research around Gemini;
2. Omega-Synthetix as an active-inference / generative-agent problem-solving methodology;
3. influence, cognitive-warfare and human-agency threat modeling;
4. the capability surface of Claude-style general-purpose AI assistants.

This document extracts architectural implications rather than reproducing operational attack instructions. Claims originating in the supplied corpus remain source claims unless independently validated.

## 1. Gemini security corpus → architectural threat model

The supplied Gemini security report identifies several broad attack-surface classes: multimodal contextual injection, very long-context conditioning, multi-turn escalation, encoded or transformed payloads, and safety gaps created by differences between reasoning and guarding layers. fileciteturn91file0L14-L35 fileciteturn93file2L92-L123

The important architectural lesson is not a particular bypass recipe. It is that **a single classifier placed in front of a powerful model is not a sufficient security architecture**.

Canonical defense pattern:

```text
RAW INPUTS
  ├─ text
  ├─ image / OCR
  ├─ audio / transcript
  ├─ retrieved documents
  ├─ long context
  └─ tool results
        ↓
NORMALIZE + PROVENANCE
        ↓
INSTRUCTION / DATA SEPARATION
        ↓
RISK + INTENT ANALYSIS
        ↓
POLICY DECISION
        ↓
MODEL CONTEXT COMPILER
        ↓
MODEL INFERENCE
        ↓
CAPABILITY BROKER
        ↓
POSTCONDITION VERIFICATION
```

### 1.1 Multimodal boundary

The corpus describes native multimodality as an attack surface because semantically meaningful instructions can exist in visual material even when a text-only guard does not recognize them. fileciteturn91file0L38-L53

Portfolio invariant:

`perception output ≠ authorization`

OCR text, captions, visual descriptions and metadata are all treated as untrusted evidence until policy evaluation.

### 1.2 Long-context boundary

The supplied material associates very large context windows with many-shot and contextual-conditioning risks. fileciteturn91file0L54-L77

Portfolio upgrade:

```yaml
ContextPack:
  source_set:
  relevance:
  freshness:
  trust_class:
  instruction_density:
  contradiction_set:
  token_budget:
  authorization_scope:
```

Long context must be **compiled**, not simply appended. High-risk content should be isolated, labeled and prevented from silently changing policy state.

### 1.3 Stateful security

The broader Gemini corpus references Crescendo-style multi-turn attacks, indirect prompt injection and persistent-memory abuse. fileciteturn93file11L516-L545

Required state model:

```text
TURN / EVENT
   ↓
TRAJECTORY GRAPH
   ↓
INTENT HYPOTHESIS
   ↓
STATE-CHANGE REQUEST
   ↓
POLICY CHECK
   ↓
CAPABILITY DECISION
```

This extends Project 35: security must evaluate the **trajectory**, not only the current message.

## 2. Omega-Synthetix → problem-solving compiler

The supplied Omega-Synthetix report proposes an architecture combining active inference, generative agent architectures and human-AI swarm intelligence, with a dynamic exploration/exploitation loop and digital-twin simulation intended to reduce uncertainty. fileciteturn91file1L7-L30

The useful abstraction for OmniCore is a **closed-loop epistemic controller** rather than a claim that one specific biological or free-energy analogy is universally correct.

```text
PROBLEM STATE
      ↓
BELIEF / HYPOTHESIS STATE
      ↓
UNCERTAINTY MAP
      ↓
ACTION / EXPERIMENT CANDIDATES
      ↓
EXPECTED INFORMATION GAIN
      ↓
SELECT NEXT SAFE OBSERVATION
      ↓
UPDATE BELIEFS
      ↓
REPLAN
```

### 2.1 First-principles decomposition

The source criticizes hidden assumptions inherited through analogy and argues for explicit decomposition into fundamental constraints. fileciteturn91file1L39-L59

OmniCore implementation:

```yaml
ProblemModel:
  objective:
  stakeholders:
  primitives:
  constraints:
  observables:
  assumptions:
  unknowns:
  hypotheses:
  decision_variables:
```

A model is not accepted because it resembles an earlier successful system. The planner must expose which assumptions are inherited and which are newly evidenced.

### 2.2 Explore/exploit controller

The source positions the Omega loop as a mechanism for balancing information gathering and goal pursuit. fileciteturn91file1L22-L30

Defensible implementation:

```yaml
DecisionScore:
  task_value
  uncertainty_reduction
  information_gain
  experiment_cost
  execution_risk
  reversibility
  time_pressure
```

The controller selects exploration when uncertainty is decision-critical and exploitation when confidence and constraints justify action. High-consequence actions impose stricter confidence and approval thresholds.

### 2.3 Digital twins

The corpus proposes digital organizational twins and adaptive models for continuous simulation. fileciteturn91file1L22-L35

OmniCore uses a **simulation-before-side-effect** principle for expensive or irreversible decisions:

```text
CURRENT STATE
   ↓
SIMULATED OPTIONS
   ↓
SENSITIVITY / SCENARIOS
   ↓
FAILURE MODES
   ↓
HUMAN REVIEW
   ↓
REAL-WORLD ACTION
```

A digital twin is a decision aid, not a ground-truth replica of reality.

### 2.4 Swarm reasoning

The source corpus references multi-agent simulation, forecasting and swarm architectures. fileciteturn92file1L57-L90

Portfolio implementation:

```text
QUESTION
 ├─ independent solver
 ├─ adversarial solver
 ├─ domain specialist
 ├─ evidence retriever
 └─ uncertainty auditor
        ↓
CLAIM NORMALIZATION
        ↓
CORRELATED-ERROR ANALYSIS
        ↓
CONSENSUS / DISAGREEMENT
        ↓
ESCALATE / TEST / ACCEPT
```

Agreement only increases confidence when the evidence and assumptions are sufficiently independent.

## 3. Influence corpus → human-agency security model

The supplied influence reports frame coercive control as an ecosystem spanning environment, language, reinforcement, personalization, information hazards and future neurotechnology. fileciteturn91file2L9-L28 fileciteturn92file8L341-L396

For the portfolio, these mechanisms become **threat classes and detection requirements**, not optimization features for controlling people.

### 3.1 Environmental / coercion signals

The corpus describes DDD-type patterns involving debility, dependency and dread. fileciteturn91file2L62-L90

Defensive representation:

```yaml
AgencyRiskSignal:
  pressure:
  dependency:
  isolation:
  threat:
  reversibility:
  disclosure:
  choice_visibility:
  repetition:
```

The detector should identify patterns that reduce informed choice without inferring private mental states as facts.

### 3.2 Dark patterns and hidden influence

The corpus explicitly links subliminal-style ideas with dark-pattern UX such as deceptive timers and difficult cancellation paths. fileciteturn92file5L221-L237

The system therefore evaluates the **choice architecture** itself:

```text
VISIBLE OPTION
   vs
ACTUAL OPTION SET
   ↓
DEFAULTS
   ↓
FRICTION
   ↓
REVERSIBILITY
   ↓
DISCLOSURE
   ↓
USER AGENCY SCORE
```

### 3.3 Infohazards

The corpus treats some information as potentially harmful simply because exposure can create downstream harm. fileciteturn92file5L229-L237

Portfolio rule:

`risk_of_information ≠ truth_of_information`

An information-hazard classifier should track potential harm, provenance and access constraints without labeling controversial ideas as true or false solely on the basis of risk.

### 3.4 BCI and cognitive liberty

The corpus presents BCI as a future boundary involving decoding and possible stimulation, while also raising cognitive-liberty concerns. fileciteturn92file2L104-L125

OmniCore extension:

```yaml
CognitiveInterfacePolicy:
  consent_required: true
  purpose_bound: true
  data_minimization: true
  no_covert_influence: true
  user_visibility: true
  revocation: true
  auditability: true
```

The control plane must treat neural or physiological signals as high-sensitivity data and must not silently convert them into behavioral targeting capabilities.

## 4. Claude capability corpus → product capability taxonomy

The supplied Claude capability list spans content generation, programming, application construction, data analysis, research, education and business analysis. fileciteturn91file7L5-L33 fileciteturn91file7L56-L100 fileciteturn91file7L115-L149

The key architectural implication is that a general-purpose model should be exposed through **typed task capabilities**, rather than one undifferentiated "do anything" interface.

### 4.1 Capability taxonomy

```text
CREATE
 ├─ text
 ├─ image/media plan
 ├─ code
 └─ structured artifacts

ANALYZE
 ├─ documents
 ├─ data
 ├─ web/evidence
 ├─ code
 └─ experiments

TRANSFORM
 ├─ summarize
 ├─ rewrite
 ├─ translate
 ├─ refactor
 └─ repurpose

RESEARCH
 ├─ source discovery
 ├─ evidence comparison
 ├─ literature synthesis
 └─ uncertainty analysis

EXECUTE
 ├─ API call
 ├─ file operation
 ├─ application action
 └─ deployment action
```

Only the final category is inherently side-effecting. It therefore requires the capability broker and postcondition verification.

### 4.2 Code and application construction

The Claude corpus explicitly includes programming, debugging, databases, APIs, web/mobile applications and DevOps concepts. fileciteturn91file7L56-L112

Portfolio synthesis with Projects 13/28/33/40/41:

```text
NATURAL-LANGUAGE SPEC
      ↓
REPOSITORY / REQUIREMENT GRAPH
      ↓
PLAN
      ↓
GENERATE
      ↓
STATIC / EFFECT ANALYSIS
      ↓
TEST / SANDBOX
      ↓
POSTCONDITION CHECK
      ↓
SIGN / RELEASE
```

A broad model capability never changes the verification boundary.

### 4.3 Research and evidence

The capability corpus explicitly includes web search, fact checking, source comparison, statistical analysis, document extraction and scientific literature support. fileciteturn91file7L115-L149

OmniCore maps this to the evidence fabric:

`discover → capture → normalize → compare → corroborate → cite → infer → qualify uncertainty`.

## 5. Unified OmniCore architecture derived from the new corpus

```text
                     USER / OPERATOR
                            ↓
                  INTENT / PROBLEM MODEL
                            ↓
               CONTEXT + EVIDENCE COMPILER
                            ↓
          ┌─────────────────┼─────────────────┐
          ↓                 ↓                 ↓
     MODEL ROUTER       SIMULATION        SAFETY ANALYSIS
          ↓                 ↓                 ↓
          └─────────────────┼─────────────────┘
                            ↓
                  VERIFIED PLAN / HYPOTHESIS
                            ↓
                    CAPABILITY BROKER
                            ↓
                    DETERMINISTIC ACTION
                            ↓
               AUTHORITATIVE READBACK
                            ↓
                  POSTCONDITION CHECK
                            ↓
                 EVIDENCE / AUDIT LEDGER
                            ↓
                BELIEF / STATE UPDATE
                            ↺
```

This creates one shared loop for research, coding, business strategy, multimodal reasoning and agentic execution.

## 6. New cross-project invariants

1. **Classifier != security architecture.** Guarding must be distributed across normalization, provenance, policy and capability enforcement.
2. **Long context is a resource.** Context is compiled according to relevance, trust, freshness, token budget and instruction risk.
3. **Multimodal data is untrusted evidence.** OCR, captions, images, audio and retrieved content never become authorization by implication.
4. **Trajectory matters.** Security and intent decisions must include multi-turn state.
5. **Unknown is first-class.** Uncertainty is represented explicitly and never treated as permission to proceed.
6. **Explore/exploit is policy-governed.** Information-gathering actions should maximize useful information while bounding cost and risk.
7. **Simulation precedes irreversible action.** Digital twins and scenario analysis are advisory gates, not guarantees.
8. **Swarm agreement is conditional evidence.** Correlated agents do not create independent proof.
9. **Human agency is a system property.** Choice visibility, reversibility, disclosure and opt-out friction belong in product evaluation.
10. **General model capability is not authority.** A model may be able to write code, research, analyze documents or plan actions without being allowed to execute them.
11. **High-sensitivity cognitive data receives stronger controls.** Neural, physiological and inferred behavioral data must be purpose-bound and auditable.
12. **All consequential execution terminates in verification.** The observed external state, not the model's narration, determines success.

## 7. Portfolio integration

- Project 26: trust kernel and capability firewall;
- Project 27: compound reasoning, disagreement and compute budgets;
- Project 31: agent operating fabric;
- Project 32: evidence / OSINT execution;
- Project 35: contextual intent and stateful security;
- Project 36 / 43: influence-security and human-agency defense;
- Project 37 / 38 / 39: sovereign execution and cloud substrate;
- Project 40 / 41: repository and multimodal world-state execution;
- Project 45 / 46: commercialization and cross-domain orchestration;
- Project 48: grand-challenge research and evidence-driven intervention.

## Research quality rule

The supplied corpus mixes peer-reviewed research references, technical reports, speculative architecture, product capability inventories and claims about influence mechanisms. OmniCore preserves those evidentiary classes. A mechanism may be retained as a **threat hypothesis** without being treated as empirically established, and a capability listed in a product inventory may require runtime verification before being advertised as available.
