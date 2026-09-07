# Master Project Architecture — Agentic Application + Vericoding Foundation

**Status:** Design baseline / implementation target  
**Version:** 0.1.0  
**Date:** 2026-09-07  

## 1. Executive architecture

The strongest synthesis of the accumulated material is a platform in which an AI application is not represented as a prompt alone. It is a versioned system composed of:

```text
PRODUCT EXPERIENCE
Web / Mobile / Voice / Admin / Builder
             |
             v
APPLICATION API / DOMAIN SERVICES
             |
      +------+------+
      |             |
      v             v
 AGENT RUNTIME   DETERMINISTIC WORKFLOWS
      |             |
      +------+------+
             |
             v
       CAPABILITY BUS
    Tools / MCP / APIs
             |
    +--------+--------+
    |        |        |
    v        v        v
  DATA     SANDBOX  EXTERNAL SYSTEMS
    |        |        |
    +--------+--------+
             |
             v
  INFRASTRUCTURE / DEPLOYMENT
             |
    +--------+--------+
    |                 |
 OBSERVABILITY       EVALS
```

The project combines the strongest concepts identified across the ecosystem: MCP as a capability protocol; Agents SDK-style agent/tool/guardrail/session abstractions; graph/state runtimes for durable workflows; visual builders as control planes; coding agents as repository-aware execution harnesses; and the Lechia concept of compiler-enforced architecture and security.

## 2. Core architectural principle

**Probabilistic reasoning must terminate at a deterministic contract boundary.**

The model may choose what to do, but the runtime decides what is structurally and operationally allowed.

```text
LLM proposal
   |
   v
typed intent
   |
   v
policy / authorization
   |
   v
validated tool contract
   |
   v
execution sandbox or approved capability
   |
   v
observable result
```

This prevents prompts from becoming hidden business logic and prevents an agent from silently escalating its authority.

## 3. Three-plane separation

### Control plane
Owns agent definitions, prompts/instructions, tools, policies, versions, evaluations, approvals, deployments and audit records.

### Execution plane
Runs model turns, tool calls, code execution, workflows and long-running tasks. Untrusted execution must be sandboxed and isolated from production credentials.

### Data plane
Owns authoritative business state, files, databases, knowledge stores and external-system records. The agent context is only a projection of this state.

## 4. Agent contract

Every production agent should be serializable as a versioned manifest:

```yaml
agent:
  id: example-agent
  version: 1.0.0
  objective: "..."
  instructions: "..."
  model: "..."
  tools:
    - capability.read_records
    - capability.propose_change
  policy:
    max_steps: 20
    side_effect_mode: approval_required
  state:
    conversation: durable
    task: checkpointed
  evaluation_suite: agent-regression-v1
  environment: staging
```

This turns the agent into an inspectable artifact rather than an opaque configuration in a UI.

## 5. Capability model

Tools are semantic capabilities, not implementation details.

Preferred progression:

`discover → validate → authorize → execute → verify → audit`

Read-only and mutating capabilities must be distinct. Prefer `get`, `search`, `propose_update`, `apply_approved_update` instead of unrestricted `write_database`.

MCP should sit at this boundary. It provides interoperability, discovery and execution semantics; it is not the place to hide orchestration policy or business-state ownership.

## 6. State model

Separate state into:

1. **ephemeral context** — current model input and temporary tool output;
2. **task state** — durable checkpoint for a running job;
3. **conversation/session state** — multi-turn history and session notes;
4. **business state** — authoritative records in domain storage;
5. **knowledge state** — indexed documents and retrieval metadata;
6. **audit state** — immutable record of consequential actions.

No safety-critical invariant should exist only in conversation memory.

## 7. Recovery-first execution

Long-running tasks should be modeled as recoverable state machines:

```text
PLANNED
  ↓
RUNNING
  ↓
WAITING_FOR_TOOL / WAITING_FOR_APPROVAL
  ↓
VERIFYING
  ↓
COMMITTED
```

Failure transitions should support retry, compensation, rollback or safe abort.

Successful intermediate work must survive interruption where practical. Approval is a state transition, not a UI-only boolean.

## 8. Compiler-inspired safety layer

The Lechia source proposes a valuable design direction: move architectural constraints into the compilation/validation pipeline rather than relying on human discipline.

The practical modern interpretation is a **Vericoding gate**:

```text
AI-generated patch
      |
 AST / type analysis
      |
 effect analysis
      |
 architecture rules
      |
 taint/security checks
      |
 unit/integration tests
      |
 formal proofs for selected invariants
      |
      v
  promotion gate
```

This should be implemented incrementally. Full dependent-type verification of arbitrary business software is a research target; typed schemas, static analysis, effect boundaries and formal proofs for critical invariants are the practical near-term foundation.

## 9. Lechia-derived language ideas worth prototyping

The source material proposes:

- Polish/domain-oriented syntax with canonical semantic normalization;
- immutable-by-default state;
- actor/process isolation and message passing;
- pattern matching with exhaustiveness checking;
- preconditions/postconditions expressed as dependent constraints;
- effect-aware architecture rules;
- semantic duplicate detection using AST normalization plus embeddings;
- cyclomatic/cognitive complexity as build-time constraints;
- taint-aware SQL/HTML security types;
- content-addressable code concepts;
- MLIR-oriented intermediate representations.

These ideas are strongest as a research compiler/toolchain project rather than as assumptions about current production compiler technology.

## 10. AI safety architecture

The safety material contributes a threat model centered on alignment and control failures:

- reward hacking;
- wireheading;
- specification gaming;
- instrumental convergence;
- corrigibility and shutdown resistance;
- unsafe exploration;
- distribution shift;
- prompt/tool injection;
- excessive agency.

Engineering response:

```text
Goal
 ↓
Policy constraints
 ↓
Capability scoping
 ↓
Action simulation / validation
 ↓
Human approval where required
 ↓
Execution
 ↓
Outcome verification
 ↓
Audit / evaluation
```

Never rely on the model's self-reported safety as the sole enforcement mechanism.

## 11. Coding-agent mode

The repository-aware coding-agent loop should remain explicit:

`inspect → plan → patch → format/typecheck → test → review → patch again`

Repository instructions, tool permissions, sandbox boundaries and verification commands belong to the harness around the model.

A builder may generate the initial project, but the repository remains the durable source of truth.

## 12. Builder integration strategy

The application can use multiple builder classes simultaneously:

- prompt-to-full-stack builders for initial product scaffolding;
- UI generators for presentation surfaces;
- visual app builders as operator/admin control planes;
- AI IDEs for repository-scale changes;
- agent runtimes for autonomous behavior;
- MCP servers for capability interoperability;
- sandbox infrastructure for risky execution.

The architecture must prevent vendor-specific state from becoming the only source of truth.

## 13. Multi-agent policy

Do not multiply agents merely because a framework supports multi-agent orchestration.

Split an agent only when one or more of these materially diverge:

- system instructions;
- tool permissions;
- risk policy;
- model requirements;
- output contract;
- context requirements;
- evaluation criteria.

Otherwise prefer a single agent plus deterministic workflow decomposition.

## 14. Evaluation architecture

Every promoted agent version should have:

```text
Golden tasks
+ adversarial tasks
+ tool correctness tests
+ policy/security tests
+ regression traces
+ latency/cost budget
+ human review samples
```

Evaluation is a continuous loop:

`traces → failure clusters → new evals → implementation change → re-run → promotion`

## 15. Deployment architecture

Use at minimum:

```text
dev → preview/staging → production
```

Agent sandboxes are separate from all three when executing untrusted code.

Secrets must be environment-scoped and injected through runtime credential boundaries, never embedded in prompts, source artifacts, tool results or logs.

## 16. Data and knowledge architecture

Use a retrieval stack in which:

```text
ingestion → normalization → indexing → retrieval → grounding → citation → evaluation
```

The agent should receive the minimum context required for the task. Large undifferentiated context windows are not a substitute for memory architecture.

## 17. Prototype roadmap

### Phase A — deterministic core
Build typed domain objects, capability registry, policy engine, audit log and state machine.

### Phase B — agent runtime
Add one agent, one model, selected tools, sessions and tracing.

### Phase C — MCP boundary
Expose capabilities through a governed MCP server and validate interoperability with an MCP client.

### Phase D — sandbox
Add isolated coding/file execution with explicit mounts, permissions and resource limits.

### Phase E — vericoding gate
Add static architecture rules, taint analysis, complexity gates and proof checks for critical invariants.

### Phase F — durable orchestration
Add checkpoints, resumable approval states, retries, compensation and long-running task handling.

### Phase G — builder control plane
Expose web/mobile/admin surfaces using a visual builder or generated frontend while preserving the same backend contracts.

## 18. Maximum-quality acceptance criteria

A project is not considered production-ready merely because an agent can complete a demo task. It must also demonstrate:

- deterministic schemas;
- capability-level authorization;
- safe failure behavior;
- durable state for long jobs;
- testable generated code;
- observable traces;
- reproducible builds;
- security and prompt-injection defenses;
- explicit human-approval boundaries;
- environment isolation;
- rollback or compensation strategy;
- evaluation coverage;
- documented assumptions and evidence quality.

## 19. Source-derived caveat

Several supplied documents deliberately push beyond conventional engineering into speculative hardware, ASI, novel compute substrates and future systems. Those concepts are retained here as research hypotheses and architectural inspiration, not as established technical facts. The practical project boundary is to extract the transferable engineering patterns while marking unverified scientific or commercial assertions as hypotheses requiring external validation.
