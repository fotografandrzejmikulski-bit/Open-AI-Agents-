# Knowledge Corpus — 2026-09-12 — AI Work Tools / Competitive Substitution / Workflow Composition

## Scope

Ten supplied visual references were reviewed as one discovery-oriented corpus. They cover AI assistants, coding, image/video generation, writing, research, presentations, knowledge management, project management, scheduling, transcription/meeting notes, automation, sales, customer service, marketing, SEO, social media, design, audio, app builders, recruiting and business productivity.

The corpus contains repeated images and static rankings. Repetition is treated as corroboration of recurring capability categories, not as independent evidence. Tool names, pricing, free/paid labels, rankings and model labels are discovery metadata only.

## Core finding

The strongest architectural signal is not any individual tool. It is the emergence of a **capability substitution graph**:

```text
USER / BUSINESS OUTCOME
        ↓
CAPABILITY REQUIREMENT
        ↓
WORKFLOW / TASK GRAPH
        ↓
CANDIDATE PROVIDERS / TOOLS
        ↓
SEMANTIC + MODALITY + QUALITY MATCH
        ↓
ACCESS / COST / LATENCY / PRIVACY
        ↓
POLICY + AUTHORIZATION
        ↓
EXECUTION
        ↓
OUTPUT QA
        ↓
MEASUREMENT
        ↓
PROVENANCE
        ↓
MEMORY / LEARNING
```

A product should therefore not be modeled as a single preferred application. It should be modeled as a set of capabilities with interchangeable, constrained implementations.

## Capability taxonomy observed

### Cognitive / language
- chatbots and general assistants;
- research and search;
- writing and rewriting;
- grammar/proofreading;
- summarization;
- knowledge management;
- email assistance;
- customer service.

### Creative / multimodal
- image generation;
- image editing;
- graphic design;
- logo generation;
- presentations;
- video generation;
- video editing;
- captions/shorts;
- voice/TTS;
- transcription;
- meeting notes;
- music/audio.

### Engineering
- coding assistance;
- agentic coding;
- app builders;
- website builders;
- workflow automation;
- spreadsheet/formula assistance;
- data visualization.

### Business operations
- sales/outreach;
- CRM;
- marketing;
- SEO;
- social media management;
- project management;
- scheduling;
- recruiting;
- productivity.

### Education
- AI fundamentals;
- machine learning;
- prompt engineering;
- application building;
- technical specialization;
- AI ethics and responsible use.

## Competitive substitution model

A basic-vs-pro or paid-vs-free comparison is insufficient for runtime routing. A candidate replacement must be scored against the actual task contract.

```yaml
CapabilityCandidate:
  capability:
  provider:
  product:
  modality_in: []
  modality_out: []
  quality_floor:
  context_limits:
  integration_requirements: []
  latency_target:
  cost_model:
  privacy_class:
  data_residency:
  licensing:
  lifecycle:
  availability:
  authorization:
  evidence:
  verified_at:
```

Required distinction:

`ALTERNATIVE ≠ EQUIVALENT`

A substitution is admissible only if all task-critical constraints remain satisfied. A free or cheaper service cannot silently replace a higher-quality or more private service when that changes the expected outcome.

## Workflow graph

The repeated category structure suggests representing work as a typed DAG rather than a linear prompt session:

```text
RESEARCH
 ├──→ WRITING
 ├──→ DATA / ANALYTICS
 └──→ STRATEGY

WRITING
 ├──→ DESIGN
 ├──→ PRESENTATION
 └──→ EMAIL / SOCIAL

DESIGN
 ├──→ IMAGE
 ├──→ VIDEO
 └──→ PRESENTATION

VIDEO
 ├──→ AUDIO / VOICE
 ├──→ CAPTIONS
 └──→ DISTRIBUTION

DISTRIBUTION
 ├──→ SEO
 ├──→ SMM
 ├──→ PPC
 └──→ ANALYTICS
```

Each edge should carry input/output contracts, provenance requirements and failure semantics.

## Work graph vs tool list

The corpus supports replacing a static “best tools” list with a dynamic work graph:

```text
TASK
 ↓
SUBTASKS
 ↓
CAPABILITIES
 ↓
CANDIDATE PROVIDERS
 ↓
CONSTRAINT FILTER
 ↓
ROUTING
 ↓
EXECUTION
 ↓
VERIFICATION
```

This directly complements the existing P100 provider/skill registry and P113 provider-neutral multimodal abstraction.

## Meeting / transcription / knowledge loop

The repeated appearance of transcription and meeting-note tools suggests an explicit evidence loop:

```text
AUDIO / MEETING
 ↓
TRANSCRIPTION
 ↓
SEGMENTATION
 ↓
ACTION / DECISION EXTRACTION
 ↓
HUMAN OR POLICY VALIDATION
 ↓
TASK / KNOWLEDGE RECORD
 ↓
FOLLOW-UP
 ↓
OUTCOME
```

Transcription output is observation, not automatically authoritative organizational truth. Decisions and tasks require provenance and appropriate confirmation.

## Automation boundary

The corpus repeatedly pairs workflow automation tools with AI agents. This reinforces the existing authorization doctrine:

`MODEL OUTPUT ≠ ACTION AUTHORIZATION`

```text
INTENT
 ↓
PLAN
 ↓
CAPABILITY RESOLUTION
 ↓
POLICY
 ↓
AUTHORIZATION
 ↓
ACTION
 ↓
READBACK
 ↓
POSTCONDITION
```

Automation should expose explicit trigger, scope, credential, rate, stop-condition and rollback semantics.

## App-builder / coding convergence

App builders, coding assistants and agentic development tools increasingly overlap. The correct abstraction is not “which app builder wins,” but:

```text
SPECIFICATION
 ↓
ARCHITECTURE
 ↓
CODE GENERATION
 ↓
DEPENDENCY RESOLUTION
 ↓
TEST
 ↓
SECURITY ANALYSIS
 ↓
BUILD
 ↓
ARTIFACT PROVENANCE
 ↓
DEPLOYMENT
 ↓
RUNTIME READBACK
```

This belongs to P100's development control plane rather than a new standalone project.

## Marketing / SEO synthesis

The marketing graphics reinforce a measurement-first loop already established in the portfolio:

```text
AUDIENCE / OUTCOME
 ↓
RESEARCH
 ↓
CONTENT / CREATIVE
 ↓
DISTRIBUTION
 ↓
SEO / PPC / SMM / EMAIL
 ↓
ANALYTICS
 ↓
ATTRIBUTION
 ↓
ITERATION
```

Tool selection is subordinate to outcome and evidence. Search volume, rankings, engagement and conversion claims require current measurement rather than infographic assertions.

## Education synthesis

Course lists should be treated as learning-resource discovery, not proof of competence:

```text
CAPABILITY GAP
 ↓
RESOURCE DISCOVERY
 ↓
LEARNING
 ↓
PRACTICE
 ↓
ASSESSMENT
 ↓
EVIDENCE OF COMPETENCE
 ↓
SKILL REGISTRY
```

## Negative / unsupported claims

The graphics do not establish:
- current pricing;
- current free-tier limits;
- API availability;
- functional equivalence;
- ranking validity;
- production quality;
- security posture;
- data-residency guarantees;
- licensing suitability;
- current model lifecycle.

Those properties require independent verification before routing or procurement decisions.

## Portfolio decision

**NO NEW NUMBERED PROJECT.**

The corpus strengthens existing capability/provider/workflow architecture, primarily:
- P100 — capability registry, provider substitution, workflow DAG, automation and development control plane;
- P113 — provider-neutral multimodal abstraction;
- P30 — marketing/SEO evidence loop;
- P114 — provenance and durable memory requirements.

## Invariants

- `LISTED ≠ VERIFIED`
- `FREE ≠ UNRESTRICTED`
- `PAID ≠ SUPERIOR BY DEFAULT`
- `ALTERNATIVE ≠ EQUIVALENT`
- `CONNECTED ≠ AUTHORIZED`
- `TRANSCRIPTION ≠ VERIFIED DECISION`
- `COURSE ≠ COMPETENCE`
- `GENERATION ≠ QA`
- `ANALYTICS ≠ ATTRIBUTION`
- `CI SUCCESS ≠ PRODUCTION CORRECTNESS`
