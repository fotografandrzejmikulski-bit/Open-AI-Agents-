# Project Evolution — 2026-09-12 — Iteration 64

## Input

InfraSentinel-Agentic: user-provided Nebius x NVIDIA hackathon architecture for autonomous SRE/infrastructure incident diagnosis and remediation using Nebius Token Factory, NVIDIA Nemotron, Tavily, NeMo Guardrails, tool calling and sandbox execution.

## Decision

**NEW_PROJECT: P121 — InfraSentinel-Agentic**

The material defines a distinct vertical: cloud/SRE operations with infrastructure-specific incidents, remediation risk tiers, sandbox execution, rollback and postcondition verification. It should consume P100's general agent-control substrate instead of duplicating it.

## New architectural knowledge

- Four-layer split: cognitive / epistemic / protective / execution.
- Live technical retrieval should be version-aware and provenance-bearing.
- Guardrails are one policy layer, not the authorization authority.
- Tool selection and tool arguments require independent validation.
- Infrastructure mutation requires sandboxing, risk classification, authorization and rollback.
- Post-action readback and independent postcondition tests are mandatory for consequential remediation.
- Fine-tuning/LoRA should be evaluated experimentally with held-out incident and safety sets.

## P100 strengthening

P100 gains a concrete SRE vertical validating its generic capability registry, policy gate, tool validation, sandbox, provenance and verification architecture.

## New invariants

`MODEL ≠ AUTHORITY`

`TAVILY RESULT ≠ VERIFIED TRUTH`

`GUARDRAIL ≠ COMPLETE SECURITY`

`TOOL CALL ≠ AUTHORIZATION`

`SANDBOX SUCCESS ≠ PRODUCTION SAFETY`

`COMMAND SUCCESS ≠ REMEDIATION SUCCESS`

`REMEDIATION SUCCESS ≠ POSTCONDITION VERIFICATION`

`TEMPERATURE ≠ DETERMINISM`

`FINE-TUNE ≠ GUARANTEED IMPROVEMENT`

`AUTONOMY ≠ UNBOUNDED ACCESS`

## Verification boundary

The supplied claims about Nemotron specifications, Nebius pricing/API, Tavily behavior, NeMo capabilities and hackathon rules remain source-reported until checked against current authoritative documentation. The included Python is a design/PoC specification, not independently tested production software.
