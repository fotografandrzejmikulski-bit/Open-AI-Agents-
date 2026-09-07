# Source Corpus — 2026-09-07

This document records the newly supplied research corpus and the implementation-grade ideas extracted from it.

## Corpus inventory

1. **Tworzenie Zintegrowanej Techniki Wpływu.PDF** — influence psychology, visual rhetoric, persuasion, neuromarketing and defensive media literacy.
2. **Twoj dokument.PDF** — Gemma 3 27B local deployment, hybrid inference, Direct Context Injection, Rclone, MCP and Unity/Unreal integration.
3. **Konfiguracja Gemma 3 LM Studio i Google Drive.PDF** — LM Studio, SearXNG/Open WebUI, Multi-Google Drive, MCP and neuro-symbolic verification.
4. **Dokument B.PDF** — local hardware constraints, performance hypotheses, MCP and verification loop.
5. **Dokument A.pdf** — autonomous engineering architecture, A2A, multimodal workflow, NSVIF and agent orchestration.
6. **Aaa.pdf** — content-product and email/newsletter product ideas.
7. **Bbb.pdf** — large prompt/content pattern collection for blog, persuasion, offers and conversion-oriented content.
8. **GGG.pdf** — AI side-hustle and productized-service concepts.
9. **Tworzenie Alternatywy dla Buildboxa Krok Po Kroku.PDF** — Engine-on-Engine architecture, Buildbox-style UX, visual graph systems, Smart Assets and production automation.

## Canonical technical themes

### Sovereign edge AI
- Gemma 3 27B is treated as a candidate local reasoning model under constrained hardware.
- Source documents describe GGUF Q4_K_M, GPU/CPU offloading, Flash Attention, 16k–32k context as practical working ranges, and 18–20 GPU layers on RTX 3070-class hardware.
- These values are **engineering hypotheses to benchmark**, not guaranteed performance claims.
- Rclone is proposed as an abstraction layer for multiple Google Drive accounts.
- SearXNG + Open WebUI are proposed for private web research.
- MCP provides the tool boundary.
- NSVIF adds symbolic checks, sandboxing and bounded self-correction for generated code.

### Agent systems
- Supervisor/orchestrator architecture with bounded specialists.
- A2A is useful when delegation gives measurable specialization, latency or cost benefits.
- MCP should separate tool capability from authorization.
- Provenance and audit should be first-class data.
- Human approval should sit at consequential side-effect boundaries.

### Open creator platform
- Engine-on-Engine approach: preserve Unity/Unreal as the runtime foundation and build a creator-oriented abstraction layer above it.
- Mind Map / graph-first navigation.
- Typed node/port systems.
- Blackboard / serialized variables.
- Event-driven runtime rather than per-frame polling where appropriate.
- Smart Assets through import heuristics and AssetPostprocessor-style automation.
- Cross-platform build and monetization abstractions should remain modular adapters.

### Influence analysis
- The source corpus combines System 1/System 2 framing, Cialdini-style influence, visual rhetoric, gaze cueing, habit loops, social proof and covert influence concepts.
- The implementation direction in this repository is **defensive**: influence detection, transparency, explainability and media literacy.
- Covert manipulation mechanisms should not be operationalized as a system for hidden psychological control.

### AI content productization
- Blog, email, newsletter, social and digital-product patterns can be unified into a research → audience model → offer → generation → QA → packaging → approval → publishing pipeline.
- Reusable template packs are a potential product abstraction.

## Evidence discipline

Every future implementation derived from these documents should label information as one of:

- Source claim
- Engineering hypothesis
- Verified behavior
- Future roadmap

Do not convert an estimate in the corpus into a production guarantee without measurement.
