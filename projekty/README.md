# Projekty — Expanded Design Lab

This directory contains project artifacts upgraded using the project's accumulated knowledge base: OpenAI Agents SDK, MCP, coding-agent patterns, AI application builders, formal verification, adversarial AI security, distributed execution, multimodal systems, model engineering, adaptive reasoning, research orchestration, prompt optimization, Google AI developer patterns, OmniCore/Nexus systems research, verified code generation, the Sugra data/MCP fabric, Skills, dynamic tool discovery, MCP Apps, sovereign execution and the source materials supplied by the project owner.

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
- evidence/hypothesis separation for research claims;
- external data capabilities with provenance, freshness and quota semantics;
- versioned Skills and bounded capability discovery;
- minimum-necessary tool exposure through filtering/deferred loading;
- defensive influence-security controls for manipulation-oriented attack surfaces.

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
| `18-gemini-3-max-cognitive-agent.md` | Multimodal reasoning + coding agent | Dynamically allocate reasoning, use measurable visual computation and keep application state explicit |
| `19-omniscience-research-orchestrator-max.md` | Research orchestration | Convert deep questions into evidence graphs, adversarial expert review, hypotheses and falsification tests |
| `20-adaptive-prompt-lab.md` | Prompt optimization | Treat prompts as versioned artifacts optimized against frozen evaluation and robustness suites |
| `21-google-ai-sovereign-developer-stack.md` | Google AI developer stack | Combine local/edge inference, cloud reasoning, agentic orchestration, multimodal compute and verification |
| `22-agentic-media-forge-multimodal-studio.md` | Multimodal production | Build a provenance-aware production pipeline for image, video, audio and visual analysis |
| `23-legacy-migration-cira-graph-engine.md` | Legacy modernization | Use AST/CFG/DFG/PDG graphs, CIRA and verification gates for safe modernization |
| `24-agentic-prompt-compiler-and-dsl.md` | Prompt compiler / DSL | Compile natural-language intent into typed, evaluable and policy-aware agent programs |
| `25-portfolio-integration-control-tower.md` | Portfolio governance | Federate project manifests, capabilities, evidence, routing, evaluation and release policy |
| `26-omnicore-trustworthy-kernel-and-agentic-safety-lab.md` | OmniCore trust + AI security | Harden the OmniCore vision with deterministic trust boundaries, capability brokering, verified generation and multimodal adversarial evaluation |
| `27-omnicore-compound-reasoning-and-self-consistency-engine.md` | Adaptive reasoning | Allocate bounded compute across cached context, parallel solvers, self-consistency, disagreement analysis and escalation |
| `28-omnicore-ai-foundry-verified-code-generation.md` | Verified code generation | Turn AI Foundry into a contract-first, provenance-aware, formally assisted generation and promotion pipeline |
| `29-sugra-agentic-data-and-research-fabric-max.md` | External data + MCP | Make Sugra a governed, provenance-aware, quota-aware evidence and data plane for research and agent operations |
| `30-omnicore-sugra-evidence-osint-control-fabric.md` | External evidence + OSINT + control | Integrate Sugra, evidence graphs, freshness/partiality gates, quota-aware planning and Zero-Trust MCP execution into the OmniCore control plane |
| `31-omnicore-sovereign-agent-operating-fabric-max.md` | Agent OS + Skills + MCP + security | Unify agent operating-system abstractions, dynamic capability discovery, versioned Skills, sovereign execution, multimodal security and adaptive hardware into one control-plane architecture |

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
                  │ Reasoning Budget │
                  │ Data Freshness   │
                  │ Quota Budget     │
                  │ Capability Risk │
                  │ Skill Version   │
                  └────────┬─────────┘
                           │
          ┌────────────────┼───────────────────┐
          │                │                   │
      Agent Runtime      Knowledge         Capability
          │             / Evidence           Catalog
          │                │                   │
          └────────────────┼───────────────────┘
                           │
                 REASONING / PLANNING
                           │
                   TOOL / SKILL SEARCH
                           │
                    VERIFIED PLAN
                           │
                 CAPABILITY BROKER
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

## Reasoning doctrine

Reasoning depth is treated as a resource to allocate, not a constant. Fast paths are preferred for simple tasks; deeper reasoning is introduced when task complexity, uncertainty or consequence level justifies it. Model-specific internal reasoning representations remain implementation details and are never treated as a user-facing source of truth.

Project 27 operationalizes this doctrine through bounded compound reasoning, cached context, multiple solver paths, disagreement detection and escalation. The supplied research emphasizes inference-time compute, context caching, RAG and agentic workflows as architectural levers rather than assuming that model size alone determines system performance. fileciteturn16file4L185-L196

Project 31 extends this into an operating-fabric model: the planner can search and load only the capability definitions needed for the current task, then allocate reasoning and tool budget under policy. The OpenAI tooling documentation explicitly supports tool search and deferred loading for large tool surfaces. fileciteturn24file1L1294-L1348

## Research doctrine

Deep research uses source planning, parallel expertise, adversarial critique, provenance tracking, falsification and resumability. A synthesis is accepted only when claims are traceable to evidence and uncertainty is explicitly represented.

Project 29/30 supplies the external evidence plane through the Sugra data/MCP fabric, while Project 31 adds general capability discovery and a unified Observation → Inference → Plan → Effect model.

## Agent Operating Fabric doctrine

The portfolio now treats an agent runtime as an operating substrate with explicit cognitive system calls:

```text
agent_syscall(intent)
agent_alloc(reasoning_budget)
agent_mount(skill)
agent_search_tool(namespace)
agent_call(capability)
agent_checkpoint(state)
agent_verify(result)
agent_commit(artifact)
```

This is an architectural abstraction inspired by the supplied AIOS-style analysis: LLM system calls, agent scheduling, context management, memory/storage management and tool management are separated rather than embedded ad hoc in each agent. fileciteturn15file2L35-L68

## Skills doctrine

Skills are treated as **versioned executable knowledge**, not harmless prompt fragments. A Skill may contain instructions, scripts and assets; its content can influence planning, tool use and command execution. The current OpenAI documentation therefore treats Skills as privileged code and instructions, recommends developer-level integration and requires explicit approval/policy controls for sensitive actions. fileciteturn28file0L14-L24 fileciteturn28file0L540-L568

Portfolio invariant:

```text
SKILL
 ↓
PROVENANCE
 ↓
VERSION
 ↓
REQUIRED CAPABILITIES
 ↓
RISK CLASS
 ↓
EVALUATION
 ↓
MOUNT
```

## Capability discovery doctrine

Large catalogs are searched rather than blindly imported. The preferred sequence is:

```text
TASK
 ↓
CAPABILITY SEARCH
 ↓
MINIMAL TOOL SET
 ↓
DEFINITION LOAD
 ↓
SCHEMA / POLICY CHECK
 ↓
AUTHORIZED CALL
```

This applies to MCP servers, function namespaces and Skill-backed tools. The `allowed_tools` mechanism provides an explicit minimum-capability filter for MCP servers. fileciteturn25file0L491-L514

## OmniCore adaptive capability doctrine

The new OmniCore materials reject forced pixel parity between devices and instead define adaptive fidelity: behavioral identity is preserved while rendering varies with hardware capacity. fileciteturn23file2L21-L35 fileciteturn23file2L39-L46

The portfolio generalizes this to:

```text
SAME INTENT
   ↓
HARDWARE / NETWORK / PRIVACY PROFILE
   ↓
ADAPTIVE CAPABILITY PLAN
   ├─ mobile
   ├─ workstation GPU
   ├─ edge NPU
   ├─ local CPU
   └─ remote accelerator
```

Policy, authorization and provenance remain invariant across profiles.

## Security doctrine

The portfolio treats covert persuasion, hidden directives, jailbreaks and unauthorized behavioral influence as security concerns. Defensive analysis may model such techniques, but implementations must not use them to bypass safety controls or covertly manipulate users.

The supplied Gemini security research distinguishes jailbreak from prompt injection and places application compromise at the boundary between untrusted input and privileged tool execution. fileciteturn23file5L39-L56

The supplied influence-oriented reports are therefore incorporated as a **defensive Influence Security** discipline. Visual persuasion, dependency loops, coercive control, propaganda/narrative engineering and social manipulation become detection and evaluation signals rather than objectives. fileciteturn15file0L15-L33 fileciteturn23file6L16-L27 fileciteturn23file7L14-L28 fileciteturn23file8L16-L24

## Behavioral evidence doctrine

The supplied behavioral-analysis research explicitly rejects the idea that a single gesture, microexpression or physiological cue proves deception. fileciteturn23file9L9-L23

Accordingly, the portfolio requires:

```text
OBSERVATION
 +
INCONSISTENCY
 +
ALTERNATIVE EXPLANATIONS
 +
CONTEXT
 +
CONFIDENCE
 →
HYPOTHESIS
```

No binary “truth detector” is considered an authoritative decision mechanism.

## OSINT / evidence doctrine

Deep OSINT is modeled as an iterative research loop in which discovered public data can become new pivot points, while scope, legality and provenance remain explicit. fileciteturn250file2L38-L55

The resulting control path is:

```text
RESEARCH QUESTION
      ↓
TARGET / SCOPE
      ↓
SOURCE PLAN
      ↓
PUBLIC / PASSIVE DATA
      ↓
ENTITY RESOLUTION
      ↓
PIVOT GENERATION
      ↓
EVIDENCE GRAPH
      ↓
COUNTER-CHECK
      ↓
REPORT
```

Active interaction with external infrastructure remains authorization-sensitive; capability does not imply permission.

## Multimodal trust doctrine

Text, image/OCR, audio/transcript, video, web content, logs, history, memory, Skills and MCP metadata are all treated as potentially untrusted input classes.

```text
MULTIMODAL INPUT
      ↓
NORMALIZATION
      ↓
PROVENANCE
      ↓
CLASSIFICATION
      ↓
CONTEXT ISOLATION
      ↓
POLICY / CAPABILITY CHECK
      ↓
REASONING
```

This unifies the supplied multimodal Gemini security research with the portfolio's existing prompt-injection defenses. fileciteturn23file5L16-L31

## MCP and remote-service doctrine

Remote MCP servers are independent trust domains. The OpenAI documentation warns that a malicious remote MCP server can exfiltrate sensitive data entering model context, and recommends careful review of server trust and data sharing. fileciteturn25file0L210-L213

The portfolio therefore applies:

```text
SERVER IDENTITY
 ↓
TOOL INVENTORY
 ↓
ALLOWED TOOLS
 ↓
APPROVAL POLICY
 ↓
DATA EGRESS CHECK
 ↓
CALL
```

Approval is a control-plane decision, not an informal model preference. fileciteturn25file0L691-L705

## UI doctrine

MCP Apps is the standards-first UI layer. Data tools remain useful without UI; render tools are separated from data processing; authoritative business state remains server-side; widget state is presentation state. fileciteturn25file1L1028-L1054 fileciteturn25file1L1160-L1193 fileciteturn25file1L1375-L1415

For networked UI, CSP allowlists remain narrow and explicit. fileciteturn25file1L1684-L1695

## Sovereign hardware doctrine

The Zero-Trust hardware material introduces a hardware root of trust, secure boot, attestation and strict compartmentation as foundations for sovereign systems. fileciteturn250file3L8-L24

Project 31 extends the trust chain:

```text
HARDWARE ROOT OF TRUST
        ↓
SECURE BOOT
        ↓
VERIFIED KERNEL
        ↓
VERIFIED AGENT RUNTIME
        ↓
VERIFIED SKILL / TOOL BUNDLE
        ↓
VERIFIED POLICY
        ↓
AUDITED EXECUTION
```

AI remains outside the immutable trust root.

## Software factory doctrine

Autonomous software engineering is treated as a staged production system rather than unrestricted code generation:

```text
INTENT
 ↓
ARCHITECT
 ↓
IMPLEMENTER
 ↓
TESTER
 ↓
SECURITY REVIEW
 ↓
VERIFIER
 ↓
REPAIR
 ↓
RELEASE GATE
```

The market and engineering reports describe coding agents that plan, modify code, run tests, inspect failures and iterate; Project 13/28/31 keeps these actions inside bounded sandboxes and promotion gates. fileciteturn23file0L35-L48

## Release doctrine

The plugin/agent release process requires accurate tool metadata, security review, domain/authentication checks and reviewer-oriented positive/negative evaluation. The current submission documentation requires at least five positive and three negative test cases. fileciteturn28file2L824-L838 fileciteturn28file2L1079-L1098

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

“Maximum” means measurable engineering quality, not unbounded autonomy. Every increase in agent capability must be accompanied by stronger state management, authorization, isolation, evaluation and recovery.
