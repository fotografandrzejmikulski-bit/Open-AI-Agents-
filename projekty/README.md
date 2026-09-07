# Projekty — Expanded Design Lab

This directory contains project artifacts upgraded using the project's accumulated knowledge base: OpenAI Agents SDK, MCP, coding-agent patterns, AI application builders, formal verification, adversarial AI security, distributed execution, multimodal systems, model engineering, adaptive reasoning, research orchestration, and the source materials supplied by the project owner.

## Engineering standard

Every project is treated as an engineered system, not a prompt-only prototype. The default target is:

- explicit product and system boundaries;
- deterministic contracts and typed schemas;
- agent/tool/MCP separation;
- durable state and resumability;
- authentication and authorization at the capability boundary;
- sandboxed execution for untrusted work;
- human approval for consequential side effects;
- observability, evaluation and auditability;
- reproducible builds and versioned artifacts;
- graceful degradation and recovery;
- an escape hatch from visual builders to inspectable source or explicit runtime contracts;
- evidence/hypothesis separation for research claims.

## Project portfolio

| Project | Scope | Primary objective |
|---|---|---|
| `01-apeiron-black-system-max.md` | Interactive creative system | Upgrade the Aperion/Black System concept into a deterministic, accessible, agent-addressable application |
| `02-vericoding-agent-security-lab.md` | AI security + compiler research | Combine architecture enforcement, taint/effect analysis, adversarial evaluation and proof gates |
| `03-nexus-cognitive-infrastructure.md` | Heterogeneous AI infrastructure | Build a substrate-neutral orchestration architecture for practical and experimental accelerators |
| `04-ai-native-operating-system.md` | AI-native runtime | Prototype AI-assisted scheduling, generated adapters and perceptual interaction with deterministic safety boundaries |
| `05-apeiron-neuroadaptive-interface-safe.md` | Physical/digital creative interface | Preserve the visual concept while eliminating covert persuasion and dark-pattern mechanisms |
| `06-cognitive-security-red-team.md` | Cognitive security | Detect hidden directives, manipulation patterns and stateful adversarial interaction sequences |
| `07-agentic-creative-studio.md` | AI application/content builder | Turn natural-language intent into verified applications and creative artifacts |
| `08-paulaOS-agentic-personal-os.md` | Personal agent system | Build a proactive, privacy-first operating layer with explicit consent and bounded memory |
| `09-omnicore-learned-kernel-lab.md` | Learned-kernel systems research | Test predictive scheduling and AI-assisted OS primitives behind deterministic safety boundaries |
| `10-sovereign-ai-local-first-stack.md` | Local/edge AI infrastructure | Build provider-independent local-first inference with privacy-aware routing and remote fallback |
| `11-model-engineering-and-qlora-lab.md` | Open-weight model engineering | Create a reproducible QLoRA/adapter pipeline with dataset, evaluation and rollback controls |
| `12-cognitive-security-and-adversarial-evaluation.md` | Defensive AI security | Convert hidden directives, Chain-of-Attack and adversarial-model research into a stateful evaluation platform |
| `13-agentic-software-factory.md` | Agentic software engineering | Create a staged factory for requirements, architecture, coding, verification, security and release |
| `14-gemini-3-adaptive-reasoning-multimodal-agent.md` | Multimodal reasoning agent | Dynamically route reasoning depth, preserve tool-call state, exploit multimodal analysis and verify outputs |
| `15-universal-research-orchestrator.md` | Scientific/research agent | Coordinate domain experts, evidence collection, hypothesis generation and falsification in resumable runs |
| `16-prompt-laboratory-and-evaluation-engine.md` | Prompt engineering | Generate structured prompt variants and select them through reproducible evaluation rather than intuition |
| `17-adaptive-model-router.md` | Multi-model infrastructure | Route requests by capability, privacy, quality, latency and cost with verification-driven escalation |

## Cross-project architecture

```text
                    USER / OPERATOR
                           │
                    Intent / Requirements
                           │
                  ┌────────▼─────────┐
                  │ CONTROL PLANE    │
                  │ Specs / Policy   │
                  │ Evals / Approval │
                  │ Provenance       │
                  │ Routing Policy   │
                  └────────┬─────────┘
                           │
          ┌────────────────┼────────────────┐
          │                │                │
      Agent Runtime      MCP/Tools      Knowledge
          │                │                │
          └────────────────┼────────────────┘
                           │
                 EXECUTION / SANDBOX
                           │
            ┌──────────────┼──────────────┐
            │              │              │
         Software       Data/Cloud     Heterogeneous
         Systems        Services        Substrates
            │              │              │
            └──────────────┼──────────────┘
                           │
               OBSERVABILITY / EVALS
                           │
                  VERSIONED ARTIFACT
```

## Security doctrine

The project portfolio explicitly treats covert persuasion, hidden directives, jailbreaks and unauthorized behavioral influence as security concerns. Defensive analysis may model such techniques, but project implementations must not use them to covertly manipulate people or bypass safety controls.

The supplied research on hidden commands and Chain-of-Attack is therefore translated into detection, provenance, stateful adversarial evaluation and regression testing rather than operational bypass recipes.

## Research doctrine

The supplied ASI/Nexus and AI-native OS documents contain a mixture of engineering concepts, forward-looking claims and speculative hardware assertions. These projects preserve the architecture as hypotheses and require independent measurement before any claimed performance advantage is treated as fact.

The OmniCore materials similarly present a learned kernel, NPS and AI Supervisor as target architecture; implementation is staged through shadow-mode, constrained control and research-only experiments rather than direct unconstrained model authority in privileged kernel paths.

## Model engineering doctrine

Local model projects preserve the distinction between base model, tokenizer, dataset, adapters, merged artifacts and serving runtimes. Fine-tuning work must include dataset validation, reproducibility, evaluation, rollback and explicit safety regression suites.

## Reasoning doctrine

Reasoning depth is treated as a resource to allocate, not a constant. Fast paths are preferred for simple tasks; deeper reasoning is introduced when task complexity, uncertainty or consequence level justifies it. Model-specific internal reasoning representations remain implementation details and are never treated as a user-facing source of truth.

## Research-orchestration doctrine

Deep research uses source planning, parallel expertise, adversarial critique, provenance tracking, falsification and resumability. A synthesis is accepted only when claims are traceable to evidence and uncertainty is explicitly represented.

## Lifecycle

`research → architecture → prototype → verification → hardening → evaluation → deployment → monitoring → revision`

A completed project should have:
- source specification;
- implementation or prototype;
- threat model;
- test/evaluation suite;
- deployment definition;
- rollback/recovery path;
- provenance/evidence record.

## Absolute-maximum rule

"Maximum" means measurable engineering quality, not unbounded autonomy. Every increase in agent capability must be accompanied by stronger state management, authorization, isolation, evaluation and recovery.
