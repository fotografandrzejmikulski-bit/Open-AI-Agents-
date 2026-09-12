# P100 Extension — Iteration 61 — Autonomous SEO / AI Search Visibility

## Purpose

Integrate the AutoSEO product corpus into the Nexus control plane as a governed autonomous-marketing capability rather than as a simple SEO tool listing.

## 1. Autonomous SEO capability graph

```text
BUSINESS / SITE
↓
OBSERVE SITE + SEARCH + COMPETITORS
↓
BUILD QUERY / TOPIC / ENTITY GRAPH
↓
SCORE OPPORTUNITIES
↓
AUTHOR CONTENT PLAN
↓
GENERATE CONTENT + VISUAL ASSETS
↓
POLICY / QUALITY / PROVENANCE GATE
↓
AUTHORIZE PUBLICATION
↓
PUBLISH
↓
READBACK
↓
MEASURE SERP + AI VISIBILITY + CONVERSIONS
↓
UPDATE MODEL / NEXT ACTION
```

## 2. AI Search Visibility registry

Add a capability class for answer-engine visibility:

```yaml
capability: ai_search_visibility
signals:
  - brand_mention
  - citation
  - recommendation
  - source_selection
  - entity_association
  - query_coverage
metrics:
  - model_share
  - citation_share
  - answer_presence
  - source_frequency
  - conversion_rate
```

`model_share` and similar AI-visibility metrics are experimental/product-derived measurements until independently standardized.

## 3. Competitive content intelligence

Add reusable workflow primitives:

- competitor discovery;
- query gap extraction;
- ranking-page feature extraction;
- topic/entity gap mapping;
- content opportunity scoring;
- intent classification;
- source-quality comparison;
- update prioritization.

Control rule:

`COMPETITOR CORRELATION ≠ CAUSAL RANKING FACTOR`

## 4. Content-factory integration

P97-compatible output contract:

```yaml
content_asset:
  query_intent: string
  target_entities: []
  source_set: []
  evidence_status: verified|mixed|unverified
  content_type: article|landing_page|faq|comparison|other
  visual_assets: []
  publication_target: string
  policy_status: pending|approved|rejected
  published_revision: string
  observed_outcomes: []
```

## 5. Backlink / mention automation risk model

External authority acquisition becomes a governed capability, not an implicit side effect.

Required observations:

- referring domain identity;
- indexability;
- topical relevance;
- authority evidence;
- network/reciprocity relationship;
- anchor distribution;
- link persistence;
- replacement/removal events;
- spam/manipulation indicators.

`BACKLINK AUTOMATION ≠ SAFE BY DEFAULT`

## 6. Publishing authorization

The autonomous system may prepare publication, but final execution follows the existing Nexus lifecycle:

`OBSERVE → PLAN → AUTHORIZE → ACT → READBACK → VERIFY`

No AI-generated content, SEO score or model recommendation can itself authorize publication or external reputation actions.

## 7. Outcome verification

Add causal-evidence separation:

```text
INTERVENTION
↓
OBSERVED SEARCH CHANGE
↓
OBSERVED AI-VISIBILITY CHANGE
↓
OBSERVED TRAFFIC CHANGE
↓
OBSERVED CONVERSION CHANGE
↓
CAUSALITY ASSESSMENT
```

The system must preserve the distinction between correlation, temporal association and causal evidence.

## 8. Quality gates

Before automated publication:

- source verification;
- factual consistency;
- intent match;
- originality / duplication checks;
- entity and topic coverage;
- policy compliance;
- brand-voice consistency;
- structured-data validity where applicable;
- image/infographic provenance;
- rollback readiness.

## 9. Strategic conclusion

AutoSEO demonstrates a commercially viable product pattern: combine research, content generation, publishing, authority acquisition and measurement into one recurring workflow.

The Nexus implementation should preserve the useful automation while adding stronger controls than the vendor marketing surface exposes:

`AUTOPILOT ≠ UNSUPERVISED AUTHORITY`

`AI VISIBILITY ≠ GUARANTEED CUSTOMER ACQUISITION`

`VENDOR CLAIM ≠ VERIFIED PERFORMANCE`
