# Knowledge Base — Business Models, Strategy, Innovation, Capabilities and Circular Economy

## Source corpus
This entry consolidates the supplied materials on business-model theory, strategy, organizational capabilities, marketing strategy, innovative business models, SME business-model design, and circular-economy strategy.

### Evidence discipline
The corpus is scholarly/educational and contains historical studies, frameworks and source-specific claims. Quantitative statements are preserved as source claims unless independently verified. Models are treated as analytical instruments rather than guarantees of commercial success.

## 1. Business model versus strategy
The literature distinguishes business model from strategy while recognizing substantial overlap. Oliński frames the business model around value creation for customers and value capture by the enterprise, while strategic thinking emphasizes longer-term goals and means of achieving them. The two constructs share resources, competencies and value-capture mechanisms but should not be collapsed into one concept. fileciteturn124file0L11-L25

Drzewiecki explicitly evaluates similarities and differences using dimensions such as construction, desired characteristics, formalization, formulation process and use. fileciteturn124file5L6-L13

Brzóska treats the business model as a comparatively static representation of the business idea/economic result architecture, while strategy expresses the organization’s actions and adaptation to changing conditions. fileciteturn124file4L29-L47

### OmniCore distinction
Use separate typed objects:
- `BusinessModelSpec` — how value is created, delivered and captured;
- `StrategySpec` — goals, competitive choices, positioning and adaptation;
- `OperatingModelSpec` — processes, resources, governance and execution;
- `OutcomeSpec` — measurable realized results.

A strategy can change without rewriting the ontology of the business model, and operations can change while the strategic intent remains stable.

## 2. Three-dimensional model-business interpretation
Morris, Schindehutte and Allen’s synthesis, as described by Kardas, groups business-model definitions into financial, operational and strategic dimensions. The financial perspective concerns profit generation; the operational perspective concerns internal processes and architecture for value creation; the strategic perspective covers positioning, stakeholders, differentiation, vision, networks and alliances. fileciteturn124file1L38-L47

This suggests a useful OmniCore business-model compiler with three explicit views:

`FINANCIAL ↔ OPERATIONAL ↔ STRATEGIC`

A candidate model is incomplete when one dimension is missing or unsupported.

## 3. Value creation and value capture
The SME material gives a compact operational definition: a business model explains how value is created, how it is delivered to the customer and how the firm earns from the created value. fileciteturn124file9L29-L35

The corpus repeatedly treats model redesign as a response to environmental change, changing customer needs, new technology, supply-side shifts and changes in competitive structure. Kachniewska emphasizes that adapting the model can become necessary under crisis, durable market transformation and shifts in demand/supply. fileciteturn124file7L44-L62

## 4. Business-model components and design
The PARP SME guide organizes practical design around:
- Business Model Canvas and its component blocks;
- business-model mechanics and recurring patterns;
- competitive advantage, Ten Types of Innovation and Blue Ocean Strategy;
- unique value proposition;
- Design Thinking;
- planning model change;
- model evaluation;
- experiments and testing. fileciteturn124file9L5-L19

The guide therefore supports a design lifecycle rather than a static canvas:

`DISCOVER → MODEL → DIFFERENTIATE → TEST → MEASURE → REDESIGN`

## 5. Strategic agility and capability architecture
Siwak places key organizational competencies within intangible assets and links them to strategy realization. The article emphasizes the challenge of balancing strategic agility with operational excellence and identifies key competencies as rare, difficult to substitute and difficult for competitors to copy. fileciteturn124file3L7-L24

This becomes an `OrganizationalCapabilityGraph`:

```text
CAPABILITY
 ├─ knowledge
 ├─ skills
 ├─ routines
 ├─ technology
 ├─ relationships
 ├─ intangible assets
 └─ governance
       ↓
STRATEGIC CHOICE
       ↓
VALUE CREATION
       ↓
OUTCOME
```

A capability is useful only when linked to an observable strategic outcome, not merely listed in an inventory.

## 6. Marketing strategy under turbulence
Golik-Górecka’s material describes hybrid real/virtual marketing strategies and stresses that information available at the right time can affect competitive position. It also argues that strategies and business models can become outdated quickly under turbulent market conditions, requiring flexible redefinition. fileciteturn124file2L18-L38 fileciteturn124file2L45-L53

### OmniCore strategic-intelligence rule
Market strategy should be represented as a living state with:
- environmental assumptions;
- evidence timestamp/freshness;
- competitive hypotheses;
- customer signals;
- channel performance;
- strategic alternatives;
- trigger conditions for revision.

## 7. Innovative business models and niche strategy
Kachniewska’s hotel-sector study argues that independent hotels can protect strategic independence by recognizing unique customer needs, redesigning their role in the value chain and involving customers in value design. The Medical Park case illustrates a niche-focused model outside the main area of network-hotel concentration. fileciteturn124file7L2-L16

Generalized pattern:

`UNDERSERVED NEED → DIFFERENTIATED VALUE → NICHE POSITION → CONTROL OVER VALUE RELATIONSHIP`

The important reusable idea is not hospitality itself; it is the capability to identify structurally underserved demand and reconfigure the value proposition around it.

## 8. Circular economy as business-model transformation
The GOZ 2030 corpus defines circular economy as a model in which resources circulate, added value is maximized and waste generation is minimized. It emphasizes that closing loops usually requires ecosystem-level cooperation and industrial symbiosis rather than isolated action within one company. The platform developed 30 strategies after examining practices, reports, expert meetings and workshops. fileciteturn124file6L10-L33 fileciteturn124file6L51-L62

### OmniCore `CircularValueGraph`
```text
MATERIAL / ENERGY / ASSET
        ↓
DESIGN
        ↓
PRODUCTION
        ↓
USE
        ↓
REPAIR / REUSE / REMANUFACTURE
        ↓
RECOVERY
        ↺
```

The graph must include economic value, material flow and stakeholder dependencies.

## 9. Cost and performance governance
The supplied volume *Zarządzanie kosztami i dokonaniami* contains work on performance measurement, management reporting, value-stream measurement, environmental costs and enterprise value. fileciteturn124file8L38-L75

For OmniCore, the key lesson is to connect business-model changes to both financial and non-financial outcome measures instead of treating revenue alone as the objective.

## 10. Strategic model-evaluation framework
The combined corpus yields a governed evaluation matrix:

| Dimension | Core question | Evidence |
|---|---|---|
| Customer value | Why would the customer choose this? | interviews, usage, conversion, retention |
| Value delivery | Can the promise be delivered reliably? | process metrics, SLA, capacity |
| Value capture | How does the organization earn? | revenue, margin, CAC/LTV, cash flow |
| Strategic fit | Does it support chosen positioning? | competitive analysis, scenario tests |
| Capability fit | Can the organization execute it? | capability graph, constraints |
| Adaptability | Can the model survive change? | sensitivity/scenario analysis |
| Sustainability | Does the model remain viable over time? | economic + resource outcomes |
| Governance | Are assumptions, rights and risks explicit? | provenance, controls, audit |

## 11. New synthesis: Adaptive Business Model Compiler
The corpus supports a new original architecture for OmniCore:

```text
MARKET / CUSTOMER / TECHNOLOGY / RESOURCE SIGNALS
                    ↓
              EVIDENCE GRAPH
                    ↓
        BUSINESS MODEL HYPOTHESES
                    ↓
             MODEL COMPILER
                    ↓
     ┌──────────────┼──────────────┐
     ↓              ↓              ↓
 FINANCIAL      OPERATIONAL      STRATEGIC
     └──────────────┼──────────────┘
                    ↓
             CAPABILITY GRAPH
                    ↓
          EXPERIMENT GENERATOR
                    ↓
            MEASURED OUTCOMES
                    ↓
        GENERALIZATION / DRIFT
                    ↓
       STRATEGY / MODEL REVISION
```

## 12. Safety and epistemic boundaries
- A business-model framework is not proof of market demand.
- A strategy document is not evidence of execution capability.
- A customer hypothesis is not a customer commitment.
- A forecast is not a realized outcome.
- A successful case study is not universal causal evidence.
- A competitive advantage claim requires evidence that the relevant capability is valuable and defensible.
- Sustainability claims require measurable resource and economic outcomes.
- Commercial optimization must not become covert behavioral manipulation or exploitation of vulnerable users.

## 13. Integration targets
This knowledge directly extends Projects 34, 45, 46, 47, 56, 60, 62, 63 and 64. It adds a stronger ontology for:
- strategy/model separation;
- capability-driven advantage;
- adaptive strategy state;
- value creation/capture analysis;
- business-model experimentation;
- circular-economy modeling;
- financial/non-financial outcome measurement.

## Source status
This entry is a source-grounded synthesis of the supplied corpus. It is not an assertion that every cited historical framework is empirically superior to all alternatives.
