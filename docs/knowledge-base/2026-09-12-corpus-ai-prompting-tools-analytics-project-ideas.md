# Knowledge Corpus — AI Prompting, Tool Substitution, Analytics & Project-Idea Discovery

Date: 2026-09-12
Source: 10 uploaded visual references
Classification: secondary discovery evidence; competitive/tooling ontology; workflow-design input

## Executive synthesis

The corpus contains six recurring information classes:

1. prompt construction patterns;
2. paid/free and basic/pro tool substitution;
3. capability taxonomies across creative, productivity, marketing and developer workflows;
4. social-media production, scheduling and analytics;
5. web analytics/product analytics signals (including the Rybbbit dashboard example);
6. a large backlog of small generative-AI application ideas.

The material is useful primarily as a **capability-discovery and workflow-composition corpus**. It is not authoritative evidence for current rankings, pricing, product limits, model versions, free tiers, product equivalence or business outcomes.

## Prompting ontology

The first visual proposes eight prompt-design dimensions:

- assign a role;
- specify output format;
- provide examples / few-shot guidance;
- set constraints;
- define tone and style;
- iterate and refine;
- state target audience;
- it also recommends explicit reasoning instructions.

For the architecture, role, output schema, examples, constraints, style and audience are useful declarative prompt parameters. Internal chain-of-thought should **not** be treated as a required exposed output contract. The safe architectural equivalent is an explicit reasoning policy with concise rationale, verification criteria and structured intermediate state where needed.

Canonical prompt contract:

```text
TASK / OUTCOME
 ↓
ROLE / CAPABILITY CONTEXT
 ↓
INPUTS + EVIDENCE
 ↓
CONSTRAINTS
 ↓
OUTPUT SCHEMA
 ↓
QUALITY / ACCEPTANCE CRITERIA
 ↓
STOP CONDITIONS
 ↓
VERIFY
```

## Capability inventory

Across the visuals, repeated capability families include:

- chat/reasoning/research;
- writing/copywriting;
- image generation/editing;
- video generation/editing;
- audio/TTS/transcription;
- presentations;
- coding assistance and app building;
- spreadsheets/data analysis/visualization;
- meeting notes;
- scheduling;
- workflow automation;
- design/branding/logo creation;
- knowledge management;
- social-media management;
- SEO/keyword research;
- email marketing;
- sales/outreach;
- recruitment/career workflows;
- education and learning.

The repeated appearance of the same providers in multiple categories supports a graph model in which products expose multiple capabilities and a capability can have multiple provider implementations.

## Paid/free substitution

The graphics present many paid/free pairs, including examples such as ChatGPT/Claude, Photoshop/Canva, Runway/Pika, Midjourney/NightCafe, Notion AI/TextCortex and Zoom/Tldv.

These pairings are discovery hypotheses only. They must not become automatic fallback rules.

Required substitution test:

```text
CAPABILITY
+ MODALITY
+ QUALITY FLOOR
+ CONTEXT / LIMITS
+ INTEGRATION
+ PRIVACY
+ LATENCY
+ COST
+ LICENSING
+ PROVENANCE
```

Invariant: `ALTERNATIVE ≠ EQUIVALENT`.

## Social-media production loop

The social-media visual divides work into content ideas, scheduling, design, analytics, images, hashtags and editing. This is more valuable architecturally than the individual product names.

Canonical workflow:

```text
IDEA / TREND SIGNAL
 ↓
CONTENT PLAN
 ↓
ASSET CREATION
 ↓
EDITING / CAPTIONS
 ↓
SCHEDULING / DISTRIBUTION
 ↓
OBSERVATION
 ↓
ANALYTICS
 ↓
ATTRIBUTION / INTERPRETATION
 ↓
ITERATION
```

A metric dashboard is an observation surface. It does not prove causality or revenue attribution without a measurement design.

## Analytics / Rybbbit signal

The supplied Rybbbit image shows a dark analytics dashboard with website metrics such as visitors, sessions, pageviews, bounce rate and session duration, plus trends over time and page/user views.

Architectural implication: P100 should represent analytics as an evidence-producing capability with metric definitions, source identity, collection window, aggregation method and provenance. Dashboard screenshots are not sufficient evidence for durable claims.

Required analytics record:

```text
SOURCE
+ METRIC DEFINITION
+ TIME WINDOW
+ FILTERS / SEGMENTS
+ RAW / AGGREGATED STATE
+ CALCULATION
+ OBSERVATION
+ INTERPRETATION
+ CONFIDENCE / LIMITATIONS
```

## Marketing / SEO

The corpus repeatedly groups SEO, keyword research, content research, social publishing, email marketing, design and analytics into one creator workflow. This reinforces the existing decomposition:

```text
DISCOVER
 → PRODUCE
 → DISTRIBUTE
 → MEASURE
 → LEARN
 → REVISE
```

Tool presence is not an SEO result. Keyword volume or ranking claims require current evidence from an appropriate measurement source.

## Project-idea corpus

The final visual lists 60 generative-AI project ideas at beginner, intermediate and advanced levels. Representative families include:

- resume/career assistance;
- social caption and tweet tools;
- naming and bio generation;
- blog/SEO generation;
- email assistance;
- document/PDF analysis;
- recipe and course generation;
- quiz generation;
- content scheduling;
- podcast and video summarization;
- job matching;
- pitch decks;
- portfolio review;
- startup validation;
- finance tracking;
- contract analysis;
- brand voice rewriting;
- text-to-website content.

These are opportunity signals, not validated market demand. Most ideas are feature-level capabilities that can be subsumed into broader products already represented in the portfolio.

## New-project decision

No new numbered project is warranted from this corpus alone.

Reason: the ideas largely decompose into existing capability families and can improve P100/P30/P113/P114. Creating one project per micro-tool would fragment the portfolio and duplicate existing architecture.

A new project should be created only if later evidence establishes a distinct product boundary, target user, defensible workflow, differentiated data moat, or independent monetization model.

## Security and evidence boundaries

- infographic ranking ≠ benchmark evidence;
- paid/free label ≠ current pricing truth;
- product pairing ≠ functional equivalence;
- dashboard screenshot ≠ raw analytics evidence;
- metric ≠ causality;
- prompt hack ≠ guaranteed model behavior;
- project idea ≠ validated market demand;
- generated copy ≠ factual claim verification;
- course/tool listing ≠ competence;
- current model/provider state must be resolved from live authoritative sources before execution.

## Portfolio integration

Primary: P100 capability/provider/workflow registry and substitution graph.

Secondary:
- P30: SEO/marketing evidence workflow;
- P113: provider-neutral multimodal capability abstraction;
- P114: provenance and verification substrate;
- relevant creative/video/audio projects inherit capability discovery but do not inherit static product claims.

Status: **KNOWLEDGE INTEGRATED — IMPLEMENTATION VERIFICATION PENDING**
