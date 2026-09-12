# Knowledge Corpus — Enterprise Agent Platform: Temporal + Keycloak + Permit + MCP + Sandboxing

**Date:** 2026-09-12  
**Trigger:** supplied Enterprise implementation plan and bootstrapping code for a distributed multi-agent platform

## Classification

**Portfolio action:** extend existing P100 / NeXus AI Code OMEGA-X architecture.  
**New project:** no.  
**Primary integration:** P100.  
**Secondary reusable boundaries:** P40 agentic execution fabric, P54 security, P37 sovereign runtime, P61 convergence, P80 self-evolution, and existing MCP/verification primitives.

## Source-derived architecture

The supplied plan proposes five phases:

1. **Monolith decomposition / infrastructure** — independent React 19 SPA, API service, PostgreSQL + pgvector.
2. **Identity / security / authorization** — Keycloak SSO, Permit.io policy enforcement, ephemeral agent identity tokens.
3. **Asynchronous orchestration / durable execution** — Temporal cluster, TypeScript workflows, Human-in-the-Loop via Signals.
4. **Agents Builder / MCP** — meta-agent for intent decomposition, prompt and JSON Schema generation, least-privilege tool assignment, and smart search routing.
5. **Execution isolation** — Firecracker microVMs, with gVisor as an alternative boundary for selected workloads.

The proposed Agents Builder flow is:

`USER INTENT → REQUIREMENTS → AGENT DRAFT → TOOL ASSIGNMENT → SANDBOX TEST → HUMAN APPROVAL → REGISTRY PROMOTION`

The supplied Ralph loop adds:

`TEST → FAILURE LOG → LLM CORRECTION → RETEST → APPROVAL`

## Architectural value for P100

This corpus materially strengthens the existing P100 capability-broker and execution architecture by making several boundaries explicit:

- **human identity != agent identity**;
- **agent identity != inherited user privilege**;
- **MCP capability != authorization**;
- **workflow durability != authorization**;
- **generated JSON != semantic correctness**;
- **sandbox success != production readiness**;
- **approval != permanent privilege**;
- **tool result != authoritative application state**.

Recommended canonical control flow remains:

`OBSERVE → PLAN → AUTHORIZE → ACT → READBACK → VERIFY`

Temporal becomes the durable orchestration substrate around that control flow; it does not become the authorization authority.

## Proposed Enterprise control plane

```text
                         OPERATOR
                            ↓
                    REACT / DESKTOP UI
                            ↓
                    IDENTITY / SSO
                       Keycloak / OIDC
                            ↓
                 POLICY + CAPABILITY BROKER
                    Permit / internal PDP
                            ↓
                    AGENTS BUILDER
                 intent → draft → tools
                            ↓
                   VALIDATION GATE
                 schema / tests / policy
                            ↓
              TEMPORAL DURABLE WORKFLOW
                 pause / retry / signal
                            ↓
             EPHEMERAL AGENT IDENTITY
                            ↓
                 MCP / SEARCH / FILE / API
                            ↓
                 SANDBOX EXECUTION
              Firecracker / gVisor / WASI
                            ↓
                 AUTHORITATIVE READBACK
                            ↓
                    VERIFY + AUDIT
                            ↓
                 HUMAN PROMOTION GATE
                            ↓
                 GLOBAL AGENT REGISTRY
```

## Important source-code audit findings

The supplied bootstrapping snippets are architectural scaffolding, not production-ready code. Several examples contain syntax or type defects and security/configuration placeholders that must be resolved before execution.

### API / Keycloak

- `session.MemoryStore` is not suitable as the production shared session store for a distributed deployment.
- The literal session secret must not exist in source code; production secrets must come from a secret-management boundary.
- Keycloak configuration must be environment-driven and validated against the actual realm/client/issuer configuration.
- `setupTemporal()` is started without awaiting readiness before the HTTP server can accept requests; startup should fail closed if the Temporal dependency is unavailable.
- Authorization must be bound to the authenticated principal and resource/tenant context, not merely a user-subject string.
- The example uses a static `tenant: "default"`; real tenancy must derive from authoritative tenant context and policy.
- Workflow IDs based only on `Date.now()` are weak for idempotency and collision resistance; use a policy-defined idempotency key.

### Agents Builder workflow

- The approval signal is currently a boolean and lacks reviewer identity, decision timestamp, policy version, draft hash, expiration, and reason.
- `condition(() => reviewCompleted)` needs a timeout/expiration path; a permanently waiting workflow is not an adequate governance model.
- The final registry write is described but not actually implemented as a separately authorized, idempotent promotion activity.
- The workflow should persist a candidate artifact/version and promote that exact immutable candidate after approval; it must not regenerate the agent between review and promotion.
- Retry semantics must distinguish transient activities from non-retryable policy/validation failures.

### LLM / structured generation

- `JSON.parse()` is not a semantic validator. Generated output must pass JSON Schema validation plus domain-specific invariants.
- Prompt-injection resistance cannot be achieved solely by instructions inside the generated system prompt. Retrieved content must remain untrusted data and tool access must be enforced outside the model.
- `responseFormat: "json"` does not establish correctness of the resulting object.
- The test harness should validate the complete schema, prohibited fields, tool scopes, side effects, policy requirements, and adversarial scenarios.
- Self-healing must be bounded by retry count, time budget, cost budget and candidate lineage.

### MCP / search routing

The proposed router separates high-privacy, deep-research, technical-documentation and general-search paths. This is a useful policy abstraction, but the `intent` value must not be trusted merely because an LLM supplied it. The capability broker should classify or authorize the route independently.

"Zero Data Retention" must be treated as a provider/service policy claim requiring contractual and runtime verification; routing to self-hosted SearXNG is a privacy architecture choice, not by itself proof that no data leaves the environment.

### Sandboxing

- Firecracker should be integrated through a dedicated privileged sandbox service rather than arbitrary shell calls from the API process.
- The example snapshot copy / Unix socket / resume sequence is illustrative and is not a complete Firecracker lifecycle implementation.
- MicroVM isolation requires kernel, device, filesystem, networking, resource and lifecycle controls; the mere use of Firecracker does not establish complete security.
- GPU workloads require a separate threat model. gVisor is not automatically equivalent to Firecracker isolation and GPU support/limitations must be validated for the exact workload.
- Code execution requires explicit CPU, memory, disk, process, wall-clock, network-egress and output-size budgets.
- Sandbox results are evidence for verification, not automatic authorization for promotion.

### Agent identity

Ephemeral tokens are a strong pattern, but TTL alone is insufficient. The token should be bound to:

- immutable agent/candidate identity;
- workflow/run identity;
- authorized capability set;
- tenant/resource scope;
- issuance policy/version;
- expiry and revocation state;
- correlation/audit identifier.

An agent must never silently inherit all privileges of its human creator.

### React registry / approval UI

The supplied React examples contain type/syntax issues (`useState<AgentData>()` versus an array, missing template literals, missing `Bearer` interpolation, and `isSending` state destructuring). More importantly, the UI must not be the authorization source. The server must re-authorize every consequential action and bind the approval to the exact candidate artifact.

### pgvector memory

- Embedding dimension must be model/version specific rather than hard-coded to 1536.
- Memory records need tenant, source, provenance, ACL/policy metadata, model/version, timestamp and retention semantics.
- Vector retrieval must apply authorization filtering before returning context to an agent.
- Long-term memory is not automatically trusted knowledge; provenance/freshness and access policy are required.
- SQL examples in the supplied snippet are incomplete as literal TypeScript strings and require parameterized, validated implementation.

## Enterprise governance additions adopted by P100

1. **Candidate Artifact ID** — every generated agent receives an immutable candidate/version identity.
2. **Approval Envelope** — approval binds reviewer, policy version, candidate digest, scope and expiry.
3. **Capability Lease** — tool access is leased to a run/agent identity and expires.
4. **Policy Decision Record** — every consequential tool authorization produces auditable evidence.
5. **Sandbox Attestation Record** — records sandbox image/version, limits, inputs, outputs and verification result.
6. **Promotion Transaction** — registry promotion is a separate idempotent authorized action.
7. **Post-Promotion Readback** — authoritative registry state is read back and compared with the promoted candidate.
8. **Bounded Ralph Loop** — self-correction has explicit iteration, time and cost ceilings.
9. **Stale-Approval Rejection** — an approval cannot promote a superseded candidate.
10. **Private Memory Filter** — RAG retrieval enforces tenant/resource authorization before context assembly.

## New reusable primitives

- `enterprise-agent-candidate`
- `approval-envelope`
- `ephemeral-agent-capability-lease`
- `policy-decision-record`
- `durable-human-approval`
- `bounded-ralph-loop`
- `sandbox-attestation`
- `idempotent-agent-promotion`
- `tenant-aware-vector-retrieval`
- `search-intent-policy-router`
- `authoritative-registry-readback`

## Relationship to existing portfolio

This is an **architecture extension**, not P123. P100 already owns the concrete NeXus AI Code / OMEGA-X product shell and already defines a capability broker, sandboxed execution, authoritative readback, verification, audit ledger, MCP fabric, agent registry and staged DGM-H promotion. The supplied Enterprise design fills missing enterprise-grade control-plane details around identity, durable workflow, policy enforcement and agent lifecycle.

## Verification status

**Verified from supplied source:** architectural intent and the exact components proposed by the user.  
**Repository corroboration:** P100 already contains the corresponding capability-broker, MCP, sandbox, readback, verification and agent-registry architecture.  
**Not independently verified:** production readiness of the supplied code snippets, exact library versions, exact Keycloak/Permit/Temporal APIs, Firecracker lifecycle implementation, provider privacy guarantees, or performance claims.
