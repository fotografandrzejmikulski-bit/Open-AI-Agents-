# Knowledge Corpus — OmniCore / Omnis / Omniscience / Security / Mathematics / Growth — Iteration 19

## Scope

This artifact consolidates the ten uploaded PDFs of 2026-09-10 and records their relationship to the existing knowledge graph and project portfolio. The batch is predominantly corroborating/repeated material rather than ten independent architectural contributions.

## Source families

### 1. OmniCore prototype
The prototype describes a `no_std` Rust kernel with AI Supervisor scheduling, SemanticFS, HAL/binary translation and MeshBus. The source contains an actual PoC-shaped repository layout (`Cargo.toml`, `src/main.rs`, supervisor, filesystem and HAL modules), but the implementation is still a prototype/stub rather than evidence of a production operating system. The AI scheduler, SemanticFS and architecture abstraction are therefore retained as engineering hypotheses and prototype patterns, not verified capabilities.

### 2. OmniCore technical feasibility
The feasibility report frames OmniCore as a synthesis of seL4, WebAssembly/WASI, LLM/RAG and 3D Gaussian Splatting. It identifies GPU integration under a microkernel as the principal integration risk and proposes virtualization/GPU passthrough as the practical bridge. It also describes a voice → Whisper/WASI-NN → LLM/RAG → 3DGS → seL4 flow. Source maturity/TRL claims are preserved as source-derived claims, not independently re-certified here.

### 3. Omnis / PUI / SemanticFS blueprint
The hybrid-language material adds context-sensitive memory management (affine/RAII, ORC, isolated tracing GC), CIRA compiler integration, UGR-backed migration and a personified UI. SemanticFS/LSFS uses semantic embeddings and ANN retrieval rather than traditional filename-first navigation. These concepts reinforce Projects 61, 80 and 87.

### 4. UGR + CIRA migration
The migration material specifies a graph-centric modernization architecture: UGR as a language-independent representation, CIRA as an OODA-loop agent with deterministic graph analysis plus probabilistic LLM reasoning, AST-level transformation, migration playbooks, continuous graph consistency checks, LSP-based IDE integration and RBAC/mTLS/security controls. This is a direct reinforcement of the existing UGR/CIRA lineage rather than a new project boundary.

### 5. Omniscience problem-solving protocol
The Omniscience document defines knowledge injection, domain-specific source selection, multi-persona expert debate and first-principles hypothesis generation. Its architecture is already generalized into Project 94, which separates problem discovery/uncertainty reduction from business-model experimentation in Project 67.

### 6. Open mathematical problems
The mathematics review covers Millennium/Landau-type open problems and emphasizes interdisciplinary methods, AI-assisted exploration and formal verification. It reinforces Project 77 (formalization/verification) and Project 79 (autonomous scientific discovery). Numerical checking is not treated as proof; unverified proof attempts remain unverified.

### 7. AI capability / sovereignty material
The AI-potential document covers local models, RAG/vector memory, recursive agent loops, autonomous tool use and fine-tuning. These are existing capability patterns already represented in Projects 19/27/54/61/72/80. Claims that local models provide unrestricted capability are treated as source framing, not as authorization or safety conclusions.

### 8. Gemini security / bypass material
The Gemini reports describe multimodal prompt injection, context manipulation, persistent-memory poisoning, browsing/tool abuse and agent-worm concepts. They are retained only as defensive threat-model and assurance knowledge. No bypass procedure is promoted into an offensive capability. The key architectural lesson is that model output, memory and tool access must remain distinct from authorization.

### 9. Sovereign AI implementation masterplan
The masterplan describes a local-first development stack using Project IDX, Nix/dev environments, Ollama, Genkit, browser/edge AI and Android-local AI. It reinforces deployment and local-first implementation patterns in Projects 61/80 and the broader sovereign-edge lineage. Tool/model/version claims remain time-sensitive implementation guidance rather than canonical facts.

### 10. Zero-budget growth / marketing
The growth report covers Fogg-style behavior models, viral growth, network effects, AI wrappers and distribution strategies. It also contains material advocating dark patterns, manipulation and aggressive exploitation of platform dynamics. The portfolio retains legitimate growth, experimentation and distribution patterns under Projects 34/66/67 while excluding coercive/deceptive manipulation as an operational objective.

## Cross-corpus synthesis

The strongest reusable pattern across this batch is:

`OBSERVE → REPRESENT → MODEL → GENERATE HYPOTHESES → SPECIALIST/AGENT ANALYSIS → BUILD/TEST → VERIFY → READ BACK AUTHORITATIVE STATE → UPDATE`

This aligns with the existing portfolio doctrine and Project 94. It does not justify another project because the reusable mission boundary already exists.

## Duplicate / lineage decisions

- OmniCore prototype material: absorbed by Projects 61/80.
- OmniCore feasibility material: absorbed by Projects 61/72/80.
- Omnis + PUI + SemanticFS: absorbed by Projects 61/80/87.
- UGR/CIRA migration: absorbed by the existing UGR/CIRA and Project 87 lineage; no new project.
- Omniscience protocol: absorbed by Projects 19/27/79/94.
- Open mathematics: absorbed by Projects 77/79.
- Gemini bypass/security material: absorbed defensively by Projects 54/72.
- Sovereign implementation masterplan: absorbed by Projects 61/80 and sovereign-edge architecture.
- Zero-budget marketing: absorbed by Projects 34/66/67.
- No independent Project 95 is justified by this batch.

## Evidence discipline

The corpus contains architectural proposals, source summaries, prototype code, forecasts and strategic recommendations. None is silently promoted to verified production capability. In particular, prototype code is not equivalent to a bootable production OS; TRL statements remain source-derived; AI-generated migration requires compilation/tests/formal checks; mathematical computational evidence is not a proof; and security bypass descriptions are threat-model inputs only.
