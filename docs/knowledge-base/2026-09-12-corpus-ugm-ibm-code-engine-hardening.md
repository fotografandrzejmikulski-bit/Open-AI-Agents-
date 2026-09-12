# Knowledge Corpus — UGM / IBM Code Engine Hardening

Date: 2026-09-12
Source: user-provided audit findings and `bridge_policy.py` excerpt.
Evidence class: source-derived audit observations; repository state was not independently located in the current search, so findings below are not presented as independently reproduced defects.

## Findings absorbed

### 1. Hatchling src-layout packaging

The source flags `packages = ["src/ugm"]` as potentially incorrect for the intended Hatchling `src` layout and proposes `packages = ["src"]` or auto-discovery. This must be verified against the exact Hatchling configuration and project tree before changing it.

Control: build a wheel/sdist in CI and test installation/import of `ugm.app` from a clean environment.

### 2. Ruff S101

The source flags an explicit ignore of Ruff S101. `assert` must not be used as a production authorization, security, input-validation or state-integrity mechanism because optimized Python execution can remove assertions.

Control: security/business invariants use explicit exceptions/validation; retain S101 enforcement unless a narrowly justified test-only exception exists.

### 3. Container ownership

The source identifies root-owned `COPY` operations followed by `USER 10001` as a possible runtime permission issue. Proposed control: use `COPY --chown=appuser:appuser` where application files need to be read/written by the non-root runtime user.

Control should also distinguish read-only application code from intentionally writable paths; do not grant broad write permissions merely to hide an ownership defect.

### 4. Fail-closed bridge token policy

The source requires the bridge to fail closed when `UGM_BRIDGE_TOKEN` is missing. The critical verification target is whether `app.py` actually invokes the policy path and whether missing credentials cause denial/fail-fast rather than a warning-only path.

### 5. Shell script rigor

`scripts/bootstrap_ibm_cloud.sh` and `scripts/one_command_deploy.sh` should use `set -euo pipefail` and explicit error handling. CLI failures must not silently permit subsequent deployment steps.

### 6. Terraform state

The source identifies absence of a remote Terraform backend as a collaboration/CI reliability risk. A remote state backend with appropriate locking/consistency semantics and access controls should be evaluated for the IBM Cloud deployment.

### 7. CI/CD resource parity

The source flags a mismatch between `--memory 4G` in a local deployment script and `--memory 1G` in GitHub Actions. This should be resolved by defining a single source of truth for deployment resources and testing the actual workload's memory envelope, rather than blindly copying 4G into CI.

### 8. Dead policy engine

The supplied `BridgePolicyEngine` defines:

- default-deny risk classification;
- risk levels L0–L4;
- step/tool-call/delegation/time budgets;
- prompt-injection policy flags;
- credential policy;
- approval + `action_hash` requirements for L3/L4.

The critical audit finding is that a policy class can become dead code if `ChatGPTBridgeRuntime` does not instantiate it and route every consequential action through `authorize_execution`, `validate_budget` and `validate_credentials`.

Control:

`REQUEST → AUTHENTICITY → SCHEMA → POLICY ENGINE → AUTHORIZATION → TOOL → READBACK → VERIFICATION`

No mutating path may bypass the policy engine.

## Important semantic correction

The excerpt's credential detector (`"AIza"`, `"Bearer "`, `"sk-"`) is only a heuristic and cannot be treated as complete secret detection. Production controls should use secret managers, workload identity, structured secret redaction and provider-specific credential handling.

Likewise, `action_hash` proves binding/integrity only if its construction, scope, freshness and verification are defined. A hash by itself is not authorization.

## Portfolio integration

Primary strengthening: **P100 — Nexus enterprise agentic control plane / DevSecOps**.

The findings reinforce:

- fail-closed authorization;
- policy engine liveness;
- no bypass paths;
- secure container execution;
- CI/CD reproducibility;
- Terraform state governance;
- shell-script failure semantics;
- package/build verification;
- secret isolation;
- resource configuration as a controlled deployment contract.

Secondary relationship: P119 where the bridge becomes a mobile/local agent gateway.

## New invariants

- `ASSERTION ≠ SECURITY CONTROL`
- `POLICY CODE ≠ ENFORCED POLICY`
- `MISSING SECRET ≠ WARNING-ONLY STATE`
- `ROOT-OWNED ≠ RUNTIME-WRITABLE`
- `LOCAL TFSTATE ≠ SAFE SHARED STATE`
- `SCRIPT CONTINUATION ≠ DEPLOYMENT SUCCESS`
- `MEMORY CONFIG ≠ VERIFIED CAPACITY`
- `ACTION HASH ≠ AUTHORIZATION`
- `SECRET HEURISTIC ≠ SECRET DETECTION`
- `BUILD SUCCESS ≠ INSTALLED-PACKAGE IMPORT SUCCESS`
