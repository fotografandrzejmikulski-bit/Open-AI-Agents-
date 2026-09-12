# P100 Extension — CineMatrix Windows Runtime & Release Assurance

## Parent
P100 — NeXus AI Code OMEGA-X Agentic Development Environment MAX

## Trigger
CineMatrix introduces a native WinUI 3 desktop shell, embedded/local AI runtimes, ComfyUI integration, large model assets and a proposed MSIX external-location distribution model.

## Release architecture

```text
SOURCE
 ↓
BUILD / SIGN
 ↓
APP PACKAGE
 ↓
MODEL-ASSET MANIFEST
 ↓
INSTALL / UPDATE TEST
 ↓
RUNTIME CAPABILITY DISCOVERY
 ↓
RENDER SMOKE TEST
 ↓
ARTIFACT HASH / PROVENANCE
 ↓
PROMOTE / ROLLBACK
```

## Required controls
- application binary and model weights versioned independently;
- model manifest records filename, format, size, hash, model version/license and adapter compatibility;
- no model weight is trusted solely because its filename matches a manifest entry;
- installation directories, writable cache directories and project-data directories are explicitly separated;
- ComfyUI localhost connectivity is treated as a capability endpoint, not an authority boundary;
- packaging claims require install/update/repair/uninstall evidence on supported Windows versions;
- signing and provenance are recorded separately from application functionality.

## Source-code audit requirements
The supplied CineMatrix code is architectural skeleton material, not a release artifact. Before promotion:
- replace hard-coded ComfyUI node IDs with validated workflow schemas/semantic node roles;
- handle WebSocket fragmentation and reconnect/readback behavior;
- verify output type/codec rather than assuming `gifs` represents the final video;
- validate cancellation semantics;
- test concurrent access to SQLite and project state;
- test memory pressure under actual model workloads;
- verify that UI progress reflects authoritative render state.

## Status
`RELEASE ARCHITECTURE ENHANCED — NO PRODUCTION BUILD VERIFIED`
