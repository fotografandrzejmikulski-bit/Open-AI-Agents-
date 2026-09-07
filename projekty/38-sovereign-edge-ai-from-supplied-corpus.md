# Project 38 — Sovereign Edge AI

## Thesis

Build a local-first agentic engineering stack for constrained hardware, combining quantized open-weight models, hybrid CPU/GPU inference, MCP tools, private research, cloud-file abstraction and neuro-symbolic verification.

## Source-derived baseline

The supplied corpus describes Gemma 3 27B, GGUF quantization, CPU/GPU offloading, 16k–32k practical context ranges on 32 GB RAM, Rclone-backed multi-drive access, SearXNG/Open WebUI research, MCP tool use and a bounded symbolic verification loop. fileciteturn69file6L258-L289

## Improved architecture

```text
Local model
   ↓
Inference gateway
   ↓
MCP capability boundary
   ├── filesystem
   ├── research
   ├── cloud-drive abstraction
   └── engineering tools
   ↓
Policy / least privilege
   ↓
Verification
   ├── AST
   ├── lint / static checks
   ├── sandbox
   └── test execution
   ↓
Human approval for consequential effects
   ↓
Audit / provenance
```

## Benchmark program

Treat every hardware setting as a hypothesis. Benchmark:

- prompt processing rate;
- generation tokens/s;
- peak VRAM;
- peak RAM;
- context length before degradation;
- tool-call latency;
- recovery after OOM / timeout;
- quality on coding and research evaluation sets.

## Safety

Abliterated model variants, if used, must not be treated as a safety control. Application-level policy, capability restrictions, sandboxing, verification and human authorization remain mandatory.

## Roadmap

Phase 1: reproducible local runner.

Phase 2: MCP connector fabric.

Phase 3: verification loop.

Phase 4: multimodal engineering workflows.

Phase 5: adaptive local/remote routing.
