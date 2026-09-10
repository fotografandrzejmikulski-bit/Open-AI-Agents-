# Project 111 — OmniEnterprise Agentic Platform & Autonomous Development Studio MAX

## Status
PROPOSED → ARCHITECTURE BASELINE

## Mission
Build a multi-tenant enterprise control plane for creating, registering, orchestrating, securing and operating AI agents and autonomous development workflows across local and cloud model infrastructure.

The platform is the enterprise product boundary above concrete developer environments and below the portfolio's shared assurance/convergence substrates.

## Why this is distinct
- **P100** owns the concrete NeXus AI Code developer environment/operator shell.
- **P102** owns enterprise cloud migration, compliance and sovereignty transformation.
- **P72** owns cross-framework runtime assurance.
- **P108** owns operator-facing LLM security validation.
- **P61** owns convergence-substrate architecture.

P111 owns the integrated enterprise platform/control plane: tenant/workspace isolation, global Agent Registry, autonomous Agents Builder, durable orchestration and autonomous development-studio composition.

## Canonical architecture
```text
TENANT / WORKSPACE
        ↓
IDENTITY + POLICY + AUTHORIZATION
        ↓
INTENT / CONTEXT LAYER
        ↓
AUTONOMOUS AGENTS BUILDER
        ↓
AGENT SPEC + JSON SCHEMA + CAPABILITY POLICY
        ↓
SANDBOXED VALIDATION + ADVERSARIAL TESTING
        ↓
GLOBAL AGENT REGISTRY
        ↓
DURABLE ORCHESTRATION / QUEUES / WORKFLOWS
        ↓
MODEL FABRIC ── DATA FABRIC ── MCP FABRIC ── DEV STUDIO
        ↓
AUTHORITATIVE READBACK + POSTCONDITION VERIFICATION
        ↓
AUDIT / EVIDENCE / OBSERVABILITY
```

## 1. Enterprise Workspace

The workspace is the authoritative tenancy boundary. It owns:
- tenant identity;
- users and roles;
- project/workspace scope;
- policy references;
- quotas;
- data residency configuration;
- audit scope;
- agent ownership and lifecycle.

UI state is never treated as authorization state.

## 2. Agents Builder

The Agents Builder converts a natural-language requirement into a versioned agent specification.

```text
INTENT PARSING
 ↓
REQUIREMENT DECOMPOSITION
 ↓
ROLE / SKILL DESIGN
 ↓
SYSTEM PROMPT COMPILATION
 ↓
JSON SCHEMA
 ↓
MINIMUM TOOL SET
 ↓
SANDBOX TEST
 ↓
SECURITY / POLICY VALIDATION
 ↓
REGISTRY PROMOTION
```

Tool assignment follows least privilege. MCP is a capability-integration mechanism, not the authorization authority.

The source architecture explicitly describes iterative testing of generated agents, rejection/correction when tool calls or schemas violate constraints, and registration only after validation. These remain architecture requirements until independently implemented and tested. fileciteturn1006file1L14-L51

## 3. Global Agent Registry

Each agent receives a versioned record containing:
- identity and owner;
- competence description;
- model preference;
- allowed tools/capabilities;
- input/output schema;
- version;
- performance telemetry;
- audit metadata;
- verification status;
- lifecycle state.

The supplied Enterprise material explicitly proposes such a global registry and searchable agent metadata. fileciteturn1006file4L95-L105

## 4. Durable Agent Orchestration

Long-running work is represented as durable state rather than ephemeral chat execution.

Candidate infrastructure from the source corpus includes PostgreSQL/pgvector, Redis, Temporal and queue-based orchestration. The exact technology choice remains an engineering decision to be benchmarked.

Required properties:
- resumability;
- idempotency;
- retries with bounded policy;
- stale-state rejection;
- event/audit trail;
- cancellation;
- rollback;
- deterministic replay where feasible.

## 5. Model Fabric

Federate:
- local GGUF/llama.cpp/Ollama/vLLM-style backends;
- centralized inference servers;
- cloud model providers;
- embedding/retrieval services.

Routing must consider quality, latency, cost, privacy, consequence and availability. A UI-selected model is not evidence that the runtime actually used that model; active configuration requires authoritative readback.

## 6. Autonomous Development Studio

Provide a platform surface for:
- visual workflow composition;
- agent graph editing;
- AST/code generation;
- live device simulation;
- test execution;
- diff/review;
- deployment staging;
- artifact provenance.

P100 remains the concrete developer-environment shell; P111 owns the enterprise composition/control-plane layer.

## 7. Private Execution

The source corpus proposes isolated execution using Firecracker/gVisor-style sandboxing and SSRF protection. P111 requires:
- least-privilege runtime capabilities;
- restricted network egress;
- resource quotas;
- filesystem isolation;
- secret isolation;
- explicit promotion gates;
- kill/cancel semantics.

Generated code and generated agent configurations are untrusted until tested.

## 8. Security and Assurance

Security is integrated as a lifecycle gate rather than a final audit:

`GENERATE → SANDBOX → TEST → ADVERSARIAL VALIDATE → VERIFY → PROMOTE`

P108 provides the dedicated LLM-security test workbench. P72 provides cross-framework assurance. P111 consumes their authoritative outcomes.

## 9. Data Architecture

The Enterprise reports propose separation of frontend, backend and durable state, with PostgreSQL/pgvector-style persistent semantic memory and distributed service architecture. fileciteturn1001file4L20-L39

The platform should distinguish:
- authoritative relational state;
- semantic retrieval indexes;
- transient caches;
- event/audit state;
- generated artifacts;
- evidence packets.

A vector index is never the sole authority for transactional state.

## 10. Observability

Capture:
- model/version;
- latency;
- tokens;
- tool calls;
- workflow state transitions;
- policy decisions;
- failures;
- retries;
- sandbox events;
- verification outcomes;
- resource consumption.

Observability failures must themselves become testable failure states.

## 11. Verification

### Tenant / authorization
- cross-tenant read/write denial;
- privilege escalation tests;
- revoked-access propagation;
- stale-token rejection;
- policy drift detection.

### Agents Builder
- schema validity;
- tool-minimization correctness;
- unsafe-tool rejection;
- sandbox validation;
- reproducibility of generated specifications.

### Runtime
- durable workflow recovery;
- idempotent retries;
- stale-state rejection;
- cancellation and rollback;
- model-routing correctness;
- authoritative postcondition checks.

### Security
- sandbox escape tests;
- SSRF/egress tests;
- prompt-injection regression;
- tool-confusion tests;
- secret-leakage tests;
- resource exhaustion;
- dependency/supply-chain checks.

### Platform
- load and latency benchmarks;
- fault injection;
- data recovery;
- audit completeness;
- evidence integrity;
- deployment reproducibility.

## 12. Definition of Done — Architecture Baseline

- Tenant and workspace boundaries are explicit and independently testable.
- Agents Builder generates versioned specifications with typed schemas and minimum required capabilities.
- Agents are sandbox-tested before registry promotion.
- Global Agent Registry is authoritative for lifecycle metadata.
- Long-running tasks survive process/node failure through durable orchestration.
- Local and cloud models share typed adapter contracts.
- Autonomous development workflows remain subject to policy and verification gates.
- Security outcomes from P108/P72 can block promotion.
- Audit/evidence records are reproducible and distinguish source, inference and verified outcome.

## Evidence classification
**SOURCE-DERIVED:** Enterprise architecture, Agents Builder, Agent Registry, monorepo and sandbox patterns described by the uploaded reports.

**INFERRED:** Their combination constitutes a distinct enterprise platform/control-plane boundary above P100 and alongside P102.

**PROPOSED:** Project 111 requires implementation and empirical validation.

**NOT ESTABLISHED:** No source evidence proves production scalability, absolute security, autonomous reliability or performance superiority.
