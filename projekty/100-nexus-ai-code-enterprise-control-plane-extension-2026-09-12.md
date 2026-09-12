# P100 Extension — NeXus AI Code OMEGA-X Enterprise Control Plane

**Date:** 2026-09-12  
**Parent:** P100 — NeXus AI Code OMEGA-X Agentic Development Environment MAX  
**Decision:** architecture extension; no new project

## Objective

Evolve the P100 product shell from a powerful agentic developer environment into an enterprise-governed distributed agent platform without duplicating existing P100 capabilities.

## Enterprise target architecture

```text
OPERATOR
  ↓
REACT 19 SPA / DESKTOP SHELL
  ↓
OIDC / SSO — KEYCLOAK
  ↓
POLICY + CAPABILITY BROKER — Permit / internal PDP
  ↓
AGENTS BUILDER
  ↓
CANDIDATE ARTIFACT + SCHEMA + TOOL PLAN
  ↓
VALIDATION / RALPH LOOP
  ↓
TEMPORAL DURABLE WORKFLOW
  ↓
EPHEMERAL AGENT IDENTITY / CAPABILITY LEASE
  ↓
MCP / SEARCH / DATA / EXECUTION
  ↓
FIRECRACKER / gVisor / OTHER SANDBOX
  ↓
AUTHORITATIVE READBACK
  ↓
VERIFY / AUDIT / EVIDENCE
  ↓
HUMAN APPROVAL ENVELOPE
  ↓
IDEMPOTENT PROMOTION
  ↓
GLOBAL AGENT REGISTRY + VERSIONED MEMORY
```

## P100 capability additions

### 1. Enterprise Identity Plane

Separate human and agent identities. Human SSO is used for authentication and organizational context; agents receive short-lived, scope-bound capability leases. No agent inherits the full privilege set of its creator.

### 2. Policy Enforcement Plane

Permit.io or an equivalent internal PDP can provide policy decisions, but the authoritative architecture remains the P100 capability broker. Every consequential action must be authorized at the point of execution.

Policy input should include:

`principal + agent + tenant + resource + action + candidate/version + context + policy_version`

### 3. Durable Execution Plane

Temporal becomes the durable orchestration substrate for long-running agent workflows, retries, waiting states and resumable Human-in-the-Loop transitions.

Temporal does not authorize actions and does not replace the capability broker.

### 4. Agents Builder

Agents Builder is promoted to a first-class P100 meta-agent service with the following lifecycle:

`INTENT → REQUIREMENTS → DRAFT → SCHEMA → TOOL PLAN → VALIDATE → SANDBOX → REVIEW → PROMOTE`

The builder may propose:

- role;
- system prompt;
- output schema;
- required tools;
- capability scopes;
- test scenarios;
- resource/time/cost budgets;
- deployment metadata.

The builder cannot grant itself privileges or directly promote its own output.

### 5. Bounded Ralph Execution

Self-correction becomes a bounded workflow:

`GENERATE → TEST → DIAGNOSE → REVISE → RETEST`

Termination conditions:

- all required tests pass;
- maximum iterations reached;
- cost/time budget exhausted;
- policy violation;
- candidate superseded;
- human cancellation.

A passing test does not automatically mean production approval.

### 6. MCP Capability Fabric

MCP remains a transport/capability exposure layer. Every tool registration must declare:

- side effects;
- scope;
- resource class;
- authorization policy;
- required identity type;
- rate/cost limits;
- expected postcondition;
- readback method;
- provenance requirements.

### 7. Smart Search Policy Router

Search routing becomes a policy-controlled capability rather than an LLM-controlled switch.

Candidate routes:

- self-hosted/private search for sensitive internal workflows;
- external deep-research provider where explicitly authorized;
- technical/neural search where appropriate;
- standard web search fallback.

Provider privacy/retention properties must be verified independently.

### 8. Sandboxed Execution Fabric

P100 should federate multiple execution substrates rather than hard-code one runtime:

- Firecracker microVMs for strong workload isolation;
- gVisor for workloads requiring its specific compatibility/security profile;
- WASI/WebAssembly for suitable restricted workloads;
- container isolation only where its threat model is acceptable.

Every sandbox receives a unique execution identity and explicit resource/network limits.

### 9. Enterprise Memory / RAG

Central PostgreSQL + pgvector may serve the enterprise registry and long-term memory, but retrieval must be authorization-aware.

Memory record minimum:

`tenant + principal/agent scope + source + provenance + content + embedding_model + embedding_version + timestamp + retention + ACL metadata`

Embedding dimensionality is selected from the active embedding model contract; it is not globally assumed to be 1536.

### 10. Promotion / Registry

Generated agents are immutable versioned candidates. Human approval applies to one exact candidate digest. Promotion is a separate idempotent server-side operation.

Required invariant:

`APPROVED_CANDIDATE_DIGEST == PROMOTED_CANDIDATE_DIGEST`

If not, promotion fails closed.

## Security invariants

- `MODEL_OUTPUT ≠ AUTHORIZATION`
- `MCP_CAPABILITY ≠ PERMISSION`
- `TEMPORAL_DURABILITY ≠ TRUST`
- `JSON_VALIDITY ≠ CORRECTNESS`
- `SANDBOX_PASS ≠ PRODUCTION_APPROVAL`
- `UI_STATE ≠ AUTHORITATIVE_STATE`
- `TOOL_RESULT ≠ POSTCONDITION`
- `HUMAN_APPROVAL ≠ PERMANENT_PRIVILEGE`
- `STALE_APPROVAL ≠ VALID_APPROVAL`

## Implementation priorities

### P100-E1 — Control-plane contracts

Define typed contracts for principal, agent, candidate, capability, policy decision, workflow run, approval envelope, sandbox execution and promotion transaction.

### P100-E2 — Candidate ledger

Persist immutable candidate manifests and digests before any review or promotion.

### P100-E3 — Durable approval

Implement Temporal wait states with approval expiration, reviewer identity, decision evidence and supersession handling.

### P100-E4 — Capability leases

Issue short-lived agent credentials bound to run/candidate/scope rather than user sessions.

### P100-E5 — Sandbox service

Move untrusted execution out of the API process into a dedicated isolated execution service.

### P100-E6 — Verification gate

Add schema validation, adversarial tests, policy tests, resource-budget tests, sandbox tests and authoritative readback.

### P100-E7 — Enterprise RAG

Add tenant-aware retrieval, provenance, freshness and ACL filtering to the central vector store.

## Code-audit status of supplied bootstrap

The supplied TypeScript is retained as a conceptual bootstrap only. Before implementation it requires syntax/type correction, production secret handling, distributed session strategy, startup dependency checks, real Keycloak/Permit/Temporal integration, complete Firecracker lifecycle control, actual schema validation, proper PostgreSQL parameterization, frontend type corrections and server-side reauthorization of approval actions.

## Definition of Done

P100 Enterprise Control Plane is ready for production evaluation only when:

1. every consequential action has an independently enforced authorization decision;
2. every agent has a distinct, scoped identity;
3. candidate artifacts are immutable and versioned;
4. approvals are bound to exact candidate digests and expire;
5. Temporal workflows are resumable and bounded;
6. generated code runs only in a governed sandbox;
7. MCP tools expose declared side effects and postconditions;
8. RAG retrieval enforces tenant/resource policy before context release;
9. promotion is idempotent and followed by authoritative readback;
10. audit evidence can reconstruct `intent → policy → candidate → execution → approval → promotion → state`.

## Relation to portfolio

This extension consolidates enterprise patterns already distributed across P100, P40, P54, P37, P61, P80 and the MCP/verification corpus. It does not create a new product identity.

**Status:** `enterprise-architecture-integrated`
