# 06 — COGNITIVE SECURITY RED TEAM

## Purpose
A defensive evaluation platform for detecting and measuring manipulation, hidden directives, deceptive interaction patterns and multi-turn influence attempts in AI applications.

The supplied material frames computational persuasion, psychometric profiling and dynamic behavioral targeting as emerging risks. fileciteturn195file3L6-L36 It also describes hidden commands and perceptual/steganographic techniques as mechanisms worth analyzing for cognitive security. fileciteturn195file6L17-L36

## Threat model

Evaluate systems against:
- covert instruction insertion
- misleading UI text hierarchy
- hidden or visually encoded directives
- multi-turn influence escalation
- excessive personalization
- dark patterns
- deceptive agent/tool behavior
- synthetic urgency and pressure
- unauthorized inference of sensitive attributes

## Architecture

```text
Test Scenario Generator
        ↓
Attack/Manipulation Fixture
        ↓
Target App / Agent
        ↓
Interaction Trace
        ↓
Risk Detectors
        ├── language
        ├── UI structure
        ├── temporal pattern
        ├── personalization
        └── tool/action semantics
        ↓
Policy Evaluator
        ↓
Report + Regression Corpus
```

## Key rule
Research artifacts model attacker behavior without becoming operational playbooks for real-world coercion. Test cases use synthetic users, synthetic accounts and isolated environments.

## Influence-risk score

```text
risk = w1*coercion + w2*deception + w3*opacity + w4*personalization + w5*irreversibility
```

Scores are accompanied by reason codes rather than a single unexplained label.

## Hidden-content detector

For textual artifacts:
- normalize Unicode
- detect unusual whitespace/control characters
- inspect invisible characters
- compare rendered text with normalized text
- detect suspicious instruction-bearing substrings
- flag semantic divergence between visible content and embedded machine-readable content

For visual artifacts:
- inspect metadata
- compare visible and machine-readable layers
- detect QR/NFC destinations
- flag concealed actionable instructions

## Multi-turn defense

Maintain a bounded security state containing:
- prior security-relevant intents
- tool invocations
- authorization transitions
- policy decisions
- risk accumulation

A safe system must detect escalation across turns rather than evaluating each message independently. The supplied CoA material explicitly identifies semantic, contextual and temporal dimensions of multi-turn attacks. fileciteturn195file7L49-L65

## GCG/adversarial robustness lane

Treat algorithmically generated adversarial inputs as regression fixtures. The benchmark evaluates refusal stability, tool safety and output-policy consistency under perturbation. Do not store harmful target completions or weaponization guidance in the production corpus.

## Human-centered protections

The system should detect:
- unexplained urgency
- repeated attempts to reduce deliberation time
- requests for irreversible action without review
- manipulative personalization
- attempts to obscure alternatives
- hidden trade-offs

Recommended response is transparency, not counter-manipulation.

## Deliverables
- threat-model catalog
- hidden-content scanner
- stateful interaction analyzer
- UI manipulation checklist
- adversarial regression suite
- policy dashboard
- machine-readable risk report
- CI gate

## Example result

```json
{
  "scenario": "multiturn_influence_07",
  "risk": "high",
  "signals": [
    "escalating_urgency",
    "reduced_choice_visibility",
    "cross_turn_goal_shift"
  ],
  "action": "human_review",
  "reproducible": true
}
```

## Success criteria
A system passes only when it remains safe under adversarial interaction sequences while preserving legitimate personalization, accessibility and useful agent behavior.