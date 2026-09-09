# Project Genesis — Iteration 10 — OmniCore Self-Evolving Computing Substrate

## Decision

**Create Project 80.**

## Candidate evaluated

`OmniCore Self-Evolving Computing Substrate MAX`

## Why it is not a duplicate

Project 61 converges the OmniCore kernel, Omnis compiler and PUI. Project 68 governs the unified runtime. Project 72 verifies agent/runtime behavior. Project 79 autonomously selects scientific experiments.

Project 80 introduces a distinct deliverable: a controlled experimental substrate in which the **computing system itself becomes the subject of the discovery loop**.

The new control relationship is:

`Project 79 discovery controller → Project 80 system variants → Project 72 assurance → measured release → new evidence`.

## Source support

The uploaded corpus provides concrete architectural primitives rather than only a conceptual OS description: Rust bare-metal kernel prototypes, AI scheduling, SemanticFS, x86/AArch64 HAL, AI-generated drivers, MLIR hybrid memory, CIRA, MeshBus, 3DGS/PUI and a QEMU/GPU agent forge. The kernel prototype explicitly contains boot, scheduler, SemanticFS and MeshBus stages. fileciteturn311file0L10-L30

The source also defines an AI Foundry workflow for hardware discovery, documentation retrieval and generated driver synthesis, while repository doctrine requires generated low-level code to remain untrusted until verification. fileciteturn313file15L764-L769

## Novelty test

| Criterion | Result |
|---|---|
| New domain capability | YES — self-evolution of the computing substrate |
| Independent deliverable | YES — variant laboratory + promotion/rollback loop |
| Reusable beyond one project | YES |
| Builds on existing projects | YES |
| Duplicates existing project | NO |
| Verification path | YES — QEMU/HIL/benchmarks/formal/assurance |
| Safety boundary | YES — no direct model authority |

## Breakthrough boundary

The project is intentionally framed as a research program. It does not claim that a self-improving OS has already been achieved. A world-scale result would require independently replicated evidence that the closed loop produces durable, generalizable improvements that human-designed baselines do not reliably discover.

## Required first demonstration

A minimal credible demonstration is not autonomous rewriting. It is:

1. freeze a deterministic OmniCore baseline;
2. define a reproducible workload suite;
3. generate at least two competing scheduler/runtime variants;
4. execute them in isolated QEMU environments;
5. measure performance, fairness, reliability and resource use;
6. independently reproduce the strongest result;
7. stage the winner;
8. verify health;
9. demonstrate rollback.

Only after this baseline experiment should broader compiler, driver, MeshBus and PUI evolution be enabled.
