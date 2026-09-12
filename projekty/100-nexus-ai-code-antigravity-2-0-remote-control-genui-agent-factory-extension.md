# P100 Extension — Antigravity 2.0 Remote Control / Mission Graph / GenUI / Agent Factory

## Classification
Direct extension of P100 NeXus AI Code OMEGA-X. No new project.

## Strategic trigger
A new Antigravity architecture report was compared against current official Google Antigravity documentation and the existing P100 architecture.

## Verified external benchmark
Google Antigravity 2.0 is documented as a standalone agent command center with synchronous/asynchronous agents, system/file/web capabilities, skills, MCP, subagents, Chrome interaction and artifact/implementation-plan workflows. Current documentation also exposes Remote Control, project-scoped permissions/settings, worktrees, browser automation, Git-native review and agent-edit diffs.

## P100 adoption

### 1. Mission Graph
Add a graph projection over the existing agent registry and execution journal.

Nodes:
- agent;
- subagent;
- capability;
- artifact;
- approval;
- execution;
- verifier;
- external runtime.

Edges:
- delegation;
- dependency;
- dataflow;
- blocking;
- authorization;
- evidence lineage.

The graph is a projection. It never becomes the authority for permissions or factual state.

### 2. Decision Surface / GenUI
Add a provider-neutral structured decision surface. A2UI is a candidate protocol adapter, but P100 must support catalog/version negotiation and maintain compatibility with newer A2UI revisions rather than hard-code legacy v0.8.

A decision surface must carry:
- decision_id;
- subject;
- risk classification;
- available actions;
- evidence/artifacts;
- authorization scope;
- expiration/freshness;
- actor identity;
- postcondition contract.

The UI action creates an authorization transition; it does not directly execute arbitrary commands.

### 3. Artifact Review Plane
Promote plans, diffs, screenshots, browser recordings, test results and architecture diagrams to first-class P100 artifacts.

Artifact state:

GENERATED → OBSERVED → REVIEWED → AUTHORIZED → EXECUTED → VERIFIED → ACCEPTED/REJECTED

Annotations and human feedback become durable, correlated evidence rather than transient chat text.

### 4. Remote Control Plane
P100 should support browser/mobile remote control of long-running local agent sessions without exposing a general-purpose shell.

Remote capability classes:
- status;
- artifacts;
- approvals;
- bounded steering;
- terminate/cancel;
- evidence/readback.

Remote transport can use an outbound-only tunnel and Zero Trust access policy. Transport security does not replace local capability authorization.

### 5. Persistent Agent Registry
Extend the existing OCN registry with project-scoped agent packages:

```text
.agents/
  agents/
    <agent-id>/
      agent.md
      skills/
      tools/
      policy/
      tests/
      provenance/
```

Agent definitions are versioned candidate artifacts. A file watcher may detect changes but may not activate privileged capabilities without validation and authorization.

### 6. Agent Factory / Meta-Orchestrator
Add a bounded meta-agent that can propose specialized agents from project needs.

Lifecycle:

DISCOVER GAP
→ GENERATE CANDIDATE
→ SCHEMA VALIDATE
→ STATIC CHECK
→ SANDBOX TEST
→ POLICY CHECK
→ AUTHORIZE
→ REGISTER
→ ACTIVATE
→ MONITOR
→ VERIFY
→ ROLLBACK

The meta-agent cannot grant itself capabilities, alter authorization policy, bypass verification, or promote its own candidate directly.

### 7. Dynamic subagent orchestration
The P100 scheduler should support parallel specialized subagents while retaining a single capability/policy boundary. Subagent lifecycle events must be journaled and linked to the parent task.

### 8. Remote approval freshness
Approvals arriving from a remote surface must be bound to:
- task version;
- artifact hash/version;
- policy version;
- requested capability;
- actor/session identity;
- expiration;
- nonce or replay protection.

Stale approvals cannot authorize newer state.

## Competitive position

Antigravity demonstrates that agentic development has expanded from IDE assistance toward command-center orchestration, artifacts, subagents, MCP/skills and remote control. P100 therefore should not compete merely as another agentic IDE.

P100's differentiating objective remains a provider-neutral control plane spanning:

```text
Antigravity / IDEs / Unity / Unreal / Android / Web / Local Runtimes / Cloud Runtimes
                              ↓
                       P100 CONTROL PLANE
                              ↓
              IDENTITY / POLICY / CAPABILITIES
                              ↓
                  MCP / AGENTS / SANDBOXES
                              ↓
                    READBACK / VERIFY
                              ↓
                    ARTIFACT / AUDIT LEDGER
```

## Non-adopted assumptions

- A dedicated Flutter mobile app is not required as the first remote-control surface; current Antigravity evidence demonstrates browser-based remote control.
- A2UI v0.8 is not treated as the current canonical protocol version.
- "Self-healing" is not treated as permission to self-modify privileged runtime policy.
- Hot-loading is not authorization.
- Remote transport is not execution authority.
- Graph visualization is not authoritative system state.

## Verification requirements

1. Graph projection consistency against authoritative journal state.
2. Decision-surface schema and catalog compatibility tests.
3. Approval replay/staleness tests.
4. Remote-control privilege-boundary tests.
5. Agent-package signature/provenance tests.
6. Sandbox promotion tests for generated agents.
7. Capability-escalation and confused-deputy tests.
8. Artifact lineage and hash continuity tests.
9. Subagent cancellation and parent/child lifecycle tests.
10. Rollback tests after failed agent activation.

## Source witnesses
- Google Antigravity official documentation and current changelog.
- A2UI protocol documentation.
- Cloudflare Tunnel / Access documentation.
- User-supplied Antigravity strategic architecture report.
- Existing P100 OMEGA-X architecture.
