# Project 100 — NeXus AI Code OMEGA-X Agentic Development Environment MAX

## Status
PROPOSED → ARCHITECTURE BASELINE → PROJECT GENESIS 2026-09-10

## Mission
Build the concrete NeXus AI Code developer environment that federates the repository's agentic development, multimodal interaction, model engineering, MCP, DGM-H/RSI and verification capabilities into one inspectable VS Code/Electron product.

## Why this is distinct
P40 owns the provider-neutral agentic development and live-world execution fabric. P61 owns OmniCore convergence. P80 owns the self-evolving computing substrate. P87 owns the Nexus hybrid language/compiler. P98 owns general-intelligence capability research and evaluation. P100 is the concrete product/integration shell that exposes these capabilities to an operator through one developer environment.

## Source-derived product surface
The supplied NeXus sources specify or report:
- NeXus AI Code branding and Polish-first UI;
- luxury obsidian/gold/copper/platinum visual system;
- multi-model chat including cloud providers and local GGUF;
- simultaneous primary + auxiliary GGUF loading with sampling/context/GPU-layer controls;
- OCN single-agent and swarm invocation;
- OCN 9-file agent registry with Meta/Main/Basic tiers;
- voice chat, camera/desktop vision, microphone/STT/TTS and GUI actuation;
- Rust + Zenoh low-latency sidecar architecture;
- MCP server for a workspace/disk;
- Tor browser integration as an optional capability;
- Unreal/Unity/Android automation targets;
- model training with llama.cpp/Unsloth-oriented tooling;
- DGM/RSI and FunSearch-style code evolution;
- quantum/system telemetry dashboard and task queues;
- Code ↔ Diff views and fitness visualization;
- multiple VS Code extensions federated under one product.

Reported implementation evidence in the source includes 13 installed extensions, successful TypeScript compilation/deployment for several components and a launched Electron instance. These reports are treated as source evidence, not independently reproduced verification.

## Canonical architecture

```text
                    OPERATOR
                       ↓
              NE XUS / POLISH UI
                       ↓
             INTENT + CONTEXT LAYER
                       ↓
        ┌──────────────┼───────────────┐
        ↓              ↓               ↓
   MODEL HUB       OCN SWARM       WORLD/VOICE
        ↓              ↓               ↓
   GGUF/CLOUD      AGENT REGISTRY    VISION/AUDIO/HID
        └──────────────┼───────────────┘
                       ↓
                CAPABILITY BROKER
                       ↓
              MCP / FILE / CLI / GUI
                       ↓
             SANDBOXED EXECUTION
                       ↓
          AUTHORITATIVE READBACK
                       ↓
        VERIFY / AUDIT / ARTIFACT LEDGER
                       ↓
             DGM-H CANDIDATE LOOP
                       ↓
        TEST → VERIFY → STAGE → ROLLBACK
```

## 1. Model Hub

Manage heterogeneous model providers and local GGUF files through a common adapter contract.

### Dual-model mode
- **Główny** — primary reasoning/generation model.
- **Pomocniczy** — secondary model for critique, routing, vision, coding or specialized assistance.

Configuration includes temperature, top-p, top-k, context length and GPU-layer allocation where supported. Actual runtime configuration must be read back from the active backend rather than inferred from UI labels.

## 2. OCN Agent Registry

Preserve the source's 9-file standard:

```text
definition.json
SKILLS.md
SUPER_SKILLS.md
ULTRA_SKILLS.md
SUPER_HOOKS.md
System_prompt.md
TOOLS.json
SUPER_TOOLS.json
ULTRA_TOOLS.json
```

Agent tiers:
- Basic: 11 / 22 / 33 skills and tools;
- Main: 33 / 66 / 99;
- Meta: 111 / 222 / 333.

These numbers are registry targets, not automatic proof of actual capability.

Support:
- direct agent invocation;
- swarm invocation;
- role-based routing;
- capability discovery;
- versioned agent definitions;
- bounded tool exposure.

## 3. Multimodal / embodied layer

The OMEGA-X source defines four functional interfaces:

`VISION → AUDIO IN → AUDIO OUT → ACTUATION`

The implementation boundary is:

`OBSERVE → PLAN → AUTHORIZE → ACT → READBACK → VERIFY`.

Vision and audio observations are provenance-bearing inputs. GUI actions are not considered successful solely because an input event was emitted.

## 4. MCP workspace fabric

Expose workspace capabilities through typed contracts for:
- read;
- write;
- list/search;
- move/copy/delete;
- execution;
- git operations;
- Python/runtime inspection;
- environment information;
- bounded HTTP access where explicitly authorized.

Every capability declares side effects, scope, approval requirement, quota and verification method.

## 5. DGM-H / RSI integration

DGM-H is integrated as a **candidate evolution subsystem**, not as an unrestricted privileged self-modifier.

```text
OBSERVE PERFORMANCE
 ↓
GENERATE CANDIDATES
 ↓
PARALLEL EVALUATION
 ↓
FITNESS / TESTS
 ↓
SECURITY + FORMAL VERIFICATION
 ↓
SANDBOX
 ↓
STAGED PROMOTION
 ↓
POST-RELEASE READBACK
 ↓
ROLLBACK IF REGRESSION
```

FunSearch-style population, tournament selection, crossover and mutation are supported as research/engineering patterns. Candidate code remains untrusted until verification.

## 6. God-Level/OCAA research adapters

P100 may expose experimental adapters for:
- Code World Models;
- MARS object/meta reasoning;
- hierarchical memory concepts;
- neuro-symbolic verification;
- AlphaEvolve-style search;
- bitemporal project memory;
- predictive resource/behavior estimation.

These adapters are explicitly marked experimental until reproducible validation exists.

## 7. UI / Design System

The source-defined visual contract uses obsidian, glass-like panels, platinum/rhodium borders, gold/copper accents, restrained typography and inline SVG icons. Polish labels are first-class product strings. The status indicator communicates model/runtime activity without pretending that UI state is authoritative.

Representative source tokens include `#0A0A0C`, `#D4AF37`, `#B87333`, platinum/rhodium border values and `JetBrains Mono` / `Inter`. fileciteturn779file0L9-L43

## 8. Extension federation

Target extension families from the supplied implementation record:

```text
nexus-agent-ocn
nexus-ai-hub
nexus-dgm
nexus-code-evolution
nexus-mcp
nexus-sensory
nexus-tor
nexus-trainer
nexus-voice-commander
nexus-quantum-dashboard
nexus-world-panels
nexus-luxury-theme
nexus-pl-language
```

The architecture treats extensions as modular capabilities under a single product control plane, not as independent competing agent authorities.

## 9. Security model

Trust hierarchy:

```text
MODEL OUTPUT                 = UNTRUSTED PROPOSAL
RETRIEVED DATA               = UNTRUSTED UNTIL VALIDATED
UI STATE                     = PROJECTION
TOOL RESULT                  = OBSERVATION
CAPABILITY BROKER            = AUTHORIZATION BOUNDARY
SANDBOX                      = EXECUTION ISOLATION
VERIFIER                     = PROMOTION BOUNDARY
AUTHORITATIVE READBACK      = FACTUAL STATE
AUDIT LEDGER                 = EVIDENCE
```

Required controls:
- least privilege;
- capability allowlists;
- short-lived credentials where applicable;
- network egress restrictions;
- sandboxing;
- postcondition verification;
- turn supersession;
- cost/time/tool budgets;
- immutable audit correlation;
- staged release and rollback.

## 10. Integration map

- **P24** — intent/prompt compilation.
- **P27** — compound reasoning and disagreement analysis.
- **P28** — verified code-generation boundary.
- **P37** — sovereign local/edge/cloud runtime.
- **P40** — agentic development and live-state execution fabric.
- **P54** — cognitive/adversarial security.
- **P57** — multimodal intelligence and interfaces.
- **P59** — autonomous execution/control fabric.
- **P61** — OmniCore convergence and PUI/runtime substrate.
- **P65** — autonomous systems/agentic OS factory.
- **P72** — cross-framework assurance.
- **P80** — self-evolving computing substrate.
- **P87** — Nexus hybrid language/compiler.
- **P90** — SOP/process compilation.
- **P91** — persona/style controls.
- **P97** — multimedia production.
- **P98** — general-intelligence research/evaluation.

## 11. Verification program

1. Full extension compile matrix.
2. Clean-install and upgrade/rollback tests.
3. Model-provider adapter conformance tests.
4. Dual-GGUF load/switch/recovery tests.
5. OCN registry schema and capability-count validation.
6. Single-agent vs swarm orchestration tests.
7. MCP scope/authorization/postcondition tests.
8. Vision/audio/GUI action replay with authoritative readback.
9. DGM-H candidate isolation and rollback tests.
10. Telemetry accuracy and actual-execution metering.
11. UI localization and SVG rendering regression tests.
12. Cross-platform Electron packaging tests.
13. End-to-end task replay: intent → plan → execution → verification → artifact.

## 12. Definition of Done

P100 reaches the next maturity gate only when:
- the product builds reproducibly;
- all enabled extensions pass integration tests;
- model and capability state are authoritative and inspectable;
- consequential actions have policy + postcondition verification;
- DGM-H candidates cannot bypass verification;
- failures are recoverable and auditable;
- reported performance is independently reproduced;
- the NeXus UI remains a projection of authoritative system state.

## Maturity
Architecture-ready product/integration concept. Source reports of installed extensions, successful builds, latency and RSI remain to be independently reproduced in the repository's verification environment.

## Derived from
P24, P27, P28, P37, P40, P54, P57, P59, P61, P65, P72, P80, P87, P90, P91, P97, P98.

## Primary source witnesses
- `NeXus AI Code.md`
- `NeXus AI Code2.md`
- `NeXus AI Code3.md`
- `Architektura OMEGA-X Multimodalny Agent ASI oparty na języku Rust, Zenoh i DGM-H.md`
- `Architektura i Rozwój Systemu Nexus AI Code.md`
- `God Level.md`
