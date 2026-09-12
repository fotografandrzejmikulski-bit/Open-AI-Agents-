# Knowledge Corpus — InfraSentinel × Antigravity/MCP/Cloud Memory/Neuro-Symbolic Verification

Date: 2026-09-12
Source: user-provided architecture, hackathon application and prototype specification.
Evidence class: SOURCE_DERIVED for exact product/model/API/package/pricing/competition claims; REUSABLE_ARCHITECTURE_CANDIDATE for normalized design patterns.

## Integration decision

Primary project: **P121 — InfraSentinel-Agentic**.

No new standalone project. The material materially strengthens the existing SRE vertical with cloud memory, MCP federation, specialist-agent roles, multi-model routing, Manager View, procedural skills, formal verification and continuous-improvement controls.

## Normalized architecture

`INCIDENT → AUTHENTICATE → OBSERVE → MEMORY/MCP CONTEXT → RESEARCH → PLAN → POLICY → AUTHORIZE → TOOL VALIDATION → SANDBOX → READBACK → VERIFY → AUDIT`

## Memory model

- Episodic memory: incident and execution history.
- Semantic memory: infrastructure/project/documentation knowledge.
- Procedural memory: validated `SKILL.md` procedures.

Memory is evidence/context, not authority. Persistent writes require provenance, ACL/tenant scope, freshness, correctness and policy validation.

## MCP model

Drive/Dropbox-style connectors are provider adapters. MCP exposes capabilities; it does not authorize them. Connector metadata must include identity, schema/version, permissions, side effects, limits, provenance, lifecycle and verifier/readback contract.

## Agent roster model

The source identifies OODA orchestration (`AG_102`), document processing (`AG_085`) and infrastructure automation (`AG_113`) as candidate roles. Registration must not grant privileges. Capability leases, sandbox profiles, budgets and evaluation suites are required.

## Manager View

The manager surface is a projection over missions, agents, plans, artifacts, approvals, executions and verifiers. Approval must be durable and cryptographically/semantically bound to the exact task/artifact/policy/capability/actor context where required; a UI button is not an authorization primitive.

## Neuro-symbolic verification

Formal/symbolic checking can validate a defined model subset and return counterexamples. Counterexamples are valuable repair inputs, but formal verification is bounded by its model and assumptions. It must be followed by runtime readback and independent postcondition verification for infrastructure actions.

## LoRA

The source proposes LoRA for organization-specific incident data. `W' = W + BA` is retained as the standard low-rank adaptation pattern. Supplied hyperparameters are source proposals only and require empirical evaluation with held-out safety/regression sets.

## Prototype assessment

The supplied Python prototype demonstrates intended component boundaries but should not be treated as production-safe implementation. In particular, substring-based destructive-command filtering is insufficient; an unrestricted `command: string` tool contract is too broad for privileged production execution; guardrails cannot replace authorization; and tool success cannot establish remediation success.

## Required P121 hardening

- typed infrastructure action contracts;
- independent argument validation;
- explicit capability/risk leases;
- tenant/environment binding;
- durable approvals;
- sandbox and resource/network budgets;
- immutable execution provenance;
- authoritative runtime readback;
- independent postcondition tests;
- adversarial prompt-injection and tool-abuse evaluation;
- bounded repair loops;
- held-out LoRA evaluation;
- rollback and idempotency.

## Invariants

`MCP ≠ AUTHORITY`

`MEMORY ≠ AUTHORITY`

`SKILL ≠ AUTHORIZATION`

`MODEL OUTPUT ≠ AUTHORIZATION`

`GUARDRAIL ≠ COMPLETE SECURITY`

`FORMAL CHECK ≠ WHOLE-SYSTEM PROOF`

`SANDBOX SUCCESS ≠ PRODUCTION SAFETY`

`COMMAND SUCCESS ≠ REMEDIATION SUCCESS`

`REMEDIATION SUCCESS ≠ POSTCONDITION VERIFICATION`

## Verification boundary

Exact claims about Antigravity, Nemotron, Nebius, Tavily, NeMo Guardrails, database extensions, package versions, pricing and hackathon requirements remain unverified source assertions unless independently checked against authoritative current sources. No claim of winning probability or commercial ROI is inferred from the supplied application narrative.
