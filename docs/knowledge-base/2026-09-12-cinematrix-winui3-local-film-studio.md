# CineMatrix — WinUI 3 / .NET Local Film Studio Corpus

## Source set
Two supplied CineMatrix documents were reviewed as one corpus:
- `CineMatrix_ Autonomiczne Studio Filmowe - Google Gemini.pdf` — 10 pages.
- `CineMatrix_ Autonomiczne Studio Filmowe.pdf` — 9 pages.

The corpus describes a Windows desktop autonomous film studio centered on WinUI 3, C#, MVVM, SQLite/EF Core, local LLMs, Wan 2.1 and ComfyUI, with explicit attention to VRAM/LOH management, cinematic shot language and local distribution.

## Durable architectural contributions

### 1. Native Windows studio shell
`WinUI 3 + Windows App SDK + XAML + CommunityToolkit.Mvvm + MVVM` is proposed as the native presentation architecture. The intended workspace resembles an NLE: screenplay/master-scene editor, generated-video preview and Master Prompt management.

### 2. Dual inference architecture
The corpus separates the language/reasoning role from visual generation: local GGUF LLM for screenplay/directorial transformation and a DiT video model such as Wan 2.1 for visual synthesis.

The stronger durable abstraction is a model-capability layer, not a hard-coded model identity.

### 3. Execution-boundary decision
The documents propose two possible integration modes:
- in-process Python embedding through CSnakes/Python.NET;
- local ComfyUI process exposed through HTTP/WebSocket.

These must be modeled as alternative execution adapters. They are not equivalent. The source code shown actually uses `127.0.0.1:8188`, `/prompt` and `/ws`, therefore it is a local process integration rather than proof of an in-process ComfyUI runtime.

### 4. VRAM-aware phase scheduling
The corpus adds a concrete resource-management concept: evict language-model GPU residency before video inference and restore it afterwards. This becomes a scheduler/resource-policy requirement, not merely a `torch.cuda.empty_cache()` call.

### 5. Managed-memory discipline
The documents explicitly target .NET Large Object Heap pressure from video buffers and propose `ArrayPool<byte>` plus asynchronous file streaming. This is adopted as a performance hypothesis requiring profiling rather than as an unconditional guarantee.

### 6. Cinematic Shot IR
The mapping of narrative intention to camera/lens/movement/lighting/color parameters should become typed intermediate representation:

`NarrativeIntent → ShotIR → Model Adapter → Workflow → Render Artifact`

The example categories include EWS/MCU/ECU, focal length, tracking/dolly/static movement, depth of field, lighting, color treatment, CFG/shift and resolution.

### 7. Local film-world persistence
SQLite + EF Core is proposed for Master Prompts, screenplay history, scene history and location/cultural context. The Cieszyn/Cieszyn Silesia material is treated as an optional project/world configuration, not a global hard-coded fact.

### 8. Distribution architecture
The corpus identifies a real product boundary between a small application binary and multi-gigabyte model assets. Model storage/download/update must therefore be independently versioned from application releases.

The proposed MSIX external-location/sparse-packaging strategy is recorded as a packaging hypothesis requiring platform validation before being treated as release truth.

### 9. Cinematic UX during compute stalls
The corpus introduces a useful UX pattern: computationally expensive model eviction/loading is represented through a continuous cinematic production state rather than a frozen UI. This belongs to P97's production-state projection layer.

## Verification findings from the supplied implementation

The documents call the code a production/core implementation, but the shown snippets contain assumptions that prevent treating it as production-verified:

- ComfyUI node IDs (`6`, `3`, `15`) are hard-coded.
- The WebSocket receive buffer/message handling is incomplete for robust fragmented/large messages.
- `videoSpan.CopyTo(frameBuffer)` is an explicit copy, so the shown path does not establish end-to-end zero-copy semantics.
- `output["gifs"]` assumes a particular workflow output shape.
- HTTP/WebSocket ComfyUI operation contradicts any claim that the shown implementation is fully in-process.
- UI state bindings require review; generation/cancellation enablement should be verified against actual desired state transitions.
- Resource eviction/restoration needs postcondition evidence that VRAM residency actually changed as intended.
- `GC.Collect`/LOH management must be benchmarked; forced collection is not itself proof of improved throughput or latency.
- Model parameter values shown in the report are source claims and must remain versioned adapter metadata until independently verified.

## Canonical integration

`P97` owns the multimedia production pipeline; this corpus specializes its local Windows desktop implementation. `P100` owns release/supply-chain assurance. `P113` owns prompt/visual compilation and model adapters. `P114` owns provenance-bearing semantic memory and retrieval.

## Security and authority invariants

- local process ≠ trusted process;
- localhost endpoint ≠ authorization authority;
- model output ≠ execution authorization;
- UI status ≠ render completion proof;
- generated file URL ≠ verified artifact identity;
- model name/version in a prompt ≠ current production capability;
- packaging claim ≠ validated installer behavior.

## Maturity
`ARCHITECTURE ENHANCED — IMPLEMENTATION NOT VERIFIED`
