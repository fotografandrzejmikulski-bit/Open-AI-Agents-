# P124 — Cognitive Dissonance Marketing Agent MAX

## Status
DESIGNED / PORTFOLIO INTEGRATION

## Mission
Agentic marketing system for narrative products, initially books, that converts story canon into emotionally intense campaign concepts, advertising copy, visual concepts, model-specific image prompts, campaign variants, experiments, and verified marketing artifacts.

The system optimizes for narrative relevance, curiosity, emotional intensity, creative differentiation, and measurable campaign performance without fabricating facts or presenting fictional elements as real-world claims.

## Core principle
`EMOTIONAL INTENSITY ≠ DECEPTION`

Marketing pressure, controversy, moral tension, curiosity gaps, and cliffhangers are creative parameters. They do not authorize fabrication, impersonation, unsupported factual claims, or concealed consequential actions.

## Canonical pipeline
`BOOK/STORY → STORY INTELLIGENCE → AUDIENCE MODEL → EMOTIONAL MAP → HOOK → TENSION → DISSONANCE → CLIFFHANGER → COPY → VISUAL CONCEPT → PROMPT COMPILER → VARIANTS → CLAIMS QA → CAMPAIGN QA → HUMAN APPROVAL → TEST → ANALYZE → EVOLVE`

## Agent topology

### A01 — Campaign Orchestrator
Owns workflow state, dependencies, lineage, approvals, retries, and artifact routing. It coordinates specialists but is not itself an authorization authority.

### A02 — Story Intelligence Agent
Builds a structured representation of characters, relationships, conflicts, secrets, turning points, moral dilemmas, revelations, ending, and spoiler boundaries.

Artifact: `story-intelligence-map`

### A03 — Emotional Mapping Agent
Maps emotions to narrative causes, scenes, characters, intensity, triggers, audience effects, and spoiler risk.

Artifact: `emotional-map`

### A04 — Audience Psychology Agent
Creates campaign-level audience segments and maps promise, emotional entry point, information gap, and explicit CTA. It works with audience segments rather than covertly manipulating identifiable individuals.

Artifact: `audience-segment-model`

### A05 — Hook Architect
Generates and scores hooks based on moral dilemma, taboo, contradiction, shock, question, accusation, impossible choice, and revelation structures.

Artifact: `hook-library`

### A06 — Cognitive Dissonance Engine
Constructs controlled tension between audience expectation and story-derived information. It must remain faithful to the source canon.

Artifact: `dissonance-map`

### A07 — Tension Architect
Controls disturbance, escalation, moral conflict, information gaps, pacing, revelation density, emotional volatility, and spoiler exposure.

Artifact: `tension-curve`

### A08 — Cliffhanger Engine
Creates safe information gaps using partial revelation, question, decision, identity, discovery, or unresolved-event structures while enforcing spoiler budgets.

Artifact: `cliffhanger-map`

### A09 — Copywriter Agent
Produces structured campaign copy: hook, body, cliffhanger, CTA. Supports multiple controlled styles including literary, psychological, cinematic, minimalist, trailer-style, social, premium, and dark-fiction variants.

Artifact: `copy-variant`

### A10 — Visual Concept Director
Translates narrative/emotional intent into subject, environment, composition, symbolism, camera, lens, lighting, texture, visual hierarchy, and negative space before prompt compilation.

Artifact: `visual-concept`

### A11 — Visual Prompt Compiler
Compiles approved concepts into model-specific prompts for Midjourney, DALL-E, FLUX, SDXL, and future image models. Model syntax and capabilities are resolved explicitly rather than blindly mixing parameters.

Artifact: `visual-prompt`

### A12 — Visual Continuity Agent
Maintains continuity of characters, age, clothing, props, locations, architecture, chronology, symbolism, lighting, and photographic language across campaign assets.

Artifact: `creative-continuity-record`

### A13 — Variant Generator
Produces controlled campaign families with distinct emotional vectors such as anger, grief, mystery, betrayal, moral dilemma, fear, and curiosity.

Artifact: `campaign-variant-set`

### A14 — Campaign Experiment Agent
Designs A/B experiments from explicit hypotheses and evaluates CTR, CPC, conversion, engagement, saves/shares, purchase/read-through where available, and creative fatigue.

Artifact: `ab-experiment`

### A15 — Claims Integrity Agent
Labels every factual assertion as supported, source-derived, interpretation, creative, or unsupported. Unsupported factual claims are blocked or routed for revision.

Artifact: `claims-ledger`

### A16 — Campaign QA Agent
Checks source fidelity, spoiler leakage, continuity, language, CTA, copy/visual consistency, prompt validity, platform constraints, claims, accessibility, and brand consistency.

Artifact: `campaign-qa-report`

## Canonical artifacts
- `campaign-project-spec`
- `story-intelligence-map`
- `emotional-map`
- `audience-segment-model`
- `hook-library`
- `dissonance-map`
- `tension-curve`
- `cliffhanger-map`
- `copy-variant`
- `visual-concept`
- `visual-prompt`
- `campaign-variant-set`
- `claims-ledger`
- `creative-continuity-record`
- `ab-experiment`
- `campaign-qa-report`
- `campaign-lineage`

## Emotional → visual translation
The engine does not reduce emotion to generic visual clichés. It transforms:

`EMOTION → NARRATIVE CAUSE → PHYSICAL SYMBOL → COMPOSITION → LIGHT → CAMERA → IMAGE`

Example:
`BETRAYAL → absence of trusted person → two objects where only one should remain → asymmetric composition → hard directional light → shallow depth of field → hyperrealistic photographic frame`

## Campaign memory
The system versions and preserves:
- book canon
- character canon
- visual canon
- campaign canon
- copy canon
- previous variants
- performance history
- rejected concepts
- spoiler boundaries

Performance data can change campaign strategy but cannot rewrite the underlying story canon.

## Operating modes
1. `DISCOVERY` — ingest and structure the source.
2. `CAMPAIGN` — design the campaign and variants.
3. `PRODUCTION` — generate approved copy, concepts, and prompts.
4. `OPTIMIZATION` — evaluate experiments and generate the next hypothesis.

## Verification and governance
Core doctrine:
- `MODEL OUTPUT ≠ AUTHORIZATION`
- `PERSONA/AUDIENCE MODEL ≠ FACT`
- `CREATIVE CONCEPT ≠ FACTUAL CLAIM`
- `GENERATED IMAGE ≠ SOURCE EVIDENCE`
- `PROMPT SUCCESS ≠ CREATIVE APPROVAL`
- `CAMPAIGN API ACCESS ≠ USER AUTHORIZATION`
- `PLATFORM SUCCESS ≠ PUBLICATION VERIFICATION`

Human approval is required before externally consequential publication, paid campaign activation, or other consequential actions. The agent records the approval state and verifies postconditions after execution.

## Safety / integrity boundary
The system may use strong emotional rhetoric, controversy, moral dilemmas, curiosity gaps, and narrative cliffhangers. It must not fabricate evidence, invent reviews or awards, impersonate real people, disguise fiction as fact, or create unsupported claims about real-world events, products, or people.

## Integration map
- **P100 — NeXus AI Code / OMEGA-X:** orchestration, capability control, provenance, verification, audit, and execution governance.
- **P07 — Agentic Creative Studio:** creative artifact production and campaign workflow.
- **P113 — OmniVisual Prompt Compiler:** model capability routing and visual prompt compilation.
- **P123 — Podcast Agent Factory MAX:** downstream consumer for podcast promotion, episode campaigns, cliffhanger/tension systems, and promotional visual assets.
- **P110 — OmniGrand Human & Creative Strategy Intelligence Fabric MAX:** strategic marketing foundation and higher-level campaign intelligence.

## Evolution loop
`CAMPAIGN → AUDIENCE RESPONSE → PERFORMANCE DATA → ANALYSIS → HYPOTHESIS → VARIANT → TEST → VERIFY → CAMPAIGN MEMORY`

The optimization loop changes the campaign strategy, not the truth conditions of the source material.

## Initial acceptance criteria
- Reconstructs a source story without inventing canon.
- Produces multiple distinct emotional campaign vectors.
- Generates hooks, bodies, cliffhangers, and explicit CTAs as separate artifacts.
- Produces visual concepts before model-specific prompts.
- Preserves visual continuity across a campaign family.
- Detects unsupported factual claims.
- Detects spoiler leakage.
- Maintains campaign lineage and version history.
- Separates creative generation from consequential publication.
- Supports measurable A/B experimentation.
- Fails closed when source truth, authority, or capability is ambiguous.

## First production contract
Input:
`title + story outline/full manuscript + target audience + campaign objective + platform + visual references + spoiler boundary`

Output:
`3+ campaign variants × {HOOK, BODY, CLIFFHANGER, CTA, VISUAL CONCEPT, VISUAL PROMPT} + CLAIMS LEDGER + QA REPORT + LINEAGE`

## Portfolio classification
P124 is a dedicated reusable marketing-agent project. Its infrastructure is shared with P100/P07/P113/P123, while the Cognitive Dissonance Engine remains a specialized reusable subsystem for narrative marketing.
