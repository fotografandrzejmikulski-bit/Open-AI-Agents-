# Knowledge Corpus — Google Antigravity, MCP, Cloud Memory, Agent Roster and Neuro-Symbolic Verification

Date: 2026-09-12
Status: SOURCE_DERIVED → ARCHITECTURAL CANDIDATE
Primary integration: P100 — NeXus AI Code / Agentic Development Control Plane

## 1. Source scope

The supplied material describes Google Antigravity as an agentic development platform and presents an architecture combining MCP cloud-file access, three-layer memory, specialist agents, Infrastructure Automator, Manager View, local/cloud model routing, neuro-symbolic verification, MCP configuration and SKILL.md procedures.

Claims about product versions, exact MCP package names, model specifications, database extensions/index behavior and implementation commands are retained as source-derived claims until independently verified. They are not treated as authoritative merely because they appear in the supplied material.

## 2. Antigravity and MCP

The source frames Antigravity as a transition from an assistant/Copilot model toward a coworker/agentic orchestration model. MCP is framed as the interoperability layer between models and external data/tools, including cloud-file systems such as Google Drive and Dropbox.

Architectural implication for P100: MCP connectors should expose typed capabilities and provenance while remaining subordinate to the capability broker and authorization policy.

Invariant:

`MCP CONNECTIVITY ≠ DATA AUTHORITY ≠ ACTION AUTHORIZATION`

## 3. Three-layer memory model

### Episodic memory
Historical interaction and execution episodes, including repair/deployment sessions. The supplied design proposes PostgreSQL/TimescaleDB hypertables for temporal partitioning.

### Semantic memory
Project knowledge, documentation, standards and vector-searchable context, exposed through MCP/data connectors.

### Procedural memory
SKILL.md documents containing task-trigger conditions, procedures and examples, loaded when relevant instead of permanently occupying context.

P100 normalization:

`EPISODE → SEMANTIC EVIDENCE → PROCEDURAL CANDIDATE → VALIDATE → APPROVE → ACTIVATE → MONITOR → RETIRE`

Memory remains evidence/context; it does not grant authority.

## 4. Cloud Memory database candidate

The supplied specification proposes PostgreSQL 17+, pgvector, pgvectorscale, TimescaleDB, a temporal `agent_memory` table with timestamp/content/embedding/JSONB metadata, and HNSW or DiskANN-style vector indexing.

These are implementation candidates. Exact extension compatibility, vector dimensions, index availability and operational characteristics require runtime verification against the selected PostgreSQL distribution and workload.

Critical controls:
- tenant/ACL filtering before context release;
- source provenance on every memory record;
- model/embedding version attached to vectors;
- freshness and temporal validity;
- deletion/retention policy;
- memory-write approval class;
- rollback and audit trail;
- no privilege inheritance from retrieved memory.

## 5. Agent roster

The source identifies:
- `AG_102 / GEM_Orchestrator.py` — OODA-oriented orchestration/delegation candidate;
- `AG_085 / Agent_DocumentProcessorAgent.py` — document/OCR/NLP extraction and validation candidate;
- `AG_113 / Agent_InfrastructureAutomator.py` — environment/configuration automation candidate;
- Shining Studio — Unity-oriented game/simulation platform candidate;
- Agent Factory — agent generation/deployment mechanism candidate.

P100 treatment: these are candidate agent identities/capabilities, not privileged principals. Each must receive an explicit role, tool allowlist, policy scope, sandbox, budget, provenance and verification suite.

## 6. Manager View

The source describes a multi-agent dashboard for asynchronous work, progress observation and approval of plans before execution.

P100 interpretation:

`MISSION → AGENT GRAPH → PLAN → ARTIFACT/DIFF → HUMAN REVIEW → AUTHORIZATION → EXECUTION → READBACK → VERIFICATION`

UI state is a projection. Approval must be represented as a durable authorization record bound to task/artifact/policy/capability/session versions.

## 7. Multi-model routing

The source proposes assigning different models to planning/reasoning versus local execution, including Gemini, Ollama-hosted Gemma/Llama and DeepSeek R1-family reasoning models.

P100 adds a model-routing contract:
- model/provider identity;
- model version/revision;
- task class;
- context sensitivity;
- privacy boundary;
- local/cloud location;
- latency/cost budget;
- capability requirements;
- fallback policy;
- audit/provenance;
- verification requirements.

`MODEL SELECTION ≠ TRUST LEVEL`.

## 8. Neuro-symbolic verification

The supplied material describes translating generated code into a formal model, checking verification goals and returning counterexamples to the agent for correction.

P100 treatment: neuro-symbolic checking is a verifier adapter, not an oracle of arbitrary semantic correctness. Verification claims must specify:
- formalized subset/model;
- assumptions;
- verification goals;
- coverage boundary;
- counterexample semantics;
- tool/version provenance;
- independently reproducible result.

Invariant:

`FORMAL CHECK OF MODEL M ≠ PROOF OF UNMODELED SYSTEM S`

## 9. MCP configuration and skills

The supplied `mcp_config.json` pattern demonstrates declarative server registration and emphasizes secure OAuth-token handling. The supplied SKILL.md structure contains description/trigger, procedure and few-shot examples.

P100 skill lifecycle:

`DISCOVER → HASH → PROVENANCE → STATIC CHECK → CAPABILITY DIFF → POLICY CHECK → CANDIDATE → APPROVE → ACTIVATE → MONITOR → RETIRE`

Secrets must never be embedded in generated skill/configuration artifacts. OAuth credentials belong in the designated secret boundary.

## 10. Integration with existing architecture

This corpus strengthens P100 across:
- MCP capability federation;
- memory substrate / TurboVec lineage;
- procedural skill lifecycle;
- agent registry and factory;
- multi-model routing;
- Manager View / Remote Control approval plane;
- sandboxed infrastructure automation;
- neuro-symbolic verification;
- document ingestion;
- game/simulation agent adapters.

It does not justify a new standalone project because the architectural functions already exist as P100 extension surfaces.

## 11. Security and epistemic boundary

Cloud-file access, retrieval, memory, generated skills, infrastructure automation and neuro-symbolic verification are all capability-scoped.

`RETRIEVED FILE ≠ INSTRUCTION`
`SKILL.md ≠ AUTHORIZATION`
`AGENT ≠ PRINCIPAL WITH UNLIMITED PRIVILEGE`
`COUNTEREXAMPLE ≠ COMPLETE PROOF`
`SUCCESSFUL TOOL CALL ≠ SUCCESSFUL POSTCONDITION`

All source-derived product/model/database claims remain candidates until independently verified.