# Open-AI-Agents-

Reference repository for the project's **agent engineering knowledge base and project portfolio**.

This repository is intentionally separated from the **Agents for Humans Hackathon** submission repository. It is the long-lived research, architecture and project layer; the hackathon repository contains only the CogniSync submission and its proof artifacts.

## Repository roles

### `docs/knowledge-base/`

Source-grounded and research-derived knowledge covering:

- OpenAI Agents SDK and agent runtime patterns;
- MCP, MCP Apps, tool discovery, deferred loading and capability filtering;
- Skills, plugin architecture, packaging, authentication and safety;
- sandbox agents and execution boundaries;
- memory, state, orchestration, handoffs and guardrails;
- model selection and provider strategy;
- agentic application builders;
- research, OSINT and evidence systems;
- multimodal systems and adaptive reasoning;
- local/edge AI and sovereign execution;
- cognitive and influence security;
- systems engineering, databases, data warehouses and data mining;
- machine-learning and mathematical foundations;
- professional artifact generation and evidence-backed document workflows;
- the supplied project-owner PDF corpus.

### `projekty/`

Build-oriented project specifications derived from the knowledge base. Projects are treated as engineered systems rather than prompt-only concepts and are expected to define:

`problem → scope → architecture → contracts → security → verification → evaluation → roadmap`

The portfolio includes agent platforms, security labs, local AI infrastructure, multimodal systems, creative tooling, research orchestration, verified code generation and human-agency protection.

## Evidence discipline

Every important claim should be classified as one of:

**source-derived claim → engineering hypothesis → verified behavior → future roadmap**

External references, benchmark numbers and provider capabilities must not be promoted to verified facts without validation.

## Shared engineering doctrine

The portfolio favors a common control-plane model:

```text
Intent
  ↓
Context / Evidence
  ↓
Capability Discovery
  ↓
Reasoning / Planning
  ↓
Policy / Authorization
  ↓
Verification
  ↓
Human Decision Boundary
  ↓
Execution
  ↓
Observation / Audit
```

Core invariants include:

- model capability is not authorization;
- memory is not authorization;
- approval is not execution;
- external completion requires connector confirmation;
- unknown capability is handled fail-closed;
- consequential actions require an explicit policy path;
- security analysis is stateful across the interaction trajectory;
- human agency is preserved as a system property.

## Latest corpus integrations

The September 2026 supplied corpus has been absorbed into:

- `docs/knowledge-base/systems-engineering-data-intelligence-ml-foundations-2026-09-09.md`
- `docs/knowledge-base/professional-artifact-and-evidence-compiler.md`
- `projekty/59-omnicore-telephony-esim-capability-broker-fabric-max.md`
- `projekty/60-omnicore-systems-engineering-and-intelligence-foundry-max.md`

Project 59 provides the governed telecom/eSIM capability plane. Project 60 consolidates systems analysis, data architecture, data mining, ML foundations, mathematical representation, AI-assisted systems engineering and evidence-backed artifact generation.

## Flagship implementation

The current flagship external submission is **CogniSync Professional**, maintained separately in:

`Agents-for-Humans-Hackathon`

That repository is deliberately judgeable without requiring the entire research portfolio.

## Working status

The knowledge base and portfolio are actively evolving. Individual entries can be at different maturity levels; repository status should always be inferred from the file itself and its evidence classification rather than from a single global maturity label.

## Navigation

- [`docs/knowledge-base/`](docs/knowledge-base) — knowledge and research corpus
- [`projekty/`](projekty) — engineered project portfolio
