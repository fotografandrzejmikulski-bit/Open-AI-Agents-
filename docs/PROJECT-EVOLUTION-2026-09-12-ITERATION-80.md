# Project Evolution — 2026-09-12 — Iteration 80

## Input

Expanded InfraSentinel-Agentic hackathon architecture covering Nebius Token Factory, NVIDIA Nemotron, Tavily Agentic Search, NVIDIA NeMo Guardrails/Colang, LoRA, MCP/cloud storage, Cloud Memory, specialist agents, Manager View and neuro-symbolic verification.

## Portfolio decision

**Primary project: P121 — InfraSentinel-Agentic**

**Classification:** existing-project extension.

**New standalone project:** no.

The material deepens the existing SRE vertical instead of defining a separate product lineage.

## P121 additions

- three-class Cloud Memory model: episodic / semantic / procedural;
- temporal/vector memory provenance contract;
- MCP cloud-data federation as capability adapters;
- specialist agent registry for orchestration, document processing and infrastructure automation;
- Manager/Mission View as a state projection over agents, plans, artifacts, approvals, executions and verifiers;
- provider-neutral local/cloud model routing;
- procedural `SKILL.md` lifecycle with provenance and capability-diff checks;
- neuro-symbolic verifier adapter with explicit model scope and counterexamples;
- bounded counterexample-driven repair loop;
- LoRA adaptation lane with held-out safety/regression evaluation;
- stronger typed tool contracts and infrastructure-action validation.

## Prototype hardening

The supplied PoC is treated as an architectural demonstration, not production-ready infrastructure. The following controls are now mandatory design targets:

- unrestricted shell-string tools are not acceptable for privileged production execution;
- substring filtering is not a sufficient security boundary;
- guardrails do not replace authorization;
- model-generated plans require independent validation;
- tool results require authoritative readback;
- production mutations require explicit risk classification, capability scope, rollback and postcondition verification.

## New control flow

`INCIDENT → AUTHENTICATE → OBSERVE → MEMORY/MCP CONTEXT → RESEARCH → PLAN → POLICY → AUTHORIZE → TOOL VALIDATE → SANDBOX → READBACK → VERIFY → AUDIT`

## New invariants

`MCP ≠ AUTHORITY`

`MEMORY ≠ AUTHORITY`

`SKILL.md ≠ AUTHORIZATION`

`MODEL OUTPUT ≠ AUTHORIZATION`

`FORMAL CHECK ≠ WHOLE-SYSTEM PROOF`

`SANDBOX SUCCESS ≠ PRODUCTION SAFETY`

`COMMAND SUCCESS ≠ REMEDIATION SUCCESS`

`REMEDIATION SUCCESS ≠ POSTCONDITION VERIFICATION`

`LOCAL MODEL ≠ AUTOMATICALLY TRUSTED MODEL`

## Evidence boundary

All exact product/model/API/package/version/pricing/competition claims supplied in the source remain SOURCE_DERIVED pending independent verification. Architecture patterns are reusable candidates and are not themselves evidence that a particular vendor implementation currently supports every described feature.

**Status:** `architecture-integrated`
