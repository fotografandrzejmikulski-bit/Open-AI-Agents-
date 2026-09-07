# 02 — VERICODING AGENT SECURITY LAB

## Status
Concept → prototype architecture.

## Purpose
A research-grade security laboratory for AI-generated software and agents. The project combines the useful engineering ideas found in the supplied material: compile-time architecture enforcement, taint-aware data handling, formal verification, adversarial evaluation, multi-turn attack detection, and explicit human approval boundaries.

## Source-derived inputs

The supplied Lechia document proposes compiler-enforced architecture rules, an effect system, dependent-type contracts, compile-time architecture assertions, semantic duplicate detection, complexity limits and taint-aware security typing. It explicitly positions these mechanisms as alternatives to relying only on human discipline and external CI checks. fileciteturn191file3L666-L700 fileciteturn191file3L718-L750

The supplied Chain-of-Attack document describes multi-turn, semantic, contextual and temporal attack chains, emphasizing that single-turn input/output filtering is insufficient against attacks distributed across conversation history. fileciteturn195file7L44-L65

The GCG report describes adversarial suffix generation as an algorithmic rather than purely semantic attack class and motivates defenses against transferable adversarial perturbations. fileciteturn195file9L19-L32 fileciteturn195file9L41-L48

## Core architecture

```text
Developer Intent
      ↓
Typed Project Specification
      ↓
AST / IR Normalization
      ↓
Architecture Policy Engine
      ├── effect rules
      ├── dependency rules
      ├── complexity rules
      ├── taint rules
      └── contract/proof obligations
      ↓
Agentic Code Generation / Refactoring
      ↓
Adversarial Evaluation Plane
      ├── multi-turn CoA simulation
      ├── prompt-injection regression suite
      ├── adversarial-input fuzzing
      └── tool-abuse tests
      ↓
Formal Verification / Proof Gate
      ↓
Human Approval for high-impact changes
      ↓
Sandboxed Execution
      ↓
Observability + Audit + Reproducible Evaluation
```

## Maximum-grade design principles

1. **Never treat model output as executable authority.** Generated code is an untrusted candidate until it passes deterministic validation.
2. **Architecture is executable policy.** Module boundaries, effects, dependency direction and safety contracts should be machine-checkable.
3. **Security is stateful.** The security engine evaluates current input plus relevant history and tool state, not only one message.
4. **Proof before privileged execution.** High-impact mutations require a machine-checkable proof or a deterministic policy result.
5. **Side effects are capability-scoped.** Read, write, deploy, delete, network and credential capabilities are separated.
6. **Recovery is part of correctness.** Failed runs must be resumable, observable and reversible where possible.
7. **Human review is a runtime state.** Approvals create resumable transitions, not informal UI confirmations.

## Project modules

### A. Lechia-inspired compiler/policy layer
- Canonical AST representation.
- Effect annotations: `pure`, `io-db`, `io-file`, `io-network`, `credential`, `deployment`.
- Dependency graph enforcement.
- Complexity budgets using cyclomatic and cognitive complexity.
- Semantic duplication analysis using normalized AST fingerprints and optional embeddings.
- Taint types for untrusted text, SQL fragments, HTML, shell arguments and tool responses.
- Contract checking for preconditions/postconditions.

### B. Agent security gateway
- Tool registry with risk classification.
- Per-tool authorization policy.
- Input/output guardrails.
- Prompt-injection indicators.
- Conversation-chain risk score.
- Tool sequence anomaly detection.
- Explicit escalation to human review.

### C. Adversarial laboratory
- Multi-turn attack corpus.
- Stateful chain-of-attack tests.
- Cross-model regression matrix.
- Adversarial suffix tests treated as security research fixtures, not as production jailbreak instructions.
- Tool-call abuse scenarios.
- Data-exfiltration simulations.
- Canary secrets and synthetic credentials.

### D. Proof gate
- Formal obligations generated from policy.
- Lean/SMT-compatible verification boundary.
- `proof_required=true` for specified capability classes.
- Block-by-default when verification cannot be established.

### E. Sandbox
- Ephemeral filesystem.
- No production credentials.
- Restricted egress.
- Resource quotas.
- Deterministic run metadata.
- Snapshot/resume support.

## Initial API contracts

### `analyze_project`
Input: repository metadata, policy profile, target environment.
Output: architecture graph, violations, proof obligations, risk score.

### `evaluate_change`
Input: proposed patch, impacted modules, capability scope.
Output: deterministic verdict, static findings, required approvals, proof status.

### `run_adversarial_suite`
Input: suite ID, target model/runtime, isolation profile.
Output: test results, trace references, regression deltas.

### `authorize_execution`
Input: change ID, capability request, actor, environment.
Output: allow / deny / human-review-required with reason codes.

## MVP

1. TypeScript/Python repository scanner.
2. AST dependency graph.
3. Effect/taint rule engine.
4. Cyclomatic complexity gate.
5. Tool-risk registry.
6. Stateful conversation security evaluator.
7. 25 adversarial regression scenarios.
8. Sandbox runner.
9. JSON audit report.
10. CI integration.

## Success criteria

- Every protected tool has a deterministic authorization decision.
- High-impact changes cannot bypass the proof/approval boundary.
- Multi-turn attack attempts are evaluated using conversation state.
- Architecture violations fail before deployment.
- All test outcomes are reproducible from versioned artifacts.

## Safety boundary

This project is explicitly defensive. Adversarial techniques are represented as controlled test classes and regression cases. It does not provide operational instructions for compromising third-party systems or manipulating people.