# OmniCore Learned Kernel Lab

## Status
Research-grade architecture and prototype roadmap.

## Purpose
Turn the OmniCore vision into a testable systems-engineering program rather than treating an AI-controlled operating system as a monolith.

## Core architecture

```text
Intent / PUI
     |
Policy + Safety Gate
     |
AI Supervisor ----> Telemetry / Evaluation
     |
Deterministic Scheduler Interface
     |
Microkernel / no_std Rust
     |
Drivers / memory / IPC / hardware abstraction
```

The source material proposes a Rust `no_std` microkernel, SASOS-style memory architecture, and an AI Supervisor for predictive process scheduling. It also explicitly requires avoiding `unsafe` except where hardware MMIO makes it necessary and avoiding floating-point state in kernel scheduling paths. Treat these as design requirements to validate experimentally, not as already-proven implementation facts. fileciteturn206file0L43-L70

## Maximum-practical improvement

The first production-safe version does **not** put an unconstrained LLM in Ring 0. The learned component produces bounded scheduling-policy candidates, while a small deterministic kernel enforces memory safety, capability checks, deadlines, watchdogs and fallback scheduling.

### Execution modes

1. **Baseline:** deterministic scheduler only.
2. **Shadow:** learned scheduler predicts but cannot affect execution.
3. **Constrained control:** learned policy selects among statically validated actions.
4. **Adaptive control:** online learning only inside a bounded policy envelope.
5. **Research mode:** experimental kernel changes execute in isolated emulation/simulation only.

## Evaluation

Measure latency, throughput, fairness, tail latency, deadline misses, CPU overhead, policy instability, recovery time and worst-case behavior against deterministic baselines.

## Safety invariants

- AI cannot directly issue arbitrary privileged instructions.
- Every policy output is typed and range-checked.
- Watchdog-triggered fallback always returns control to the deterministic scheduler.
- Kernel state mutations are transactional and auditable.
- Training data and telemetry are isolated from trusted kernel state.

## Research extensions

Explore AI Foundry for driver synthesis, semantic system interfaces, and perception-driven UI only after the deterministic substrate is stable. The broader OmniCore material explicitly describes a transition from static OS abstractions toward adaptive kernel, middleware and interface layers. fileciteturn206file1L22-L32