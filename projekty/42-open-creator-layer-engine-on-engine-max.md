# Project 42 — Open Creator Layer MAX

## Thesis
Build an open, engine-neutral creator layer above established game engines, turning natural-language intent and visual graph editing into reproducible, native-engine artifacts without replacing the engine's renderer, physics, asset pipeline or runtime.

## Source-derived foundation
The original Open Creator Layer concept uses an Engine-on-Engine architecture, graph-first navigation, typed visual nodes, Smart Assets, event-driven logic, automated asset setup and an escape hatch to native engine tooling. This is preserved and upgraded into a provider-neutral creator control plane. fileciteturn157file0L2-L2

## Architecture

```text
USER INTENT / REFERENCE IMAGE / VOICE
                ↓
         CREATOR CONTEXT
                ↓
        PROJECT GRAPH / MIND MAP
                ↓
        TYPED DESIGN GRAPH
                ↓
         AI CREATOR AGENTS
        ↙        ↓         ↘
  CODE AGENT  ASSET AGENT  SCENE AGENT
        ↘        ↓         ↙
          ENGINE ADAPTER
                ↓
      NATIVE ENGINE ARTIFACTS
                ↓
      COMPILE / TEST / PREVIEW
                ↓
       PLAYABLE VERIFICATION
                ↓
      SIGNED PROJECT SNAPSHOT
```

## Engine-neutral contract

```yaml
EngineAdapter:
  engine_id:
  version:
  capabilities:
  project_schema:
  import_rules:
  build_targets:
  scripting_surface:
  scene_api:
  asset_pipeline:
  test_hooks:
  export_targets:
```

The creator layer must not encode assumptions that belong exclusively to one engine.

## Graph-first authoring

Everything important is represented as typed graph state:

```yaml
CreatorNode:
  id:
  kind: scene|entity|script|asset|event|logic|material|ui|camera|audio
  inputs:
  outputs:
  constraints:
  provenance:
  version:

CreatorEdge:
  from:
  to:
  relation:
  type:
```

Invalid connections fail before code generation.

## AI multi-agent studio

Specialization is explicit:

- **Architect Agent** — converts intent into project graph and contracts.
- **Code Agent** — generates native scripts/components.
- **Scene Agent** — constructs hierarchy, transforms and world layout.
- **Asset Agent** — imports, validates, tags and prepares assets.
- **Behavior Agent** — creates deterministic state/behavior graphs.
- **Optimization Agent** — profiles frame time, memory and draw-call hotspots.
- **Verifier Agent** — checks contracts, tests and invariants.

The agents share state through the creator graph; they do not mutate each other's opaque private context.

## Native artifact rule

AI-generated changes must resolve to inspectable native artifacts:

`graph → source/assets/config → engine project → build output`.

The visual layer is an authoring surface, not the sole source of truth.

## Smart Asset pipeline

```text
IMPORT
 ↓
IDENTIFY / HASH
 ↓
LICENSE / PROVENANCE CHECK
 ↓
OPTIMIZE / TRANSCODE
 ↓
ATLAS / MATERIAL / LOD PREP
 ↓
ENGINE IMPORT
 ↓
VALIDATE
```

Assets retain provenance and licensing metadata.

## Deterministic build and preview

A creator graph must be reproducibly compiled from a pinned toolchain, engine version and dependency set. Preview runs in a disposable environment before promotion.

## Live world-state integration

The creator layer adopts the Project 40/41 distinction:

`DESIGN STATE ≠ ENGINE STATE ≠ RUNTIME STATE ≠ UI STATE`.

After an AI action, the engine is queried for authoritative state rather than trusting the model's narration of success.

## Action contract

```yaml
Action:
  name:
  arguments:
  preconditions:
  postconditions:
  side_effect_class:
  timeout:
  approval:
```

An editor action is considered successful only after authoritative readback verifies its postcondition.

## Versioning and branching

Every AI edit creates a reversible change set:

```text
BASE SNAPSHOT
      ↓
AI CHANGESET
      ↓
VALIDATION
      ↓
PREVIEW
      ↓
HUMAN REVIEW
      ↓
COMMIT / REVERT
```

Support branching for alternative designs without mutating the canonical project until promotion.

## Security

- engine APIs are capability-scoped;
- arbitrary shell/network access is disabled by default;
- imported assets are untrusted inputs;
- plugins/extensions are versioned and evaluated;
- secrets never enter generated scene/script text;
- external network access uses allowlists;
- project mutation requires path/operation policy;
- packaged builds pass supply-chain gates.

## Performance agent

Optimization is continuous but measurable. Track:

`CPU frame time + GPU frame time + memory + draw calls + asset footprint + load time + crash rate`.

Optimization proposals require before/after measurements and must not silently trade correctness for performance.

## Multiplayer / collaborative extension

Represent edits as structured changesets rather than raw file patches where possible:

`intent → graph delta → conflict detection → merge → compile → verify`.

This enables agent-assisted collaboration without giving one agent implicit authority over another user's work.

## Evaluation

### Creation
- time to first playable;
- graph validity;
- artifact editability;
- successful import/build rate.

### Agent quality
- intent-to-graph fidelity;
- code correctness;
- repair success;
- asset-placement accuracy.

### Runtime quality
- frame-time regression;
- crash rate;
- memory regression;
- state-verification accuracy.

### Safety
- unauthorized mutation rate;
- network-policy violations;
- secret leakage;
- supply-chain rejection rate.

## Definition of Done

Project 42 is complete when a user can describe a game/system, build it through a graph-first creator surface, inspect native engine artifacts, run a verified preview, iterate through reversible AI changes and export a reproducible native project without surrendering control of the underlying engine.
