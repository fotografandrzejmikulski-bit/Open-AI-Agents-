# P121 Extension — InfraSentinel Cloud Memory, MCP, Agent Registry & Neuro-Symbolic Verification

Date: 2026-09-12
Parent: P121 — InfraSentinel-Agentic
Classification: EXISTING PROJECT EXTENSION
Source: user-provided hackathon architecture/application specification

## Purpose

Extend InfraSentinel with the reusable architecture patterns introduced by the supplied Antigravity/MCP/cloud-memory and neuro-symbolic verification material, while preserving P121's SRE-specific authorization, sandbox and postcondition gates.

## Extended control plane

`INCIDENT → AUTHENTICITY/SCHEMA → MEMORY/MCP CONTEXT → POLICY/RISK GATE → AGENT ORCHESTRATOR → RESEARCH → PLAN → TOOL VALIDATION → SANDBOX → READBACK → VERIFICATION → AUDIT`

## Cloud Memory

Three memory classes are adopted as an interoperability model:

- episodic: timestamped incident, diagnosis, remediation and rollback history;
- semantic: infrastructure/documentation/project knowledge and version-aware retrieval;
- procedural: validated `SKILL.md` operational procedures.

Memory retrieval is context, not authority. A memory write is a candidate until provenance, ACL, freshness, correctness and policy checks pass.

Proposed logical record:

`memory_id / timestamp / tenant / ACL / incident_id / source / content / embedding / embedding_model_version / freshness / retention / provenance`

The source's PostgreSQL + vector + temporal-extension configuration is retained as a candidate implementation, not a verified mandatory stack. Exact versions, extensions, index types and embedding dimensions require environment-specific validation.

## MCP federation

Cloud storage and external service connectors are treated as capability adapters:

`MCP → CAPABILITY BROKER → POLICY → AUTHORIZATION → ACTION`

Connector requirements:

- provider and connector identity;
- schema/version;
- transport;
- permissions and side effects;
- tenant/ACL scope;
- limits and timeouts;
- provenance;
- verifier/readback contract;
- lifecycle state.

Retrieved documents must be treated as untrusted data. Instructions embedded in a document cannot silently become agent instructions or privileges.

## Agent roster

The source-described candidates are mapped into P121 as specialist roles:

- `AG_102` — OODA-oriented orchestration and delegation;
- `AG_085` — document/form extraction and validation;
- `AG_113` — infrastructure environment automation.

No roster entry receives authority merely by being registered. Each agent requires identity/version, role, allowed tools, capability leases, memory scope, sandbox profile, resource budget, policy version, evaluation suite and activation state.

## Manager / Mission View

The control surface should project:

`incident / agent / mission / plan / artifact / approval / execution / verifier / runtime`

A UI approval is not itself authorization. Durable approval must bind to task version, artifact hash/version, policy version, capability, actor/session, expiration and replay protection.

## Multi-model routing

P121 adopts provider-neutral routing metadata:

`TASK → MODEL SELECTION → CONTEXT/PRIVACY → COST/LATENCY BUDGET → CAPABILITY REQUIREMENTS → POLICY → EXECUTION → VERIFICATION`

Cloud and local models may serve different roles, but locality, model size or low temperature does not establish correctness or authority.

## Neuro-symbolic verification

A formal or symbolic verifier may validate a defined subset of an agent-generated plan or program and produce counterexamples. P121 requires:

- explicit verification goal;
- modeled scope;
- assumptions;
- input/output contract;
- verifier/tool/version provenance;
- reproducible run;
- counterexample retention;
- independent runtime/postcondition verification.

`FORMAL PROPERTY VERIFIED ≠ WHOLE SYSTEM VERIFIED`

A counterexample can be fed into a bounded repair loop, but automatic repair must return to policy, sandbox and verification rather than becoming self-authorizing.

## LoRA / continuous improvement

The source's LoRA strategy becomes an experimental adaptation lane:

`INCIDENT DATA → PROVENANCE → DATASET VALIDATION → HELD-OUT SAFETY SET → TRAINING CANDIDATE → EVALUATION → REGRESSION/SECURITY CHECK → APPROVAL → DEPLOYMENT`

The supplied hyperparameters are hypotheses, not universal optima. Training loss alone cannot establish SRE improvement.

## Prototype hardening findings

The supplied PoC structure is useful as an architecture demonstration but requires the following controls before production:

- do not use substring checks as the primary destructive-action defense;
- validate tool arguments independently of the LLM;
- separate plan generation from execution authorization;
- prevent raw model-generated shell from directly reaching privileged infrastructure;
- use typed action contracts rather than a single unrestricted `command` string;
- make tool execution idempotent where possible;
- bind actions to environment, tenant and capability scope;
- add timeout/resource/network budgets;
- distinguish retryable tool failure from policy/security failure;
- record immutable execution lineage;
- verify postconditions against authoritative runtime state;
- keep production mutation disabled until adversarial validation passes.

## Security invariants

`MCP ≠ AUTHORITY`

`MEMORY ≠ AUTHORITY`

`SKILL.md ≠ AUTHORIZATION`

`MODEL OUTPUT ≠ AUTHORIZATION`

`GUARDRAIL ≠ COMPLETE SECURITY`

`FORMAL CHECK ≠ WHOLE-SYSTEM PROOF`

`SANDBOX SUCCESS ≠ PRODUCTION SAFETY`

`COMMAND SUCCESS ≠ REMEDIATION SUCCESS`

`REMEDIATION SUCCESS ≠ POSTCONDITION VERIFICATION`

`LOCAL MODEL ≠ AUTOMATICALLY TRUSTED MODEL`

## Epistemic status

Exact claims concerning Antigravity behavior, MCP package names, PostgreSQL/TimescaleDB/pgvector/pgvectorscale versions, Nemotron model specifications, Nebius pricing/API, Tavily parameters, NeMo Guardrails capabilities, LoRA API parameters and hackathon rules remain source-derived until independently verified. The architectural patterns are retained as reusable design candidates.
