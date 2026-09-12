# Project Evolution — Iteration 67 — IBM Zenoh / Bitemporal Memory / HRR Native Factory

## Trigger

Second, expanded corpus pass on the IBM Cloud autonomous native-application factory architecture.

## Decision

No new standalone project. The material strengthens the existing cross-project architecture spanning P100, P86, P119 and P121.

## P100 — Nexus AI Code / DevSecOps

Add a formal MCP-to-Zenoh capability boundary preserving caller identity, request identity, capability scope, policy decision, idempotency and provenance across transport translation. Extend RSI governance with independent evaluation and promotion gates.

## P86 — OmniGame / Native Build Factory

Extend the native build abstraction beyond game builds to explicit platform capabilities for Swift/iOS/macOS, Kotlin/Android, Rust/Tauri, Windows and Linux. Host, SDK, signing, emulator and toolchain constraints remain explicit capabilities.

## P119 — OmniMAS Local Android

Adopt the CoALA memory decomposition as an interoperability model: episodic build history, semantic native API/design knowledge and procedural validated build/scaffold procedures. Add bitemporal reconstruction and HRR/vector-symbolic representation as optional memory/indexing layers, not as truth authorities.

## P121 — InfraSentinel-Agentic

Carry forward the control-plane distinction between transport, observation, authorization and execution. Zenoh is a data plane; it cannot confer authorization. Independent readback and postcondition verification remain mandatory.

## New architecture primitives

### Bitemporal memory

`VT` captures validity of a fact or rule; `ST` captures system/transaction history. This enables historical reconstruction and regression analysis while preserving the distinction between temporal provenance and truth.

### HRR / vector-symbolic representation

Circular convolution and FFT can provide a fixed-dimensional representation for structured component relationships. Similarity remains an observation/indexing signal and cannot replace exact retrieval or verification.

### Merkle-DAG + Bloom + CRDT

Use Merkle lineage for content identity, Bloom filters for probabilistic candidate membership, and CRDTs for conflict-tolerant state merging. Exact readback remains mandatory after probabilistic or convergent operations.

### MCP → Zenoh gateway contract

```text
MCP REQUEST
↓
AUTHENTICATE
↓
SCHEMA / CAPABILITY CHECK
↓
POLICY DECISION
↓
ZENOH MESSAGE
↓
EXECUTOR
↓
READBACK
↓
VERIFICATION
```

## Required invariants

`TRANSPORT ≠ AUTHORIZATION`

`MESSAGE ≠ TRUSTED INSTRUCTION`

`MEMORY ≠ AUTHORITY`

`HRR SIMILARITY ≠ TRUTH`

`BLOOM MEMBERSHIP ≠ EXACT MEMBERSHIP`

`CRDT CONVERGENCE ≠ SEMANTIC CORRECTNESS`

`SELF-IMPROVEMENT ≠ SELF-AUTHORIZATION`

`SIGNATURE ≠ SAFETY PROOF`

`BUILD SUCCESS ≠ RUNTIME SUCCESS`

## Verification status

Architecture-level integration recorded. Vendor-specific performance figures, protocol overhead, product availability, exact SDK versions and production SLAs remain unverified source claims until independently measured or documented.
