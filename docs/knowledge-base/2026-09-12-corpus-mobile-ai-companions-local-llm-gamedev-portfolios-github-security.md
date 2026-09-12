# Knowledge Corpus — Mobile AI / Local LLM / AI Companions / GameDev / Portfolio Builders / GitHub Engineering

**Date:** 2026-09-12
**Status:** INGESTED → VERIFIED / ARCHITECTURAL SYNTHESIS
**Decision:** NO_NEW_PROJECT — extend P86, P100, P113, P118/P119 and the portfolio/web-builder knowledge layer.

## 1. Source normalization

The supplied batch contains several distinct source families:

1. `fotografaandrzej333/GDevelop` — fork of the GDevelop engine.
2. `fotografaandrzej333/ollama` — fork of Ollama.
3. GitHub `ai-companion`, `mobile-ai`, `openrouter`, `voip-communications`, `image-to-video-generation`, `video-generation`, `godot-4` topics.
4. Polish market articles covering ChatGPT alternatives and AI presentation tools.
5. Privacy/virtual-number/VoIP/email-relay sources, substantially overlapping an already-ingested corpus.
6. Low-code/no-code and AI-agent builder sources.
7. Portfolio-builder sources and the user's forks of Plasmic, Builder, GrapesJS, Dopefolio and React portfolio templates.
8. GitHub engineering/security sources: repository taxonomy, artifact metadata, Well-Architected material, npm, Electron, CodeQL, Sponsors, Marketplace, MCP, Codespaces, roadmap and community resources.
9. SentinelOne research on AI-assisted malware tooling.
10. Google Play listing for Rosytalk AI Character Chat.

Repeated URLs were deduplicated. The repeated VoIP topic and repeated MoreMins/Zadarma sources add no independent evidence beyond the already-ingested privacy/identity corpus.

## 2. Personal fork audit

### GDevelop

`fotografaandrzej333/GDevelop` is a public fork created on 2026-09-12. Its upstream is `4ian/GDevelop`. The upstream README describes GDevelop as a full-featured no-code open-source engine for 2D, 3D and multiplayer games on mobile, desktop and web, with an event-based system, modular behaviors and AI-assisted creation. Its architecture separates `Core`, `GDJS`, `GDevelop.js`, `newIDE` and `Extensions`. The README states that the core/engine/IDE/extensions are MIT licensed and that exported games can be distributed commercially without being forced open-source.

Architectural extraction:

```text
NATURAL LANGUAGE / VISUAL GAME DESIGN
        ↓
EVENT-BASED GAME MODEL
        ↓
ENGINE + EXTENSIONS
        ↓
EDITOR / PREVIEW
        ↓
EXPORT TARGETS
        ↓
MOBILE / DESKTOP / WEB
```

The important new signal for P86 is not merely no-code game development. It is the convergence of **AI-assisted creation + no-code event systems + multi-target export + extension ecosystem**.

### Ollama

`fotografaandrzej333/ollama` is a public fork created on 2026-09-12. Its upstream is `ollama/ollama`. The current README describes Ollama as a local open-model runtime with CLI, REST API, Python and JavaScript libraries, model importing/Modelfiles, Docker support and integrations with coding agents and assistants. It explicitly lists integrations with Claude Code, Codex, Copilot CLI, DeepSeek Harness, Droid, OpenCode and OpenClaw, and lists mobile clients and SDKs including Swift.

Architectural extraction:

```text
LOCAL MODEL RUNTIME
        ↓
REST / SDK / CLI
        ↓
AGENT / APP / IDE
        ↓
LOCAL DATA / RAG / TOOLS
        ↓
CONTROLLED EXECUTION
```

This materially strengthens the repository's local-first inference/provider-neutral architecture.

## 3. Mobile AI and companion ecosystem

GitHub's current `ai-companion` topic contains hundreds of public repositories and a meaningful Swift subset. Current examples include self-hosted AI companion systems, local voice interaction, Live2D/VRM avatars and real-time digital-human systems. The `mobile-ai-agent` ecosystem includes Android AI coding agents and mobile-agent projects.

The Google Play listing for Rosytalk describes a character-chat product with realistic/anime characters and roles including friend, family member, study partner and life coach; it currently shows 5M+ installs, 40.8K reviews and an adult-oriented content rating.

The durable architecture signal is:

```text
PERSONA / CHARACTER MODEL
        ↓
MEMORY
        ↓
LOCAL / REMOTE MODEL ROUTING
        ↓
TEXT + VOICE + AVATAR
        ↓
MOBILE STATE
        ↓
SAFETY / CONSENT / AGE POLICY
        ↓
USER EXPERIENCE
```

Critical invariants:

- `AI_PERSONA ≠ REAL_PERSON`
- `MEMORY ≠ AUTHORITY`
- `CHARACTER_STATE ≠ USER_IDENTITY`
- `EMOTIONAL_SIMULATION ≠ HUMAN_RELATIONSHIP`
- `MODEL_OUTPUT ≠ AUTHORIZATION`

This is best treated as an extension of the existing Fable/StoryWorld and OmniMAS/local-mobile-agent architecture rather than a new generic companion project.

## 4. OpenRouter and provider-neutral routing

The current GitHub `openrouter` topic shows a large ecosystem of projects using OpenRouter for model-agnostic routing, model comparison and agent harnesses. The discovery value is architectural: applications increasingly separate **application capability** from the underlying model provider.

Recommended registry abstraction:

```yaml
ModelRoute:
  capability:
  provider:
  model:
  modality:
  context:
  latency:
  cost:
  privacy:
  locality:
  availability:
  authorization:
  fallback_class:
  observed_at:
```

`OPENROUTER ≠ AUTHORITY`; it is a provider/gateway candidate. Routing still requires policy, capability matching and postcondition verification.

## 5. AI presentation market

The 2026 NextDocs article evaluates presentation systems using research quality, output quality, brand consistency and export flexibility. Its comparison includes NextDocs, Gamma, Gemini for Google Slides, Canva, Pitch, Claude, ChatGPT, SlidesAI, MagicSlides and Genspark. It emphasizes a shift from simply generating slides to supporting research, data accuracy, multi-variant generation and professional exports.

Architectural extraction:

```text
RESEARCH
↓
NARRATIVE / OUTLINE
↓
MULTI-VARIANT GENERATION
↓
BRAND / DESIGN SYSTEM
↓
FACT / SOURCE VALIDATION
↓
EXPORT
↓
HUMAN REVIEW
```

The ranking itself is discovery evidence, not a canonical market ranking.

## 6. AI alternatives to ChatGPT

The WeNet and MaxRoy articles are useful market-discovery sources. They repeatedly classify alternatives by **specialization**: research/search, long-context document work, coding, marketing, Google/Microsoft ecosystem integration, privacy and multi-model access.

The reusable insight is:

`MODEL CHOICE SHOULD FOLLOW JOB / CAPABILITY / CONSTRAINTS, NOT BRAND LOYALTY.`

These articles are not authoritative current benchmarks; claims and model versions must be independently verified.

## 7. Video generation ecosystem

Current GitHub topic evidence shows a substantial open-source image-to-video/video-generation ecosystem. Examples include LTX-Video, ComfyUI-LTXVideo, Helios, VideoCrafter, vLLM-Omni, Wan and HunyuanVideo-I2V. A separate `video-generator` ecosystem also includes MCP-connected short-video automation pipelines.

Architecture implication for P97/P113:

```text
PROMPT / SOURCE MEDIA
↓
VIDEO CAPABILITY
↓
MODEL / PROVIDER ADAPTER
↓
TEMPORAL / MOTION CONTROL
↓
RENDER
↓
QUALITY / SAFETY / PROVENANCE
↓
DISTRIBUTION
```

GitHub topic membership is discovery/classification evidence, not quality proof.

## 8. Godot / agentic game development

The current Godot 4 topic contains active agentic-game-development projects including GodotMaker, GodotPrompter, `godogen`, and MCP-based Godot tooling. A current TypeScript-filtered topic view also shows `godot-mcp-enhanced`, which advertises a three-layer headless/editor/game-bridge architecture with sandboxing, recording, frame verification and cross-version CI, and `dsh-godot-game-studio`, which exposes bounded Godot MCP tools for audit, test, simulation, validation and release.

This is a significant extension of P86:

```text
NATURAL LANGUAGE
↓
GAME SPEC / UGDL
↓
GODOT AGENT SKILLS
↓
MCP / EDITOR / HEADLESS BRIDGE
↓
BUILD
↓
RUNTIME TEST
↓
FRAME / LOG VERIFICATION
↓
RELEASE
```

The combination of MCP + headless/editor/game bridge + frame verification is especially relevant to the repository's `READBACK → VERIFY` doctrine.

## 9. Low-code / no-code and AI builders

ToolJet's current 2026 comparison describes self-hosting, AI-assisted development, Git synchronization, governance and many integrations. Modelence's August 2026 comparison emphasizes a more important decision framework: license, self-hosting effort, free-feature boundaries, community health, production readiness and open-source vs open-core status.

Reusable architecture rule:

```text
PUBLIC REPOSITORY
        ≠
FULLY OPEN PRODUCT
        ≠
FREE FEATURE SET
        ≠
LOW OPERATIONAL COST
```

For builder selection the registry should capture:

`LICENSE + SELF_HOSTING + PAID_FEATURE_BOUNDARY + DATA_CONTROL + EXTENSIBILITY + PRODUCTION_READINESS + MAINTENANCE_COST`.

This extends P100's app-builder/provider registry.

## 10. Portfolio-builder ecosystem

The user's supplied portfolio repositories are mostly forks/templates rather than independent original products:

- `mojealterego/plasmic` — fork of Plasmic; visual React builder/CMS.
- `mojealterego/grapesjs` — fork of GrapesJS; open-source web-builder framework.
- `mojealterego/Dopefolio` — fork of rammcodes/Dopefolio; developer portfolio template, GPL-3.0.
- `mojealterego/react-portfolio` — fork of ubaiMutl/react-portfolio; React portfolio template.
- `BuilderIO/builder-public` — archived public fork/repository; current Builder development is in `BuilderIO/builder`.
- `tamojit-123/developerPortfolio` — customizable React portfolio template with GitHub-connected projects and Docker support.

GitHub topic evidence currently shows a large portfolio-website ecosystem and dozens of portfolio-generator projects. This is not a reason to create another generic portfolio project. The stronger synthesis is a **portfolio compilation layer**:

```text
GITHUB / PROJECT SOURCES
↓
REPOSITORY CLASSIFICATION
↓
PROJECT / SKILL / EVIDENCE EXTRACTION
↓
CONTENT MODEL
↓
DESIGN SYSTEM
↓
PORTFOLIO PRESENTATION
↓
LIVE / STATIC / CMS / BUILDER OUTPUT
```

This directly supports the user's existing MojeAlterego web/product work and should remain a capability layer rather than a separate knowledge-project identity.

## 11. GitHub engineering / supply-chain knowledge

GitHub's official documentation confirms that repository topics are classification/discovery metadata; topic membership must never be treated as a quality or security guarantee.

GitHub's artifact metadata API now exposes artifact provenance/deployment/storage records keyed by artifact digest. This provides a direct control-plane pattern for linking a built artifact to deployment environments and attestations.

npm's current documentation strengthens the supply-chain model with OIDC trusted publishing, short-lived workflow-specific credentials and automatic provenance attestations for supported public-package publishing flows. npm explicitly recommends trusted publishing over long-lived tokens when available.

CodeQL remains the semantic static-analysis layer: it allows code to be queried as data and supports vulnerability-pattern detection across supported languages/frameworks.

Electron's current security checklist reinforces concrete desktop hardening requirements: secure content, context isolation, sandboxing, CSP, restricted navigation/window creation, validated IPC senders, avoiding unsafe external content and use of current Electron versions.

Combined architecture:

```text
SOURCE
↓
BUILD
↓
SAST / CODEQL
↓
DEPENDENCY / PACKAGE CONTROLS
↓
ARTIFACT DIGEST
↓
PROVENANCE / ATTESTATION
↓
DEPLOYMENT RECORD
↓
RUNTIME READBACK
↓
VERIFY
```

## 12. AI-assisted malware / defensive intelligence

SentinelOne's Predator AI research documents a 2023 Python infostealer/hacktool that integrated a ChatGPT-driven interface to simplify interaction with disparate attack-related utilities. The research describes AI being used for data enrichment and context around scanner results.

This is defensive threat intelligence, not a recommendation to reproduce offensive functionality.

Architecture implication for P100/P108/P32:

`AI INTERFACE + TOOL AGGREGATION` is itself a threat pattern and should be monitored as an agentic-abuse class.

Important invariant:

`LLM ASSISTANCE ≠ NEW AUTHORITY`

AI can lower the operational complexity of existing tools without changing the underlying authorization boundary.

## 13. Cross-source synthesis

The entire batch converges on a single architecture:

```text
CAPABILITY
   ↓
MODEL / ENGINE / BUILDER / PROVIDER
   ↓
ADAPTER
   ↓
WORKFLOW
   ↓
STATE / MEMORY
   ↓
POLICY
   ↓
AUTHORIZATION
   ↓
EXECUTION
   ↓
READBACK
   ↓
VERIFICATION
   ↓
PROVENANCE
```

This applies across:

- mobile AI companions;
- local LLM runtimes;
- AI game development;
- video generation;
- presentation generation;
- low-code builders;
- portfolio generation;
- GitHub software delivery;
- desktop applications.

## 14. New invariants

- `FORK ≠ ORIGINAL IMPLEMENTATION`
- `TOPIC ≠ QUALITY PROOF`
- `OPEN SOURCE ≠ ALL FEATURES FREE`
- `SELF-HOSTED ≠ ZERO OPERATING COST`
- `MODEL PROVIDER ≠ CAPABILITY AUTHORITY`
- `LOCAL MODEL ≠ AUTOMATICALLY SAFE MODEL`
- `AI COMPANION ≠ HUMAN RELATIONSHIP`
- `SYNTHETIC PERSONA ≠ REAL IDENTITY`
- `REPOSITORY ≠ VERIFIED ARTIFACT`
- `BUILD SUCCESS ≠ RELEASE AUTHORIZATION`
- `ARTIFACT DIGEST ≠ SECURITY PROOF WITHOUT ATTESTATION / CONTEXT`
- `PROVENANCE ≠ MALWARE-FREE GUARANTEE`
- `AI ASSISTANCE ≠ AUTHORIZATION`

## 15. Portfolio decision

**NO_NEW_PROJECT.**

The batch increases the density of existing architecture:

- **P86** — agentic/no-code game production and Godot verification.
- **P100** — provider registry, local models, OpenRouter, builders, GitHub supply chain, npm/Electron/CodeQL.
- **P113** — multimodal model/provider adapter layer for video and local inference.
- **P118** — AI character/storyworld/companion capabilities.
- **P119** — local Android/mobile agent runtime and device-control verification.
- **P97** — multimodal/video/content factory.
- **Portfolio/web-builder layer** — Plasmic/GrapesJS/Builder/portfolio-template capability set.

The most important incremental discovery is the **closed-loop mobile/game AI architecture combining local inference, agent skills, MCP/editor bridges and observable runtime verification**.
