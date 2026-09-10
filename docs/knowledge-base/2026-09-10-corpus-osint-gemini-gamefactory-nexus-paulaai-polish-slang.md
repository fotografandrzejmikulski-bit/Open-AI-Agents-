# Knowledge Base — OSINT, Gemini Agents, Text-to-Game, Nexus, PaulaAI and Polish Registers — 2026-09-10

## Source batch

17 uploaded files were reviewed. The batch contains:
- NEXUS-GHOST / autonomous OSINT agent architecture;
- Gemini multi-platform agent-builder architecture;
- Text-to-Game Android generation factory;
- four distinct game-adaptation families plus duplicate book-adaptation copies;
- Polish youth and prison-register dictionaries plus a PWN dictionary reference artifact;
- Nexus hybrid programming-language specification;
- two identical PaulaAI Android transformation reports.

## Deduplication

Exact/near-exact duplicates in this batch:
- `Tworzenie Gry na Podstawie Książki (1).pdf` = `Tworzenie Gry na Podstawie Książki_260105_101356.pdf`;
- `Tworzenie i Ulepszanie Aplikacji PaulaAI (1).pdf` = `(2).pdf`;
- `SŁOWNIK GWARY WIĘZIENNEJ.doc` and `Słownik polskiej grypsery (gwary więziennej).doc` contain substantially overlapping lexical material and are treated as two source witnesses of one corpus, not two products.

## 1. OSINT agent

NEXUS-GHOST combines local Gemma/Ollama inference, a FastAPI stateful backend, Three.js/WebGL visualization and SSE streaming. Its Autonomous Command Loop turns an operator directive into model analysis, tool selection, execution, context reinjection and final synthesis. The source also describes active port scanning, passive search/dorking, web crawling, EXIF extraction and IP geolocation.

Repository decision: deepen Project 32 rather than create a generic second OSINT agent. The useful engineering delta is a local-first agent shell, deterministic tool contracts, event streaming, visual evidence workstation and resumable investigation state. Active reconnaissance remains authorization-gated; source patterns for credential discovery or stealth are not production objectives.

## 2. Gemini agent builder

The Gemini report decomposes an agent builder into cognitive, execution and orchestration layers and covers Google Gen AI SDK, ADK, MCP, desktop Python, Streamlit, Android/Kotlin, Gemini Nano/AICore, MediaPipe RAG, multi-agent orchestration, memory and prompt-injection defenses.

Repository decision: integrate with Projects 33, 61 and 72. The provider-specific architecture strengthens the provider-neutral contract rather than creating a Gemini-only canonical runtime.

## 3. Text-to-Game Android factory

The Android game factory is materially more specialized than a generic app builder. It defines:
- Flutter/Kotlin mobile control client;
- FastAPI orchestration;
- Universal Game Description Language (UGDL) as an intermediate game representation;
- engine adapters for Godot 4 and Unity 6;
- generated `.tscn/.gd/project.godot` or `.unity/.cs/.meta` artifacts;
- Docker/GitHub Actions headless build farms;
- APK/AAB signing and artifact storage;
- scenario segmentation, mechanic extraction and asset extraction;
- RAG/context management for long scenarios.

Repository decision: create Project 86, because this is a concrete game-specific compilation and delivery factory rather than merely another generic app builder. It integrates Projects 33, 52, 61, 65, 69, 72 and 80.

## 4. Człowiek Roku adaptations

The UE5 report defines Cieszyn and satellite locations as emotional memory zones, with Lens System, Stigma Meter, TimeRift and MemoryParticle mechanics. The Unity Android report maps Lumen/Nanite/Niagara/SceneCapture/streaming concepts to URP, baked lighting, VFX Graph, AsyncGPUReadback and additive scenes. The HTML report defines an isometric Three.js/React Three Fiber tech-noir implementation with procedural city tiles, WFC, GLSL selective desaturation, rain-on-lens and kinetic typography.

Repository decision: evolve Project 73 into a multi-target product architecture covering UE5 desktop/console, Unity Android and WebGL/Three.js. The two book-adaptation PDFs are duplicates and add no independent lineage.

## 5. Distinct game adaptations

`Tworzenie Gry Na Podstawie Komiksu (1).pdf` describes **Druga Połowa** as a TPP narrative exploration game in UE5 with time-stopping, Soul Seeker flashlight, Memory Particles, snow interaction and an interaction component. This is a distinct creative product from Człowiek Roku and CCR, therefore Project 88 is created.

`Tworzenie Gry w Unreal Engine 5 (1).pdf` describes **CCR: The Closed Lens**, a TPP narrative adventure/puzzle in UE5. It treats light as a memory carrier, Closed Lens time cycles, Photo-Reality Manipulation, TimeRift and MemoryParticle systems. This is a game implementation distinct from Project 82's graphic-novel/transmedia universe, therefore Project 89 is created.

## 6. Nexus hybrid language

The Nexus specification proposes one language spanning C/C++, C#, JS/TS, Lua, Python, GDScript, Java, Kotlin and Swift. Its architecture includes ownership/borrowing, ORC, isolated tracing GC, reified generics, sound gradual typing, null safety, significant indentation, multiline lambdas, exhaustive pattern matching, structured concurrency, actors, Result types, C/C++ ABI bridging, dynamic-language interpretation and WASM/JS emission through LLVM/MLIR.

Repository decision: create Project 87 as a dedicated language/compiler research project. Existing Projects 61 and 80 remain the runtime/convergence/self-evolution consumers; Project 24 remains the prompt/agent DSL compiler and is not conflated with a general-purpose programming language.

## 7. PaulaAI

The two PaulaAI reports are duplicates. They describe migration from a Replit web prototype to Android through Capacitor, GitHub/CI/CD, native plugins, RAG/vector memory, voice/STT/TTS, vision, mobile-first UX, Play policy and backend scaling. Repository decision: evolve Project 08 and connect delivery concerns to Project 33 and runtime concerns to Project 61. No new PaulaAI project is required.

## 8. Polish lexical/register corpus

The youth dictionary is a large contemporary colloquial register source. The two prison/slang documents overlap heavily and provide a prison-register corpus. The PWN file is a one-page continuation/reference artifact rather than a complete dictionary dataset.

Repository decision: deepen Project 75 with register-aware lexical records, provenance, source witness tracking and contextual constraints. The corpus is not treated as a normative dictionary or as evidence that a term is current outside its documented register.

## Cross-portfolio impact

- Project 32: local OSINT agent architecture, event loop, tool contracts and evidence workstation.
- Project 33: Gemini provider abstraction, game-specific delivery stages and Android build governance.
- Project 52: executable game-generation inputs, UGDL and engine-neutral rules-to-build pipeline.
- Project 61: Gemini/Android edge architecture, Nexus compiler target, game/runtime convergence.
- Project 73: multi-target Człowiek Roku architecture and anti-spoiler/provenance continuity.
- Project 75: youth/prison/standard-language register graph.
- Project 08: PaulaAI Android/RAG/voice/vision evolution.
- Project 82: CCR game-lineage separation from graphic-novel/transmedia canon.
- Project 80: Nexus/compiler/self-evolution reinforcement.

## New projects

### Project 86 — OmniGame Text-to-Android Factory MAX
A governed text/scenario-to-playable-Android game production factory using UGDL, engine adapters and reproducible headless builds.

### Project 87 — Nexus Hybrid Programming Language & Compiler MAX
A research compiler/toolchain for the proposed Nexus language, with typed memory domains, concurrency, ABI interoperability and MLIR/WASM/native lowering.

### Project 88 — Druga Połowa Interactive TPP Experience MAX
A distinct UE5 adaptation of the comic `Druga Połowa`, centered on time, memory, exploration and atmospheric interaction.

### Project 89 — CCR: The Closed Lens Interactive Game MAX
A distinct UE5 game implementation of the CCR universe, separate from Project 82's graphic-novel/transmedia production system.

## Epistemic and safety boundaries

- OSINT claims remain provenance-bound; identity, motive and relationship inference require corroboration.
- Active reconnaissance is capability- and authorization-gated.
- Generated game code is untrusted until build, test and runtime verification.
- Engine compatibility claims require real build targets; the source's market percentages are not treated as established facts.
- Nexus is a proposed architecture, not an established production language.
- Slang dictionaries describe source corpora and registers; they do not establish universal usage or normative correctness.
- Medical, legal and privacy claims appearing in source references are not promoted to professional advice.
