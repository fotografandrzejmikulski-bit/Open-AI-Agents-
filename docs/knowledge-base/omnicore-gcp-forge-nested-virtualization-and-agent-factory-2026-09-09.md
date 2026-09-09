# OmniCore GCP Forge — Nested Virtualization & Agent Factory

## Source boundary

Consolidated from `Konfiguracja Chmurowej Infrastruktury AI (1).pdf` and `(2).pdf`, which are overlapping infrastructure runbooks for the OmniCore concept.

## Reference architecture

The documents describe a GCP-based `OmniCore-Forge` environment combining nested virtualization, GPU acceleration, local LLM inference, vector retrieval, bare-metal Rust development, QEMU/KVM testing and federated coding agents.

```text
GCP L1 VM
 ├─ QEMU/KVM → L2 kernel test environment
 ├─ GPU → local inference
 ├─ Ollama → model runtime
 ├─ ChromaDB → vector memory
 ├─ RAG / Vision RAG → technical-document retrieval
 └─ MCP → agent coordination
```

## Infrastructure concepts

The source emphasizes choosing hardware that supports nested virtualization and GPU attachment, with N1/Haswell-era configurations presented as the reference scenario. Exact current GCP availability and compatibility are time-sensitive and must be verified against current provider documentation.

The runbook includes an `n1-standard-16` reference, Ubuntu 22.04, NVIDIA T4, large persistent storage, GPU drivers, Docker, Ollama and ChromaDB. These are source-derived configuration examples, not universal requirements.

## Kernel engineering constraints

The proposed `.cursorrules` constitution establishes `no_std`, `core`/`alloc`, panic-abort, explicit safety comments for `unsafe`, fixed-point arithmetic in Ring 0, `x86_64-unknown-none`, driver traits and volatile MMIO access. These are reusable guardrails for AI-assisted systems programming.

## AI Foundry pipeline

The source defines a five-stage concept:

```text
HARDWARE DISCOVERY
 → DOCUMENT RETRIEVAL
 → TEXT/TABLE/VISION EXTRACTION
 → LOCAL LLM ANALYSIS
 → RUST DRIVER GENERATION
 → BUILD/TEST/REPAIR LOOP
```

The pipeline uses PDF extraction/OCR/table tooling, embeddings and ChromaDB before model-assisted code generation. Generated low-level code remains untrusted until compile, emulator, memory-safety and runtime verification.

## Network security

The source recommends private networking and SSH local forwarding for Ollama/ChromaDB rather than exposing those services publicly. MCP is treated as a coordination channel, not an authorization authority. Capability and authorization must be independently enforced.

## Agent federation

The source assigns distinct roles to Cursor, Devin and Windsurf and uses MCP for state/artifact exchange. A reusable version is:

`specialist agent → typed artifact → broker → verifier → shared authoritative state`.

## Mapping

Direct convergence target for OmniCore, AI Foundry, SemanticFS, PUI, MCP orchestration and Project 72 runtime assurance. The two source PDFs are consolidated as one lineage rather than duplicated.