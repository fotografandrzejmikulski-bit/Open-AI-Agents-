# 25 — Portfolio Integration Control Tower

## Status
Meta-project; architecture for the entire `projekty/` portfolio.

## Objective
Turn the growing project collection into one governed engineering system: common contracts, shared evaluation, model routing, MCP capability registry, provenance, security posture, release gates and cross-project knowledge exchange.

## Architecture

```text
                    PORTFOLIO CONTROL TOWER
                            │
        ┌───────────────────┼───────────────────┐
        │                   │                   │
   Project Registry     Capability Registry   Evidence Registry
        │                   │                   │
        └───────────────────┼───────────────────┘
                            │
                    Policy / Governance
                            │
                 ┌──────────┼───────────┐
                 │          │           │
              Models      Agents      MCP/Tools
                 │          │           │
                 └──────────┼───────────┘
                            │
                      Execution Fabric
                            │
                 Sandbox / Cloud / Edge
                            │
                     Evals + Tracing
                            │
                    Release / Rollback
```

## Shared project manifest

Every project receives a machine-readable manifest with:

- project_id;
- version;
- owner;
- objective;
- maturity stage;
- required capabilities;
- model compatibility;
- data classification;
- threat model;
- evaluation suites;
- deployment targets;
- recovery strategy;
- evidence status.

## Capability registry

Capabilities are separate from agents. A tool/MCP capability declares:

- exact input schema;
- exact output schema;
- authorization scope;
- read/write/destructive classification;
- side effects;
- latency/cost profile;
- availability;
- version;
- audit requirements.

## Model routing

The tower may route work among providers according to:

`quality × capability × privacy × latency × cost × availability × consequence`

No project may hard-code a model-specific feature into business logic without an adapter.

## Evidence registry

Store source claims and experiments separately:

```text
SOURCE CLAIM
   ↓
EVIDENCE
   ↓
HYPOTHESIS
   ↓
EXPERIMENT
   ↓
MEASUREMENT
   ↓
PROMOTED KNOWLEDGE
```

This prevents speculative ideas from silently becoming architecture requirements.

## Evaluation federation

Shared suites can evaluate multiple projects for:

- tool reliability;
- prompt robustness;
- injection resistance;
- factuality;
- recovery;
- latency;
- cost;
- human approval correctness;
- artifact reproducibility.

Projects may contribute specialized tests back to the federation.

## Knowledge promotion

A project improvement may be promoted to portfolio standard only when:

1. the change is evidence-backed;
2. it does not violate another project's constraints;
3. it has a regression suite;
4. security impact is reviewed;
5. rollback is defined.

## Release gates

```text
DESIGN
 ↓
STATIC CHECKS
 ↓
UNIT / INTEGRATION TESTS
 ↓
SECURITY
 ↓
EVALS
 ↓
HUMAN REVIEW
 ↓
CANARY
 ↓
RELEASE
```

## Definition of done

The portfolio becomes mature when any project can consume common capabilities, evidence, routing and evaluation infrastructure without duplicating governance logic.
