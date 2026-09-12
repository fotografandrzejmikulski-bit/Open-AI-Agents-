# Corpus: AI Tool Market — Capability Expansion and Competitive Substitution

**Date:** 2026-09-12
**Role:** source-derived market corpus from operator-supplied tool catalogs
**Primary integration:** P100 — NeXus AI Code / OMEGA-X

## 1. Source scope

The supplied corpus expands the observed AI-tool market across presentations, spreadsheets, scheduling, knowledge management, chatbots, image generation, writing, email assistance, workflow automation, graphic design, data visualization, coding, meeting notes, video generation, SEO, websites, productivity, data/Excel, Word/document workflows, search, paint/drawing, and tool/skill catalogs.

It also contains comparative pairings such as ChatGPT→Claude, Runway→RecCloud, Canva→Microsoft Designer, Midjourney→DALL-E 3, PowerPoint→Google Slides, Grammarly→QuillBot, Zapier→Bardeen, Fireflies→Laxis, Synthesia→HeyGen, Durable→10Web and Iconfinder→Icons8.

These pairings are treated as **substitution hypotheses**, not evidence that the products are equivalent, superior or currently available.

## 2. Normalization requirements

The source contains duplicates, aliases, misspellings, obsolete product names, mixed product/function entries and category overlap. Examples include Grammarly/Grammerly, Midjourney variants, Fireflies variants, 10Web/10WEB, Github Copilot/GitHub Copilot, Bing Create/Bing AI, and repeated products across multiple categories.

Before any provider is admitted to a canonical registry:

`RAW NAME → ENTITY RESOLUTION → CURRENT STATUS → CAPABILITY EXTRACTION → EVIDENCE → REGISTRY`

No static list is authoritative for current pricing, availability, feature scope or product lifecycle.

## 3. Capability ontology expansion

Observed capability classes:

- presentation generation;
- spreadsheet generation/formula assistance;
- scheduling and calendar optimization;
- knowledge management and personal memory;
- general chat/reasoning;
- image generation;
- writing/copywriting/rewrite;
- email assistance;
- workflow automation;
- graphic/UI design;
- data visualization;
- coding assistance;
- meeting transcription/notes;
- video generation/editing;
- SEO and search optimization;
- website generation;
- social/X publishing;
- sales/outreach/CRM assistance;
- research and academic knowledge work;
- resume/career workflows;
- voice/audio/music;
- prompt/model tooling;
- education and AI literacy;
- agent runtime/tool/skill orchestration.

## 4. Market structure

The corpus supports a layered model:

```text
USER JOB
  ↓
CAPABILITY
  ↓
SUB-CAPABILITY
  ↓
WORKFLOW STEP
  ↓
PROVIDER / PRODUCT
  ↓
INTEGRATION / API / MCP
  ↓
QUALITY + COST + LATENCY + DATA POLICY
```

The strategic unit should therefore be the **job/workflow contract**, not the product name.

## 5. Competitive substitution graph

Comparative pairings should be stored as directed, evidence-qualified edges:

`PRODUCT_A --[task/capability, evidence, date]--> PRODUCT_B`

A substitution edge requires evaluation of:
- task equivalence;
- output quality;
- modality;
- integration surface;
- latency;
- cost;
- privacy/data handling;
- reliability;
- automation depth;
- lifecycle status.

A category match alone is insufficient.

## 6. Workflow opportunity layer

The most important strategic signal is repeated adjacency between categories:

```text
RESEARCH → WRITING → DESIGN → VIDEO → DISTRIBUTION → SALES → ANALYTICS
```

and:

```text
MEETING → TRANSCRIPTION → KNOWLEDGE → TASKS → SCHEDULING → FOLLOW-UP
```

and:

```text
IDEA → WEBSITE → CONTENT → SEO → SOCIAL → LEADS → CRM → ANALYTICS
```

These chains identify opportunities for vertical agents and workflow-native products that coordinate several capabilities instead of duplicating a single generator.

## 7. Tool/skill registry signal

The supplied Available Tools / Available Skills material is useful as a benchmark for a capability registry containing browser, clarification, code execution, scheduling, delegation, filesystem, smart-home, autonomous-agent, creative, email, GitHub, MCP, media, MLOps, note-taking, productivity, research and software-development capabilities.

However, tool availability must remain separate from authorization:

`DISCOVERED ≠ INSTALLED ≠ HEALTHY ≠ AVAILABLE ≠ AUTHORIZED ≠ ALLOWED`

Skills remain instruction/procedure assets, not permission grants.

## 8. Education corpus

The supplied AI-learning entries identify recurring onboarding themes: AI fundamentals, ethics, ChatGPT, AI in business, career applications, prompt engineering, AI fluency and responsible generative AI.

This strengthens the education capability ontology but does not establish current course availability or free/certificate status without independent verification.

## 9. Security corpus boundary

The supplied WiFi Pumpkin, Hashcat and EAPHammer material is classified as **cybersecurity tool corpus**, not as a product recommendation or execution recipe. The market-intelligence layer may catalog security capabilities and risk classes, but privileged offensive operations remain governed by P100 authorization, sandboxing and policy controls.

## 10. New reusable primitives

- ai-tool-entity-record
- capability-taxonomy-node
- provider-lifecycle-record
- capability-substitution-edge
- workflow-adjacency-graph
- tool-evidence-record
- market-opportunity-score
- skill-capability-separation
- tool-availability-state
- competitive-gap-candidate

## 11. Integration decision

This corpus materially extends the existing P100 capability/provider registry and competitive-substitution architecture. It does **not** justify a separate standalone project by itself.

A future dedicated market-intelligence product should only be promoted to a standalone project if it acquires independent scope such as continuous provider verification, measurable demand signals, opportunity scoring, competitor monitoring and automated candidate generation.

## 12. Core invariants

`TOOL_LIST ≠ CURRENT_TRUTH`

`CATEGORY_MATCH ≠ FUNCTIONAL_EQUIVALENCE`

`PROVIDER_EXISTS ≠ PROVIDER_AVAILABLE`

`AVAILABLE ≠ AUTHORIZED`

`SKILL ≠ PERMISSION`

`STATIC_CATALOG ≠ MARKET_DEMAND`

`SIMILAR_PRODUCT ≠ BETTER_PRODUCT`

`GENERATED_OUTPUT ≠ BUSINESS_OUTCOME`
