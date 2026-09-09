# Marketing Strategy for Small Business — Source-Derived Knowledge Module

## Status
`SOURCE_DERIVED → ENGINEERING_SYNTHESIS → PROPOSED`

This module extracts reusable marketing-strategy methodology from the supplied small-business marketing guide. It is a knowledge layer, not a claim that the source's framework is universally optimal.

## 1. Strategy workflow

The source presents marketing strategy as a structured sequence rather than intuition alone:

`goal → business characterization → profitability/revenue matrix → growth objectives → SWOT → UX/UI and communication audits → competitor communication audit → customer needs → segmentation → 7P → BVP/USP → targeting → proto-personas → Customer Journey Map → communication strategy → marketing plan`.

The source explicitly states that the current market requires knowledge in addition to intuition and frames the guide as a compromise between academic theory and practical experience. fileciteturn80file5L59-L72

## 2. Business and marketing strategy are coupled but distinct

The supplied management literature distinguishes a business model from strategy. The business model is broader in its representation of value creation, value-chain position, resources, partners and customer relationships; strategy emphasizes longer-term goals, action and competitive positioning. fileciteturn81file7L283-L301

A reusable system should therefore maintain separate objects:

```yaml
BusinessModel:
  value_creation:
  value_delivery:
  value_capture:
  resources:
  partners:
  customers:
  economics:

Strategy:
  objectives:
  competitive_position:
  choices:
  action_patterns:
  constraints:
```

## 3. Customer intelligence layer

The marketing source emphasizes customer needs and expectations, segmentation, targeting, proto-personas and Customer Journey Maps. These should become structured evidence rather than decorative personas.

```text
SEGMENT
  ↓
PROTO-PERSONA
  ↓
NEED / EXPECTATION
  ↓
CONTEXT / TRIGGER
  ↓
CUSTOMER JOURNEY
  ↓
TOUCHPOINT
  ↓
MESSAGE / OFFER
  ↓
MEASURED OUTCOME
```

## 4. Positioning and proposition

The workflow explicitly includes BVP (Brand Value Proposition) and USP (Unique Selling Proposition), followed by communication strategy. The engineering interpretation is to maintain a traceable chain from customer problem to differentiated value claim and then to observable communication assets. fileciteturn81file5L209-L224

## 5. Measurement and execution

The final artifact should not stop at a strategy document. A governed marketing system should connect objectives to KPIs, experiments, channels, customer-journey observations and realized outcomes.

```text
OBJECTIVE
 → HYPOTHESIS
 → OFFER / MESSAGE
 → CHANNEL
 → EXPERIMENT
 → KPI
 → RESULT
 → LEARNING
 → STRATEGY UPDATE
```

## 6. Integration

This module strengthens the repository's existing adaptive business-model and strategy lineage, especially Project 66/67. It does not create a duplicate project merely because the source adds another marketing methodology.
