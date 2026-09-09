# Knowledge Base — Business Model, Strategy, Innovation and Governance

## Source corpus
This knowledge module synthesizes the newly supplied business-model and strategy corpus: research papers on business-model definitions and strategy relationships, organizational competencies, innovative business models in hospitality, contemporary hybrid marketing strategies, SME business-model guidance, and the GOZ 2030 circular-economy strategy handbook.

The source material is treated as scholarly/industry guidance. Historical survey numbers, projected savings, market effects and case-study outcomes remain source-derived claims until independently validated.

## 1. Business model versus strategy
A recurring distinction across the corpus is that a business model explains how an organization creates, delivers and captures value, while strategy concerns longer-term goals, choices and means of reaching them. The concepts overlap in resources, value capture and competitive positioning, but should not be collapsed into one object. Oliński explicitly frames business model and strategy as separate but related conceptual entities, with value as a central category of the business model. fileciteturn124file0L11-L25

Kardas summarizes three useful perspectives on business-model definitions: financial, operational and strategic. A robust business model therefore should expose how value is created, how internal processes enable that creation, and how the organization positions itself and interacts with stakeholders. fileciteturn124file1L38-L47

Drzewiecki likewise distinguishes the more static representation of a business model from the more adaptive behavioral character of strategy. fileciteturn124file5L31-L46

## 2. Core business-model representation
The practical SME material provides a direct operational definition: a business model answers three questions — how value is created, how value is delivered to the customer, and how the company earns from the value created. It separately states that business model is not strategy. fileciteturn124file9L30-L40

This becomes a machine-oriented contract:

```text
CUSTOMER / NEED
      ↓
VALUE CREATION
      ↓
VALUE DELIVERY
      ↓
VALUE CAPTURE
      ↓
ECONOMIC OUTCOME
```

## 3. Business Model Canvas and pattern thinking
The SME handbook organizes business-model work around Business Model Canvas, repeatable business-model mechanisms, competitive advantage, unique value proposition, Design Thinking, change planning, evaluation and experimentation. fileciteturn124file9L5-L19

This is useful for OmniCore as a structured design grammar rather than as a rigid universal ontology. Business-model patterns should be reusable hypotheses with explicit assumptions, dependencies and evidence states.

## 4. Dynamic adaptation and model redesign
The marketing-strategy paper stresses that business environments are turbulent, strategies can become obsolete quickly, and organizations need the ability to redefine them as conditions change. Information, timing and technology are highlighted as strategic resources; online and offline strategies can be combined as hybrid market approaches. fileciteturn124file2L20-L38 fileciteturn124file2L45-L74

The hospitality research similarly argues that the ability to modify a business model is a condition for coping with changing demand, supply structures and competitive landscapes. fileciteturn124file7L44-L62

Engineering implication: a business model is a versioned state machine, not a static slide.

## 5. Competitive advantage and organizational competencies
Siwak treats key organizational competencies as intangible strategic assets that are rare, difficult to substitute and hard to imitate, and links them to strategy execution and value creation. fileciteturn124file3L7-L24

For OmniCore, competencies should be represented as a capability graph:

```text
RESOURCE
  ↓
CAPABILITY
  ↓
COMPETENCE
  ↓
ACTIVITY
  ↓
VALUE CREATION
  ↓
OUTCOME
```

The graph should preserve whether an edge is observed, inferred or hypothesized.

## 6. Model evolution and strategic reorientation
Brzóska frames the business model as a schematic representation of the business idea and differentiates it from strategy as the more flexible set of actions and behaviors. He links business models with resources, skills, value chain and profitability and treats model change as an instrument of strategic reorientation. fileciteturn124file4L28-L47

This suggests a controlled transformation loop:

```text
CURRENT MODEL
 ↓
MARKET / TECHNOLOGY SIGNALS
 ↓
ASSUMPTION MAP
 ↓
ALTERNATIVE MODEL VARIANTS
 ↓
ECONOMIC / CUSTOMER / OPERATIONAL TESTS
 ↓
EVIDENCE UPDATE
 ↓
ADOPT / REVISE / REJECT
```

## 7. Experimentation
The SME corpus explicitly includes experimentation and testing as a phase of business-model development. fileciteturn124file9L13-L19

OmniCore should therefore support hypothesis-led experiments rather than merely generate business ideas:

```yaml
BusinessModelExperiment:
  hypothesis:
  target_segment:
  value_proposition:
  channel:
  revenue_mechanism:
  cost_assumptions:
  operational_constraints:
  experiment:
  metric:
  baseline:
  threshold:
  evidence:
  decision:
```

## 8. Circular economy and ecosystem models
The GOZ 2030 handbook frames circular economy as an economic model in which resources circulate, added value is maximized and waste generation is reduced. It emphasizes that implementation often requires cooperation beyond a single company and explicitly highlights industrial symbiosis and broader stakeholder ecosystems. fileciteturn124file6L10-L33 fileciteturn124file6L51-L62

Engineering translation:

```text
RESOURCE INPUT
 ↓
USE / TRANSFORMATION
 ↓
PRODUCT / SERVICE
 ↓
RECOVERY / REUSE / REMANUFACTURE
 ↓
SECONDARY VALUE
 ↓
ECOSYSTEM LOOP
```

Circularity becomes a graph property rather than a marketing label.

## 9. Evidence and governance rules
The corpus contains heterogeneous academic definitions, case studies, surveys and strategic recommendations. OmniCore must preserve source class and confidence.

Required evidence states:
- `SOURCE_DERIVED`
- `OBSERVED`
- `INFERRED`
- `HYPOTHESIS`
- `EXPERIMENTAL`
- `VALIDATED`
- `REJECTED`
- `STALE`

Rules:
- business-model canvas completeness is not market validation;
- competitive advantage is not guaranteed by novelty;
- a case study is not causal proof for all firms;
- a strategic recommendation is not an observed outcome;
- an economic projection is not realized value;
- a customer segment description is not customer authorization or identity evidence.

## 10. Safe use of strategic influence material
The marketing and adoption sections may inform transparent UX, positioning, communication and voluntary referral mechanisms. They must not be transformed into covert persuasion, dependency engineering, exploitative personalization or vulnerability targeting. Human agency remains a system invariant.

## 11. Integration with existing OmniCore knowledge
This module extends Projects 34, 43–46, 56 and 63–65 by supplying a deeper model/strategy distinction, business-model pattern language, capability-to-value mapping, experiment contracts, adaptive strategic redesign and circular/ecosystem business modeling.
