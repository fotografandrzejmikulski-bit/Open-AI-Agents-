# P100 Extension — Antigravity 2.0 Project / Plugin / Skill / Hook / SDK Control Plane

**Status:** ACTIVE / integrated
**Date:** 2026-09-12
**Parent:** P100 — NeXus AI Code / OMEGA-X Agentic Development Environment

## Purpose

Extend P100 with a governed interoperability model for Antigravity 2.0's strongest architectural primitives: Projects, Plugins, Skills, Hooks, MCP, Subagents, Artifacts, Scheduled Tasks and the Antigravity SDK.

## Target architecture

```text
OPERATOR
  ↓
ANTIGRAVITY PROJECT CONTEXT
  ↓
PROJECT POLICY + IDENTITY + CAPABILITY BROKER
  ↓
MISSION CHALLENGE / IMPLEMENTATION PLAN
  ↓
AGENT HARNESS
  ├── CUSTOM AGENT / SUBAGENT
  ├── SKILL DISCOVERY → ACTIVATION → RESOURCE LOAD
  ├── MCP FEDERATION
  ├── HOOK POLICY INTERCEPTORS
  ├── TERMINAL / BROWSER / FILE TOOLS
  └── SCHEDULED TASK CONTROLLER
  ↓
SANDBOX / EXECUTION
  ↓
AUTHORITATIVE READBACK
  ↓
VERIFY / AUDIT / ARTIFACT PROVENANCE
  ↓
HUMAN APPROVAL WHERE REQUIRED
  ↓
IDEMPOTENT PROMOTION
```

## Project security context

A P100 adapter should translate an Antigravity Project into an explicit control-plane object containing:
- project identity and lineage;
- allowed folder set;
- tool/capability allowlist;
- MCP server allowlist;
- network policy;
- secrets reference policy;
- model/version constraints;
- skill/plugin provenance requirements;
- sandbox budgets;
- approval policy;
- audit correlation ID.

The desktop Project boundary is a useful security context but is not itself the final authorization authority.

## Plugin and skill supply chain

Every external plugin/skill is handled as an artifact:

`DISCOVER → HASH → PROVENANCE → STATIC CHECK → CAPABILITY DIFF → POLICY CHECK → CANDIDATE → APPROVE → ACTIVATE`

Required records:
- plugin_id / skill_id;
- source repository or package provenance;
- content hash;
- version;
- declared tools;
- observed tools;
- MCP endpoints;
- hook definitions;
- requested permissions;
- policy decision;
- activation timestamp and actor.

Skills are instruction assets, not permission grants.

## Progressive context loader

P100 should generalize Antigravity's progressive skill disclosure:

1. **Discovery:** load only name/description/metadata.
2. **Activation:** load the selected skill instructions.
3. **Execution resources:** load only referenced files/resources required for the current operation.

Each transition is subject to provenance, ACL, prompt-injection screening and context-budget controls.

## Hook policy interceptor

Hooks are mapped to the P100 authorization lifecycle:

`PROPOSED_TOOL_CALL → PRE-TOOL POLICY → EXECUTE → POST-TOOL OBSERVATION → POSTCONDITION VERIFY`.

A hook may deny or transform an operation but cannot create authority that the policy broker has not granted. Post-tool hooks cannot substitute for authoritative verification.

## MCP federation

Antigravity MCP servers become one adapter among many in the P100 Capability Broker. Each lease should bind:
`agent_id + project_id + workflow_id + tenant + capability + server_id + scope + expiry + policy_version + correlation_id`.

Remote and local MCP transports must be treated equivalently from an authorization perspective.

## SDK bridge

The Antigravity SDK is treated as an embedded runtime surface. SDK agents must traverse the same:
`IDENTITY → POLICY → CAPABILITY → EXECUTION → READBACK → VERIFY → AUDIT` path as desktop and CLI agents.

SDK lifecycle hooks are valuable observation/control points but are not an independent security root.

## Subagent governance

Subagents inherit bounded permissions. P100 adds:
- explicit parent agent ID;
- delegation purpose;
- candidate task hash;
- maximum depth;
- tool scope;
- time/resource budget;
- cancellation authority;
- result provenance.

Dynamic delegation cannot expand privilege.

## Scheduled task governance

Scheduled tasks require:
- explicit owner;
- bounded cadence;
- expiry or review date;
- policy version;
- credential/capability lease;
- output destination;
- alert conditions;
- cancellation path;
- execution audit.

A scheduled task is a durable workflow, not a perpetual agent permission.

## Artifact governance

Artifacts and implementation plans are treated as reviewable intermediate representations:
`ARTIFACT_CREATED → PROVENANCE → REVIEW → FEEDBACK → REVISION → VERIFY`.

Visual artifacts are evidence of what the agent rendered/generated, not proof that the underlying runtime is correct.

## Model lifecycle

Model identity must be versioned. P100 must not encode Gemini 3.5 Flash as a permanent assumption. The official September 2026 changelog already records Gemini 3.8 Flash in AGY Enterprise, so routing must support model/version drift and deprecation-aware provenance.

## Required invariants

`MODEL_OUTPUT ≠ AUTHORIZATION`

`PROJECT_SCOPE ≠ AUTHORIZATION`

`PLUGIN_MANIFEST ≠ TRUST`

`SKILL_INSTRUCTION ≠ PERMISSION`

`MCP_CAPABILITY ≠ PERMISSION`

`HOOK_ALLOW ≠ FINAL_AUTHORIZATION`

`SUBAGENT ≠ INDEPENDENT_AUTHORITY`

`SANDBOX_PASS ≠ PRODUCTION_APPROVAL`

`ARTIFACT ≠ VERIFIED_RUNTIME`

`SDK_RUNTIME ≠ POLICY_BYPASS`

`SCHEDULED_TASK ≠ UNBOUNDED_PERSISTENCE`

`TOOL_RESULT ≠ POSTCONDITION`

## Implementation priority

**P0:** project security context + capability broker mapping.

**P0:** plugin/skill provenance and activation ledger.

**P0:** hook interception adapter and authoritative postcondition verification.

**P1:** MCP federation adapter with ephemeral capability leases.

**P1:** SDK runtime bridge.

**P1:** bounded subagent delegation.

**P1:** scheduled-task policy controller.

**P2:** artifact UX / implementation-plan federation.

## Decision

Integrate as a P100 extension. Do not create a new portfolio project. Antigravity 2.0 is a reference implementation/benchmark for the P100 neutral agent control plane, not its trust authority.
