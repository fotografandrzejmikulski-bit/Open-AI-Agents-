# Omnis Hybrid Language and CIRA — Knowledge Base

## Source provenance
Derived from the supplied Omnis strategy/design materials. The documents are architectural proposals; numerical market, performance and migration claims remain source claims and are not independently validated here.

## Core concepts
- Context-sensitive memory model: affine ownership/RAII, ORC for shared graph/UI structures, isolated tracing GC for dynamic workloads.
- Reified generics, sound gradual typing, explicit nullability and fail-fast dynamic/static boundary checks.
- Significant whitespace, inline multi-line blocks and exhaustive pattern matching.
- MLIR-centered heterogeneous compilation across CPU/GPU/TPU/FPGA/QPU targets.
- Structured concurrency plus actor-style isolated mutable state.
- Universal Graph Registry (UGR) for cross-ecosystem dependency metadata, resolution and virtualization.
- Compiler-Integrated Refactoring Agent (CIRA) for legacy analysis, transformation and verification.

## Engineering interpretation
The strongest reusable pattern is a typed compilation/control plane spanning source languages, dependency graphs, intermediate representations, generated artifacts and verification. The architecture must keep compiler intelligence separate from authorization and release authority.

## Dependency virtualization
UGR is modeled as a dependency graph and compatibility layer. Imported packages are untrusted supply-chain inputs. Capability manifests, provenance, SBOM, vulnerability scanning and sandboxed execution are mandatory before promotion.

## CIRA migration pipeline
`SOURCE → PARSE/AST → CFG/DFG/SEMANTIC GRAPH → TRANSFORM PLAN → GENERATED CODE → BUILD → TEST → EQUIVALENCE/INVARIANT CHECKS → SECURITY CHECKS → SIGN → STAGED PROMOTION`

AI-generated migration is never treated as proof merely because the model reports equivalence.

## Adoption/product boundary
Developer experience can reduce friction and improve flow, but the portfolio does not use covert behavioral pressure, compulsive engagement or dependency engineering. Product adoption must be measurable through transparent value, interoperability and user choice.

## Cross-project links
Connects directly with Projects 13, 23, 28, 31, 33, 37, 39, 40, 41, 49, 60/61 and the software-factory verification stack.
