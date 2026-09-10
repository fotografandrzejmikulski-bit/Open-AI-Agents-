# Project 103 — OmniGame Unity Autonomous Production Engine MAX

## Status
PROPOSED → ARCHITECTURE BASELINE → PROJECT GENESIS 2026-09-10

## Mission
Build a Unity-specific autonomous game-production engine that converts a narrative blueprint, GDD or structured design brief into inspectable scene graphs, prefabs, scripts, tests and iterative editor changes through a guarded agent loop.

## Why this is distinct
- **P40** owns provider-neutral agentic development and live-state execution.
- **P86** owns text/scenario → Android game factory output.
- **P88/P89** own specific CCR game/world experiences.
- **P100** owns the general NeXus AI Code product shell.
- **P103** owns the **Unity-specific narrative-to-production compiler/executor**: Unity Editor state, scene graph, prefab persistence, Unity MCP/UTCP, structured scene IR and Unity-aware in-memory C# compilation.

## Canonical architecture

```text
NARRATIVE / GDD / BLUEPRINT
            ↓
INTENT + ENTITY EXTRACTION
            ↓
GAME DESIGN IR / JSON SCHEMA
            ↓
SCENE TOPOLOGY + PREFAB PLAN
            ↓
UNITY MCP / UTCP TOOL BROKER
            ↓
UNITY EDITOR STATE
  ├── hierarchy
  ├── scenes
  ├── prefabs
  ├── assets
  └── console/errors
            ↓
GENERATE / MUTATE
            ↓
ROSlyn IN-MEMORY C# VALIDATION
            ↓
BUILD / PLAYMODE / TEST
            ↓
READBACK + ASSERTIONS
            ↓
CHECKPOINT / PROMOTE / ROLLBACK
```

## 1. Narrative-to-Scene Compiler

The model does not directly emit arbitrary Unity API code for every spatial operation. It first produces a deterministic structured representation describing entities, prefab identifiers, transforms, rotations, hierarchy relationships and other schema-constrained parameters. A Unity-side executor validates the representation and performs the corresponding editor operations.

This follows the source's LLMER-oriented principle of moving spatial construction from unconstrained code generation toward structured data generation. fileciteturn859file1L395-L415

## 2. Unity MCP / UTCP bridge

The source describes MCP as the communication boundary between the external model/orchestrator and the Unity Editor, with tools for scene hierarchy, console diagnostics, prefab operations and project state. It also describes UTCP/Code Mode as a possible optimization for chaining multiple editor operations inside a sandboxed execution cycle. fileciteturn859file1L257-L279 fileciteturn859file1L290-L304

Every tool declares:
- input schema;
- read/write side effects;
- scope;
- authorization requirement;
- timeout;
- verification method;
- rollback/checkpoint behavior.

## 3. Roslyn in-memory compilation

The source proposes Microsoft Roslyn-based compilation of generated C# in memory to avoid repeatedly forcing Unity domain reloads. The pipeline is:

```text
SOURCE STRING
 ↓
CSharpSyntaxTree.ParseText
 ↓
REFERENCE RESOLUTION
 ↓
CSharpCompilation.Create
 ↓
MemoryStream
 ↓
AssemblyLoadContext
 ↓
SANDBOXED EVALUATION
 ↓
READBACK / ERROR FEEDBACK
```

The source explicitly identifies metadata-reference management as a major implementation challenge. fileciteturn859file1L305-L339

## 4. Persistent Unity state

Long-running autonomous production requires durable project memory and authoritative readback. The system must preserve:
- current GDD/architecture decisions;
- generated scene IR;
- prefab registry;
- asset provenance;
- build/test history;
- known failures;
- accepted/rejected candidate changes;
- checkpoints and rollback points.

## 5. Prefab and scene persistence

Generated objects must be persisted through Unity-aware APIs rather than treated as ephemeral editor state. The source identifies `PrefabUtility.SaveAsPrefabAssetAndConnect` and `EditorSceneManager.MarkSceneDirty` as examples of the required persistence boundary. fileciteturn859file1L416-L428

## 6. Autonomous loop

```text
OBSERVE PROJECT
 ↓
PLAN
 ↓
GENERATE STRUCTURED CHANGE
 ↓
AUTHORIZE
 ↓
APPLY IN SANDBOX/CHECKPOINT
 ↓
COMPILE
 ↓
TEST
 ↓
READBACK
 ↓
CRITIQUE
 ↓
REPAIR OR PROMOTE
```

Autonomy is bounded by policy. Generated code and scene mutations remain untrusted until they pass the applicable validation gates.

## 7. Safety model

- Model output ≠ editor authorization.
- MCP ≠ authorization.
- A successful tool call ≠ successful game-state mutation.
- Editor UI state ≠ authoritative state.
- Generated C# ≠ trusted code.
- Simulation/play mode ≠ production evidence.
- Checkpoint ≠ verification; postcondition readback remains mandatory.
- Self-healing candidates require test and rollback boundaries.

## 8. Verification matrix

| Gate | Evidence |
|---|---|
| G0 | schema and project-state consistency |
| G1 | Unity Editor connection/readback |
| G2 | tool authorization/scope |
| G3 | scene graph mutation correctness |
| G4 | prefab persistence |
| G5 | Roslyn compile correctness |
| G6 | PlayMode/EditMode test results |
| G7 | build reproducibility |
| G8 | checkpoint/rollback correctness |
| G9 | long-session memory consistency |
| G10 | end-to-end narrative → playable artifact replay |

## Source-derived technical baseline
The supplied Unity report describes a blueprint in which the AI brain is external to the Unity Editor, communicates through MCP/UTCP, uses structured JSON for scene construction, relies on UnityEditor APIs for persistent changes, and uses Roslyn for in-memory C# compilation. fileciteturn859file1L143-L163 fileciteturn859file1L257-L273

The same source notes that Unity's native AI ecosystem already includes project-aware Ask/Plan/Agent modes and checkpoints, plus local inference via Sentis; these are treated as compatibility/reference inputs rather than assumptions that P103 itself exists. fileciteturn859file1L175-L204

## Maturity
Architecture baseline. No claim of a production-ready autonomous Unity agent is established by the source alone.

## Derived from
P40, P61, P72, P80, P86, P87, P88, P89, P90, P97, P100.

## Primary source witness
- `Autonomiczne AI w Unity.PDF`
