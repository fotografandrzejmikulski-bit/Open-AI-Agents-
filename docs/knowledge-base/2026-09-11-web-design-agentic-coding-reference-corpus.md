# Knowledge Base — Agentic Web Design / Reference-to-Code Corpus — 2026-09-11

## Corpus

`10/10 supplied images reviewed`.

The corpus describes a repeatable workflow for turning visual web references into production-oriented frontend work with Claude Code and other agentic coding environments:

1. find a high-quality visual reference;
2. inspect/capture the reference implementation or HTML when legitimately available;
3. provide the reference plus project context to the coding agent;
4. activate reusable UI/UX and frontend-design skills;
5. import motion/interaction patterns from a component library such as 21st.dev;
6. implement in the target repository;
7. run iterative visual/functional QA;
8. preserve provenance, authorization and verification boundaries.

## Source-derived observations

### A. Reference-first web design

The supplied Webflow slide recommends using a professionally designed template as a visual reference rather than starting from a blank page. Current Webflow documentation confirms that its template marketplace provides professionally designed starting points, including landing pages, responsive layouts, reusable sections and interactions. citeturn0search3turn0search15

Engineering interpretation: visual reference selection should become an explicit input to the frontend specification rather than an informal inspiration step.

### B. Reference-to-code through 21st.dev

The supplied 21st.dev slide proposes copying a component prompt and asking the coding agent to place it into a target section. Current 21st.dev material describes a living library of React components/templates/themes and states that components ship with prompts that can be pasted into coding environments; its current surface includes animated heroes, shaders, backgrounds, marketing blocks and UI components. citeturn0search1turn0search6

Engineering interpretation: introduce a typed `DesignReference` / `ComponentReference` object rather than treating copied prompts as opaque text.

Suggested minimum fields:

```yaml
DesignReference:
  id:
  source:
  source_url:
  capture_type: screenshot|template|component|prompt|html
  license_or_usage_basis:
  visual_intent:
  target_surface:
  extracted_tokens:
  motion_requirements:
  provenance:
  verification_status:
```

### C. HTML capture from DevTools

One supplied slide instructs the user to inspect a page and copy `document.documentElement.outerHTML` from the browser console. This is a useful technical observation about obtaining the rendered document tree, but it is **not** evidence that arbitrary third-party HTML may be copied, redistributed or reused without restriction.

For the project architecture, HTML capture must be classified as untrusted external input and passed through:

`CAPTURE → SANITIZE → LICENSE/USAGE CHECK → EXTRACT DESIGN SIGNALS → REIMPLEMENT → VERIFY`.

The preferred target is design-system extraction and independent reimplementation, not blind duplication of third-party code, tracking logic, credentials, proprietary assets or hidden behavior.

### D. Claude Code as the implementation substrate

The supplied slides frame Claude Code as the environment in which a visual reference, project context and reusable skills are combined into a working landing page. The current Everything Claude Code ecosystem provides concrete evidence for the same architectural pattern: agents, skills, hooks, commands, rules and MCP configurations are separated into reusable workflow components. citeturn0search0turn1search0

The current upstream ECC material also documents cross-platform support and reusable `SKILL.md` definitions, with security, verification and specialized-agent workflows. citeturn1search7turn1search9

Engineering interpretation: skills are not merely prompt snippets. They should be versioned workflow modules with scope, prerequisites, tool requirements, risk class and verification criteria.

### E. OpenCode / Kilo / Antigravity reinforce provider-neutral agentic development

The supplied final screenshot groups Antigravity, Kilo Code and OpenCode as alternative agentic coding environments. Current documentation supports the broader architectural observation:

- Kilo Code exposes IDE/CLI/cloud/mobile surfaces, specialized agents, MCP, granular permissions and provider/model selection. citeturn2search0turn2search6turn2search9
- OpenCode exposes reusable agents, on-demand `SKILL.md` skills, MCP management and a provider layer supporting many hosted and local providers. citeturn1search12turn1search13turn2search8turn2search13
- Google Antigravity is documented as an agentic development platform / command center for launching, monitoring and orchestrating multiple agents. citeturn2search16

Engineering interpretation: P100 should model the **agent harness** independently from the model provider, skill catalog, MCP layer and authorization boundary.

## Canonical pipeline derived from the corpus

```text
VISUAL DISCOVERY
      ↓
REFERENCE CAPTURE
      ↓
PROVENANCE / USAGE CHECK
      ↓
DESIGN SIGNAL EXTRACTION
      ↓
DESIGN SPEC / TOKENS / COMPONENT MAP
      ↓
SKILL + AGENT SELECTION
      ↓
REFERENCE-TO-CODE COMPILATION
      ↓
MOTION / INTERACTION INTEGRATION
      ↓
BUILD / LINT / TYPECHECK / TEST
      ↓
VISUAL REGRESSION + RESPONSIVE QA
      ↓
ACCESSIBILITY + PERFORMANCE QA
      ↓
SECURITY / SUPPLY-CHAIN GATE
      ↓
ARTIFACT + PROVENANCE
      ↓
PROMOTION
```

## New architectural primitive: Design Reference Graph

P100/P40 should treat a visual reference as a graph rather than a screenshot:

```yaml
DesignReferenceNode:
  id:
  source:
  capture:
  visual_tokens:
  layout_primitives:
  components:
  motion:
  typography:
  imagery:
  interaction:
  responsive_rules:
  usage_basis:
  provenance:
  confidence:

DesignReferenceEdge:
  kind: inspires|implements|contains|animates|variants|derived_from|verified_by
  source:
  target:
  confidence:
```

This permits multiple references to contribute to one page without allowing a single copied page to become an unexamined implementation specification.

## New architectural primitive: Skill Contract

A reusable frontend skill should expose:

```yaml
SkillContract:
  id:
  version:
  trigger:
  inputs:
  outputs:
  allowed_tools:
  required_context:
  side_effects:
  risk:
  compatibility:
  verification:
  provenance:
```

This extends the existing P100 provider/skill registry and the portfolio-wide distinction between capability availability and authorization.

## Security invariants

- screenshot ≠ source code;
- copied HTML ≠ permission to redistribute;
- visual similarity ≠ legal equivalence;
- component prompt ≠ trusted code;
- installed skill ≠ authority;
- connected provider ≠ authorization;
- tool success ≠ verified UI state;
- generated UI ≠ production-ready UI;
- external benchmark/showcase ≠ local QA evidence.

## Project mapping

| Signal | Primary project | Secondary projects | Impact |
|---|---|---|---|
| reference-first web design | P100 | P33, P40 | HIGH |
| 21st.dev prompt/component workflow | P100 | P40, P16 | HIGH |
| HTML/DOM reference capture | P40 | P100, P33 | MEDIUM-HIGH |
| reusable frontend skills | P100 | P16, P24 | HIGH |
| agent harness separation | P100 | P17, P31, P40 | HIGH |
| Kilo/OpenCode/Antigravity comparison | P100 | P17, P40 | MEDIUM-HIGH |
| visual regression / responsive QA | P40 | P28, P72 | HIGH |

## New-project decision

**NO NEW NUMBERED PROJECT.**

The corpus is a direct extension of existing agentic development, visual intelligence, prompt-compilation and verification lineages. The correct action is to strengthen P100/P40/P33/P16 rather than create another overlapping web-design project.

## Evidence boundary

The images are treated as user-supplied visual evidence. Current product/repository behavior was separately checked only where it materially affects architecture. Volatile counts, labels and marketing claims visible in screenshots are not promoted to durable facts.
