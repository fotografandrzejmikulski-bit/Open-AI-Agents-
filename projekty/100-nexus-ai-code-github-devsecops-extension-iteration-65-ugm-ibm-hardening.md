# P100 Extension — Iteration 65: UGM / IBM Cloud Engine Hardening

## Purpose

Integrate the supplied UGM bridge audit into the enterprise agent-control and DevSecOps substrate of P100.

## Required control path

`REQUEST → AUTHENTICITY → SCHEMA → POLICY ENGINE → AUTHORIZATION → TOOL → READBACK → VERIFICATION`

Every consequential action must traverse this path. A policy implementation that is not invoked by the runtime is considered ineffective.

## Hardening matrix

| Surface | Required control |
|---|---|
| Hatchling | Validate wheel/sdist installation and `ugm.app` imports from a clean environment |
| Ruff | Do not rely on `assert` for production security/business invariants |
| Docker | Use explicit ownership for runtime-readable/writable paths; remain non-root |
| Bridge token | Missing `UGM_BRIDGE_TOKEN` must fail closed on protected operations |
| Shell | `set -euo pipefail`, explicit CLI error handling and verification |
| Terraform | Remote state and locking/consistency strategy for shared CI/CD operations |
| Code Engine memory | One versioned resource contract; validate actual memory envelope |
| Policy engine | Instantiate and enforce `BridgePolicyEngine` on every mutating path |
| Credentials | Secret manager/workload identity/redaction rather than substring heuristics |
| Action hash | Bind authorization to exact action, context, freshness and approved state |

## BridgePolicyEngine model

The supplied policy model defines L0–L4 risk levels, execution budgets, prompt-injection boundaries, credential policy and approval requirements for high-risk actions.

P100 integration requirements:

1. unknown actions default to deny/high risk;
2. L3/L4 actions require explicit approval and a verified action binding;
3. retrieved content and tool output are data, not instructions;
4. budget checks occur before execution;
5. credentials never enter model context unless explicitly permitted by policy;
6. policy decisions are auditable;
7. policy failures are fail-closed;
8. policy cannot be bypassed through alternate tool adapters.

## CI verification gates

- build wheel/sdist;
- install into clean environment;
- import runtime entry points;
- run Ruff including S101 unless narrowly justified;
- build container and inspect file ownership;
- run as non-root UID;
- test missing-token denial;
- test each risk tier;
- test prompt-injection flags;
- test budget exhaustion;
- test secret-redaction cases;
- force IBM CLI failure and confirm shell stops;
- validate Terraform backend configuration;
- compare deployment resource contract across local/CI paths;
- run mutation-path tests proving policy invocation.

## Architectural doctrine

`POLICY EXISTS ≠ POLICY ENFORCED`

`FAIL-CLOSED ≠ LOG-AND-CONTINUE`

`SECURE CONFIGURATION ≠ VERIFIED RUNTIME`

`NON-ROOT ≠ CORRECT FILE OWNERSHIP`

`REMOTE STATE ≠ AUTOMATICALLY SAFE STATE`

## Relationship to P121

The same policy/verification primitives are directly reusable by InfraSentinel-Agentic for autonomous infrastructure operations. P100 remains the generic control plane; P121 consumes the hardened implementation for SRE operations.
