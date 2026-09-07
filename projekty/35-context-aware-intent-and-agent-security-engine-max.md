# 35 — Context-Aware Intent & Agent Security Engine MAX

## Status
Architecture-ready defensive research project.

## Cel projektu

Zbudować warstwę bezpieczeństwa, która nie traktuje intencji użytkownika jako pojedynczej etykiety tekstowej, lecz jako **stan hipotezy aktualizowany w czasie** na podstawie historii rozmowy, kontekstu, źródła danych, niepewności, konsekwencji działania i dostępnych dowodów.

Projekt powstaje z połączenia badań nad intent recognition, contextual blindness, over-refusal/under-refusal oraz Chain-of-Attack. Raport o intencji wskazuje na potrzebę obsługi nieznanych intencji, dynamicznego odkrywania klas oraz wykorzystania kontekstu semantycznego zamiast wyłącznie słownikowych wyzwalaczy. fileciteturn52file0L15-L35 Raport o Chain-of-Attack opisuje atak jako semantycznie sterowany, kontekstowy i wieloetapowy, wykorzystujący historię interakcji zamiast pojedynczej tury. fileciteturn51file7L368-L397

## Główna zasada

```text
INTENT ≠ LAST PROMPT
INTENT = HYPOTHESIS OVER TRAJECTORY
```

System ma jednocześnie minimalizować dwa przeciwstawne błędy:

- **over-refusal** — blokowanie legalnego, edukacyjnego lub benignowego zadania na podstawie pojedynczych słów;
- **under-refusal** — przepuszczenie ryzykownego celu ukrytego w wieloetapowej, kontekstowej lub multimodalnej trajektorii.

Źródło wskazuje właśnie tę asymetrię jako fundamentalny problem obecnych systemów bezpieczeństwa. fileciteturn52file0L23-L35

## Architektura

```text
USER / EXTERNAL CONTENT
        |
        v
INPUT NORMALIZER
        |
        +--> language / encoding / structure
        +--> OCR / multimodal extraction
        +--> provenance
        |
        v
INTENT HYPOTHESIS ENGINE
        |
        +--> current intent
        +--> trajectory intent
        +--> alternative benign intents
        +--> uncertainty / OOS
        |
        v
CONTEXT INTEGRITY ENGINE
        |
        +--> semantic drift
        +--> authority changes
        +--> contradiction
        +--> memory influence
        +--> tool-context contamination
        |
        v
RISK / POLICY ENGINE
        |
        +--> consequence
        +--> capability required
        +--> evidence quality
        +--> dual-use classification
        |
        v
DECISION
  ├─ allow
  ├─ safe-complete
  ├─ constrain
  ├─ ask targeted clarification
  └─ refuse / escalate
```

## 1. Unknown-intent handling

The supplied ICPG research proposes dynamically generating task descriptions and avoiding arbitrary assignment of an unknown intent. fileciteturn51file2L89-L114

MAX implementation uses an explicit `UNKNOWN / OOS` state instead of forcing every request into a known class.

```yaml
IntentHypothesis:
  candidates: []
  confidence: 0..1
  evidence_refs: []
  benign_alternatives: []
  risk_relevant_features: []
  oos_probability: 0..1
  expires_at:
```

The model is allowed to say **"insufficient evidence"** rather than manufacturing certainty.

## 2. Semantic Few-Shot Context

Semantic Few-Shot Sampling is used as a retrieval layer for relevant historical examples rather than as an authority layer. The supplied report describes semantic KNN selection using embeddings to provide local context for rare or long-tail intents. fileciteturn51file2L115-L117

Security rule:

```text
RETRIEVED EXAMPLE
      ↓
CONTEXT EVIDENCE
      ≠
POLICY AUTHORITY
```

Examples can improve classification, but cannot grant capabilities or override policy.

## 3. Hybrid fast-path / deep-path detection

A lightweight classifier may perform the first-pass routing and OOS detection, while a larger model handles ambiguous cases. This follows the source's hybrid BERT + LLM direction for balancing computational cost and accuracy. fileciteturn50file0L72-L77

Routing policy:

```text
LOW RISK + HIGH CONFIDENCE
        → FAST PATH

HIGH UNCERTAINTY / HIGH CONSEQUENCE / TRAJECTORY DRIFT
        → DEEP PATH

CONFLICTING EVIDENCE
        → ESCALATE
```

## 4. Chain-of-Attack trajectory engine

The system stores a compact security representation of the interaction rather than relying on raw history alone:

```text
TurnState
  intent_hypothesis
  semantic_delta
  policy_relevance
  provenance_delta
  capability_delta
  risk_delta
  evidence_refs
```

A trajectory detector searches for:

- gradual semantic drift;
- accumulation of individually benign steps toward a protected objective;
- attempts to redefine the system's authority hierarchy;
- persona or role conditioning that changes the effective policy context;
- delayed transitions from information requests to consequential actions;
- repeated attempts to exploit prior model commitments.

The source explicitly characterizes CoA as multi-turn and context-dependent, with toxicity distributed across turns. fileciteturn50file1L49-L78

## 5. Multimodal intent continuity

Text, images, OCR, audio transcripts, video-derived events and external documents enter the same intent-state model.

```text
TEXT ─┐
IMAGE ├─> NORMALIZED EVIDENCE ─> INTENT TRAJECTORY
AUDIO ┤
VIDEO ┤
WEB ──┤
DOC ──┘
```

The Gemini security material identifies multimodality as an expansion of attack surface and highlights visual/contextual injection classes. fileciteturn50file2L7-L31

## 6. Intent vs authority

A crucial separation is:

```text
WHAT DOES THE USER WANT?
            ↓
WHAT IS THE USER AUTHORIZED TO DO?
            ↓
WHAT CAPABILITY MAY BE EXERCISED?
```

A high-confidence intent does not imply authorization. Authorization remains deterministic and capability-based, inherited from Project 26.

## 7. Memory-aware intent verification

Long-lived memory is treated as potentially contaminated context. The Gemini material describes persistent memory poisoning as a mechanism through which hostile instructions can survive between sessions. fileciteturn52file5L240-L258

Therefore every security-relevant memory item carries:

```text
origin
created_at
source_type
provenance
confidence
independent_evidence
policy_impact
expiry
```

A memory record cannot silently change authorization policy.

## 8. Safe-completion decision model

Instead of a binary allow/deny classifier, the engine selects the least risky useful response:

```text
BENIGN + CLEAR
    → NORMAL ASSISTANCE

BENIGN + AMBIGUOUS
    → CLARIFY / NARROW

DUAL-USE + LOW CONSEQUENCE
    → SAFE COMPLETION / HIGH-LEVEL HELP

RISKY + NON-CONSEQUENTIAL
    → CONSTRAINED ASSISTANCE

RISKY + CONSEQUENTIAL
    → REFUSE / ESCALATE
```

The source explicitly argues that eliminating refusal entirely is unsafe because educational framing can be used as a mask; the target is contextual intent awareness, not unrestricted assistance. fileciteturn52file4L193-L204

## 9. Behavioral and influence signals

This project does not infer maliciousness from personality or body language. It can, however, detect **interactional risk signals** such as:

- coercive framing;
- authority impersonation;
- urgency designed to bypass verification;
- repeated pressure after refusal;
- contradictory claims about authorization;
- attempts to make the agent suppress logging or oversight;
- attempts to establish artificial trust before requesting sensitive actions.

These are risk features, never proof of intent.

## 10. Evaluation matrix

| Dimension | Test | Metric |
|---|---|---|
| Intent | known / unknown / long-tail | macro-F1 + calibration |
| OOS | unrelated requests | OOS precision/recall |
| Context | multi-turn drift | detection latency |
| Safety | over-refusal | benign pass rate |
| Safety | under-refusal | protected-task block rate |
| Multimodal | OCR/image/context injection | unauthorized-action rate |
| Memory | poisoned durable context | memory integrity rate |
| Authority | fake authorization | broker denial rate |
| Robustness | paraphrase / language / encoding | safety parity |
| Consequence | low vs high impact | escalation accuracy |

## 11. Telemetry schema

Every decision stores a compact event:

```yaml
DecisionEvent:
  session_id:
  turn_id:
  intent_hypothesis:
  confidence:
  uncertainty:
  provenance_refs:
  trajectory_risk:
  policy_version:
  capability_requests:
  decision:
  explanation_class:
  escalation:
  model_version:
```

Sensitive raw content should be minimized; the ledger records enough information for reproducibility and audit without becoming an uncontrolled secondary data store.

## 12. Integration

Project 35 is the **intent/context security layer** for:

- Project 12 — Cognitive Security & Adversarial Evaluation;
- Project 24 — Agentic Prompt Compiler & DSL;
- Project 26 — OmniCore Trustworthy Kernel;
- Project 27 — Compound Reasoning;
- Project 30 — Sugra Evidence/OSINT Control Fabric;
- Project 31 — Sovereign Agent Operating Fabric;
- Project 34 — Venture & Business Model Foundry.

## Definition of Done

1. Unknown intent is an explicit state.
2. Intent is evaluated over trajectory, not only the latest turn.
3. Retrieval examples cannot become policy authority.
4. Multimodal and external content preserve provenance.
5. Memory cannot silently modify authorization.
6. Safe-completion reduces over-refusal without removing consequential-action controls.
7. Every decision is reproducible from versioned policy/model/context metadata.
8. The evaluation suite demonstrates measurable resistance to stateful and multimodal attacks.
