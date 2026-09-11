# GitHub DevSecOps & Agent Engineering Corpus — 2026-09-11

## Corpus status

`SOURCE INGESTED → EXTERNAL-VERIFIED REFERENCE KNOWLEDGE → PROJECT IMPACT ANALYSIS`

This artifact consolidates the GitHub/GitHub-adjacent links supplied for study. It records reusable engineering principles and their impact on the portfolio. External documentation is treated as reference evidence; it does not prove that an equivalent feature is already implemented in `Knowledge-projects`.

## Source families

- GitHub Docs repository and contribution model.
- GitHub repositories, organization/project/package surfaces and repository query patterns.
- GitHub Codespaces and dev-container configuration/security.
- GitHub Artifact Metadata and artifact provenance concepts.
- GitHub CodeQL, code scanning, CLI, query packs and model packs.
- GitHub Apps / short-lived installation tokens and least-privilege permissions.
- Official Model Context Protocol repository/specification.
- GitHub Marketplace Apps and Actions.
- GitHub Community as a feedback/discovery loop.
- GitHub public roadmap as a product-planning reference model.
- npm documentation and dependency/package governance.
- Electron security guidance.
- Open Source Guides and repository/project presentation patterns.

## 1. GitHub as an engineering control plane

GitHub should be modeled as more than source hosting. The useful control-plane surfaces are:

```text
REPOSITORY
 ├── SOURCE
 ├── ISSUES / DISCUSSION
 ├── PROJECTS
 ├── ACTIONS / CI
 ├── CODE SECURITY
 ├── PACKAGES / ARTIFACTS
 ├── CODESPACES
 ├── APPS / INTEGRATIONS
 └── RELEASE / PROVENANCE
```

For the portfolio, this reinforces the separation between source truth, planning state, CI evidence, artifacts and deployed runtime state.

## 2. Codespaces / environment-as-code

GitHub Codespaces is a dedicated, configurable development environment. Repository-level dev-container configuration can define the working environment so a new environment contains the required project setup. Security guidance emphasizes isolated environments, trusted repositories, dependency hygiene and development environment secrets.

Reusable principle:

`BUILD ENVIRONMENT = VERSIONED PROJECT ARTIFACT`

This is applicable to P100 and the wider repository verification fabric. It should not be confused with production runtime isolation.

## 3. CodeQL as code-as-data security analysis

CodeQL treats supported source code as queryable data. The workflow is conceptually:

```text
SOURCE
  ↓
CODEQL DATABASE
  ↓
QUERIES / QUERY PACKS / MODELS
  ↓
FINDINGS
  ↓
SARIF / CODE-SCANNING ALERTS
```

GitHub documentation explicitly lists Java/Kotlin among supported compiled languages, alongside C/C++, C#, Go, JavaScript/TypeScript, Python, Ruby, Rust and Swift. GitHub Actions workflows are also analyzable.

CodeQL packs separate reusable queries, libraries and model packs. Query packs bundle compiled queries and dependencies for more consistent execution. Model packs can extend analysis for frameworks not recognized by default, where supported.

Reusable principle:

`SECURITY ANALYSIS = QUERYABLE EVIDENCE, NOT A VAGUE CHECKMARK`

The repository should distinguish CodeQL configuration, CodeQL execution, findings and remediation evidence.

## 4. Artifact provenance and digest discipline

The supplied GitHub Artifact Metadata reference establishes a useful artifact-lifecycle model: artifacts should be associated with identity, digest and provenance/deployment context rather than being treated as anonymous build outputs.

Portfolio implication:

```text
SOURCE COMMIT
    ↓
BUILD
    ↓
ARTIFACT DIGEST
    ↓
PROVENANCE
    ↓
ENVIRONMENT / DEPLOYMENT RECORD
    ↓
RUNTIME VERIFICATION
```

A passing build is not proof that the deployed artifact is the artifact that was built, nor that the runtime behaves as intended.

## 5. GitHub Apps and least privilege

GitHub App installation-token patterns reinforce short-lived, scoped credentials and least-privilege permissions. The agent architecture should therefore prefer capability-scoped, expiring credentials over broad persistent tokens where an integration supports them.

This strengthens the repository invariant:

`CAPABILITY ≠ AUTHORIZATION ≠ CREDENTIAL`

A tool can exist, an agent can request it, and a credential can be technically capable of performing it without any of those facts alone authorizing the action.

## 6. MCP standardization

The official Model Context Protocol repository provides the specification, schema and documentation. MCP should be treated as a capability integration protocol with explicit client/server roles, capability negotiation, typed tools/resources/prompts and versioned protocol contracts.

The important portfolio rule remains:

`MCP EXPOSURE → CAPABILITY DISCOVERY → POLICY/AUTHORIZATION → EXECUTION`

not:

`MCP TOOL EXISTS → AGENT MAY EXECUTE`

Tool schemas and annotations are useful for interoperability and reasoning, but untrusted metadata must not become the sole security authority.

## 7. Marketplace / ecosystem architecture

GitHub Marketplace demonstrates a distribution layer for Apps and Actions. For agent systems this suggests a separation between:

- capability implementation;
- packaging;
- discovery/installation;
- permission grant;
- runtime authorization;
- versioning;
- security evidence.

An installable agent/tool is not automatically trusted merely because it is discoverable through a marketplace.

## 8. Electron security

Electron guidance materially strengthens P100 because P100 is explicitly an Electron/VS Code-oriented product concept.

Relevant controls include:

- current Electron/runtime versions;
- context isolation;
- sandboxing;
- restrictive Content Security Policy;
- HTTPS/WSS for remote content;
- no insecure content mixed into privileged windows;
- restricted navigation and window creation;
- sender validation for IPC;
- minimal preload/API exposure;
- dependency scrutiny;
- avoiding unsafe external-command/browser bridges;
- treating remote content as untrusted.

The desktop UI is therefore a security boundary, not merely a presentation layer.

## 9. npm dependency governance

The npm corpus strengthens dependency governance as part of the software supply chain. Dependency selection, update policy, package provenance and security review belong in the engineering lifecycle rather than being deferred to deployment.

Reusable principle:

`DEPENDENCY GRAPH = PART OF THE ARTIFACT'S SECURITY CONTEXT`

## 10. Documentation as an agent-readable system

GitHub Docs and related documentation patterns show that documentation can expose structured, machine-consumable information for AI agents. For this repository, project READMEs, knowledge artifacts and machine-readable portfolio deltas should therefore preserve explicit terminology, evidence classes, contracts and lifecycle states.

Documentation is an engineering interface:

`HUMAN READER ↔ DOCUMENTATION ↔ AGENT CONTEXT COMPILER`

## 11. Feedback and roadmap loops

GitHub Community and public-roadmap structures provide a useful product-learning model:

```text
USER / DEVELOPER SIGNAL
      ↓
ISSUE / DISCUSSION / FEEDBACK
      ↓
TRIAGE
      ↓
ROADMAP / PROJECT
      ↓
IMPLEMENTATION
      ↓
RELEASE
      ↓
OBSERVED OUTCOME
      ↺
```

This is relevant to P100 and future agent-product governance but does not imply that every GitHub workflow should be copied literally.

## 12. Portfolio impact

### P100 — NeXus AI Code OMEGA-X

Highest-impact project. The corpus strengthens:

- Codespaces/dev-container reproducible development environments;
- CodeQL/SAST security gates for supported languages, especially TypeScript/JavaScript/Rust/Kotlin/Java paths;
- artifact digest/provenance and deployment records;
- GitHub App least-privilege credential adapters;
- GitHub Projects/Issues/Actions/Packages as an integrated engineering control plane;
- MCP capability/authorization separation;
- Marketplace-style capability packaging and discovery;
- Electron security hardening;
- npm dependency/supply-chain governance.

No new project is required because these are direct extensions of P100's existing developer-environment/control-plane mission.

### P117 — NeXus Mobile Multimodal Agent Runtime MAX

The corpus strengthens the release and verification boundary:

`Android source → reproducible build → SAST/CodeQL → signed/digested artifact → deployment record → device/runtime readback`.

CodeQL is directly relevant to Java/Kotlin analysis. Artifact provenance is relevant to APK/AAB release identity. Codespaces are useful as a reproducible development option but are not part of the mobile runtime itself.

### P119 — OmniMAS Local Android Agent Runtime MAX

The supplied Kotlin implementation now supersedes the earlier intake assumption that Kotlin implementation files were absent. The runtime has direct implementation evidence for Planner/LLM decisioning, Grounding, Execution, task memory, notification capture and the mission loop.

The external GitHub corpus adds:

- CodeQL/SAST as a future CI gate;
- reproducible build configuration;
- dependency governance;
- APK/AAB digest and provenance requirements;
- separation of build evidence from deployment/runtime evidence.

It does not prove that these controls are currently implemented.

### P114 / assurance lineage

The corpus reinforces reusable assurance concepts already represented in P114/P72: evidence chains, artifact identity, security scanning and promotion gates should remain separate from model output and UI state.

### No new numbered project

No distinct project is justified by this corpus. The material is predominantly cross-cutting DevSecOps/control-plane knowledge and maps cleanly into P72/P100/P117/P119/P114.

## 13. Canonical engineering lifecycle added to the knowledge graph

```text
INTENT
 ↓
CONTEXT / SOURCE
 ↓
PLAN
 ↓
AUTHORIZE
 ↓
IMPLEMENT
 ↓
TEST
 ↓
SAST / CODEQL
 ↓
BUILD
 ↓
ARTIFACT DIGEST
 ↓
PROVENANCE
 ↓
DEPLOY
 ↓
AUTHORITATIVE READBACK
 ↓
VERIFY
 ↓
AUDIT / RELEASE EVIDENCE
```

This is an engineering synthesis from the supplied sources and existing repository doctrine, not a claim that the entire lifecycle is already automated.

## Evidence boundaries

- GitHub documentation claims: **EXTERNAL-VERIFIED CONTEXT**.
- MCP specification concepts: **EXTERNAL-VERIFIED CONTEXT**.
- Project mappings: **INFERRED / ARCHITECTURE SYNTHESIS**.
- P100/P117/P119 implementation status: must be supported by repository/source evidence independently of the external documentation.
- CodeQL execution in this repository: **NOT VERIFIED by this corpus**.
- Artifact provenance implementation in this repository: **NOT VERIFIED by this corpus**.
