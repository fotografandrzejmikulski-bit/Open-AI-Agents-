# Agentic Software Factory

## Objective
Build a reusable software-production system in which AI agents handle bounded engineering stages while deterministic tooling, tests and human approval remain authoritative.

## Factory pipeline

```text
Intent
  ↓
Requirements Compiler
  ↓
Architecture Planner
  ↓
Implementation Agent
  ↓
Static Analysis
  ↓
Tests + Evals
  ↓
Security Review
  ↓
Preview Sandbox
  ↓
Human Approval (when consequential)
  ↓
Production Deploy
  ↓
Observability + Rollback
```

The supplied automation material frames coding agents such as Cursor, Windsurf and Devin as a federated orchestration layer rather than simple autocomplete. OmniCore research similarly treats the human as an intent architect and formal auditor. fileciteturn206file0L18-L31

## Maximum-practical design

### Role separation

- **Planner:** converts intent to explicit requirements, constraints and acceptance criteria.
- **Architect:** creates boundaries, contracts and dependency graph.
- **Builder:** writes code inside a restricted workspace.
- **Verifier:** runs tests, type checks, static analysis and security checks.
- **Reviewer:** compares the artifact against requirements and regression baselines.
- **Release agent:** prepares deployment only after policy gates pass.

### Shared artifacts

`requirements.yaml`, `architecture.md`, `contracts/`, `evals/`, `threat-model.md`, `release-manifest.json`, `run-state.json`.

### Execution controls

Agents receive least-privilege capabilities. Build environments are isolated. Production credentials never enter coding sandboxes. Side effects require explicit policy authorization and, when necessary, human approval.

## Recovery-first runtime

Every stage emits checkpoints. Failed steps resume from the latest valid checkpoint; release stages support rollback to the previous verified artifact.

## Quality gate

A change is releasable only when functional requirements, type contracts, tests, security checks and evaluation thresholds all pass.

## Builder integration

Visual app builders and AI IDEs are treated as interchangeable frontends to the same artifact model. The source of truth remains versioned code, schemas and runtime configuration, not the generated UI alone.