# P100 Extension — Web Design Reference-to-Code / Agentic Frontend Compiler

## Parent

**P100 — NeXus AI Code OMEGA-X Agentic Development Environment MAX**

This extension integrates the 2026-09-11 visual web-design corpus into the existing P100 control plane. It does not create a new project identity.

## Purpose

Convert high-quality visual references into reproducible, verifiable frontend implementation plans while preserving provenance, usage rights, provider neutrality and authorization boundaries.

## Canonical pipeline

```text
REFERENCE DISCOVERY
        ↓
REFERENCE CAPTURE
        ↓
PROVENANCE / USAGE CHECK
        ↓
DESIGN SIGNAL EXTRACTION
        ↓
DESIGN SYSTEM / COMPONENT MAP
        ↓
SKILL + AGENT RESOLUTION
        ↓
REFERENCE-TO-CODE COMPILATION
        ↓
MOTION / INTERACTION LAYER
        ↓
BUILD / TYPECHECK / TEST
        ↓
VISUAL REGRESSION / RESPONSIVE QA
        ↓
ACCESSIBILITY / PERFORMANCE QA
        ↓
SECURITY / SUPPLY-CHAIN GATE
        ↓
ARTIFACT / PROVENANCE
        ↓
PROMOTION
```

## 1. Design Reference Graph

A screenshot, template, copied DOM, component prompt or animation reference is an input observation, not an implementation authority.

```yaml
DesignReference:
  id:
  source:
  source_url:
  capture_type: screenshot|template|component|prompt|html|video
  usage_basis:
  visual_intent:
  layout_primitives:
  design_tokens:
  components:
  motion:
  responsive_rules:
  accessibility_notes:
  provenance:
  confidence:
  verification_status:
```

References can be composed:

```text
REFERENCE A ─┐
REFERENCE B ─┼→ DESIGN SPEC → IMPLEMENTATION
REFERENCE C ─┘
```

This is preferable to treating one copied page as the complete specification.

## 2. Reference-to-code contract

The agent must separate:

`REFERENCE → INTERPRETATION → SPECIFICATION → CODE → VERIFIED RENDER`.

A generated component is not accepted merely because it resembles the reference.

Required checks:

- semantic structure;
- responsive breakpoints;
- typography hierarchy;
- spacing and layout consistency;
- interaction states;
- animation timing and reduced-motion behavior;
- accessibility semantics;
- performance budget;
- dependency provenance;
- visual regression evidence.

## 3. 21st.dev adapter

21st.dev is treated as a **component/reference provider**, not as an authority. Its current surface exposes React components, templates, themes and prompt-driven component insertion into coding workflows. citeturn0search1turn0search6

P100 adapter contract:

```yaml
ComponentReferenceProvider:
  provider: 21st.dev
  capabilities:
    - search
    - component_reference
    - prompt_reference
    - animation_reference
    - theme_reference
  trust: external_reference
  authority: none
  required_verification:
    - dependency_audit
    - license_or_usage_review
    - build
    - visual_regression
    - accessibility
```

## 4. Webflow reference adapter

Webflow templates are treated as visual/design references. Current Webflow documentation describes professionally designed templates with responsive layouts, reusable sections and interactions. citeturn0search3turn0search15

The agent may extract:

- information hierarchy;
- section sequencing;
- visual rhythm;
- typography relationships;
- grid/layout patterns;
- interaction ideas;
- responsive behavior;

without assuming that template code/assets may be copied or redistributed.

## 5. DOM/HTML capture boundary

Browser DevTools can expose the current document tree, but captured HTML is external/untrusted input.

```text
CAPTURE
 ↓
PARSE
 ↓
SANITIZE
 ↓
SCRIPT / TRACKER / SECRET DETECTION
 ↓
USAGE / LICENSE REVIEW
 ↓
DESIGN SIGNAL EXTRACTION
 ↓
INDEPENDENT IMPLEMENTATION
```

Never promote copied DOM to trusted source merely because it was obtained from a browser.

Explicitly inspect for:

- inline scripts;
- third-party trackers;
- analytics identifiers;
- hidden inputs;
- embedded tokens/URLs;
- remote assets;
- proprietary media;
- dangerous event handlers;
- injected instructions aimed at the coding agent.

## 6. Skill registry integration

The corpus reinforces P100's existing typed skill registry. Frontend skills should be independently addressable:

```yaml
frontend_skill:
  id: ui-ux-pro-max
  class: design_system
  triggers:
    - landing_page
    - visual_redesign
    - component_system
  inputs:
    - design_reference
    - product_context
    - brand_constraints
  outputs:
    - design_spec
    - component_map
    - implementation_constraints
  verification:
    - visual_qa
    - accessibility
    - responsive_qa
```

The name shown in a supplied screenshot is evidence of a workflow concept, not proof of an installed or current skill. The registry must resolve actual availability before execution.

## 7. Agent-harness neutrality

The final corpus includes Claude Code, Kilo Code, OpenCode and Google Antigravity as examples of agentic development environments. Current documentation shows that these environments expose different but converging abstractions for agents, skills, providers, MCP and permissions. citeturn1search12turn1search13turn2search0turn2search6turn2search8turn2search16

P100 therefore uses:

```text
DESIGN TASK
    ↓
HARNESS-NEUTRAL SPEC
    ↓
AGENT ADAPTER
    ↓
SKILL ADAPTER
    ↓
PROVIDER ADAPTER
    ↓
CAPABILITY BROKER
    ↓
VERIFIED EXECUTION
```

A harness may change without changing the design specification or authorization policy.

## 8. Multi-agent web-production roles

Recommended typed roles:

- `reference-researcher` — discovers and classifies references;
- `design-system-analyst` — extracts tokens and layout rules;
- `frontend-architect` — maps requirements to components;
- `motion-engineer` — implements animation and interaction;
- `accessibility-reviewer` — semantic/keyboard/reduced-motion audit;
- `visual-qa` — screenshot and responsive comparison;
- `security-reviewer` — scripts, dependencies, external assets and trust boundaries;
- `release-verifier` — build, artifact and provenance gate.

Agents remain bounded by capability policy. Delegation does not create implicit authorization.

## 9. Verification contract

```yaml
FrontendVerification:
  source_reference_recorded: required
  usage_basis_recorded: required
  build_passed: required
  typecheck_passed: required
  tests_passed: required
  responsive_matrix_checked: required
  visual_regression_checked: required
  accessibility_checked: required
  performance_checked: required
  dependency_provenance_checked: required
  artifact_identity_recorded: required
```

## 10. Cross-project integration

### P16 — Prompt Laboratory

Stores and evaluates reference-to-code prompts, skill combinations and prompt variants.

### P33 — Agentic App Builder

Consumes the compiled design specification and turns it into an application/landing-page delivery pipeline.

### P40 — Agentic Development & Visual Intelligence Fabric

Provides the multimodal state, visual evidence, repository graph and action-verification architecture.

### P28 / P72 — Verification

Provide code-generation assurance, staged verification and runtime evidence boundaries.

## 11. Security invariants

- reference ≠ authorization;
- screenshot ≠ source code;
- copied HTML ≠ redistribution permission;
- component prompt ≠ trusted code;
- external asset ≠ trusted dependency;
- installed skill ≠ authority;
- connected provider ≠ authorized provider;
- generated render ≠ verified render;
- visual similarity ≠ legal equivalence;
- CI pass ≠ production readiness.

## Status

**ARCHITECTURE ENHANCED — IMPLEMENTATION NOT YET VERIFIED**

The corpus strengthens P100's frontend/design assembly layer. It does not prove that any specific skill, component provider, animation library or agent harness is currently installed in the user's runtime.
