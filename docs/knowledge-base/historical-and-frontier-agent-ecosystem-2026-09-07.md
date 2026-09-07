# Historical & Frontier AI Agent Ecosystem — Knowledge Synthesis — 2026-09-07

## Scope

This document absorbs the supplied comparison of milestone autonomous agents, modern task agents, coding agents and ChatGPT/MCP integration patterns, then cross-checks the most important integration claims against current public documentation.

The purpose is not to rank products permanently. The purpose is to extract reusable **agent architecture patterns** and convert them into OmniCore design primitives.

## 1. Historical milestones

### Auto-GPT / BabyAGI pattern

The early 2023 generation established a fundamental loop:

```text
GOAL
 ↓
TASK GENERATION
 ↓
TASK PRIORITIZATION
 ↓
TOOL EXECUTION
 ↓
OBSERVATION
 ↓
TASK UPDATE
 ↓
REPEAT
```

BabyAGI's original March 2023 project explicitly introduced task planning as a method for autonomous agents; the original repository was later archived. Newer BabyAGI variants explore self-building agents and dynamic tool creation.

Architecture lesson:

`AUTONOMOUS LOOP != TRUSTED AUTONOMY`

A loop must have explicit budgets, termination criteria, capability limits, provenance and recovery semantics.

### Devin / autonomous coding-agent pattern

The coding-agent milestone demonstrates a different architecture: the agent is not merely generating code in chat; it operates over a development environment containing a repository, terminal, files, tests and execution state.

Reusable pattern:

```text
REQUIREMENT
 ↓
REPOSITORY UNDERSTANDING
 ↓
PLAN
 ↓
EDIT
 ↓
BUILD / TEST
 ↓
OBSERVE FAILURE
 ↓
REPAIR
 ↓
RETEST
 ↓
ARTIFACT / DEPLOYMENT
```

OmniCore consequence: a coding agent must be modeled as a **capability-bounded execution worker**, not as a privileged code oracle.

## 2. Contemporary task-agent pattern

### Perplexity Computer

Current documentation describes Computer as an independent digital worker that can synthesize web and work-context information, use hundreds of app connectors, create assets and functioning applications, conduct research and act on schedules.

Reusable pattern:

```text
SEARCH-NATIVE REASONING
 +
CONNECTOR FABRIC
 +
ACTION EXECUTION
 +
LONG-RUN TASK STATE
 =
GENERAL TASK WORKER
```

The key architectural idea is the combination of retrieval, tool execution and persistent task state rather than search alone.

### Manus

Current Manus documentation describes both temporary sandboxes and a persistent Cloud Computer. The desktop product can operate on local files and applications primarily through command-line execution, while the cloud computer provides persistent filesystem/process state.

Reusable distinction:

```text
EPHEMERAL SANDBOX
    ≠
PERSISTENT AGENT COMPUTER
```

Persistence must therefore be an explicit security capability with ownership, purpose, expiry, data-egress and human-approval policy.

### Zapier AI / Agents

Zapier represents the workflow/action-fabric pattern: the agent's differentiator is not necessarily model intelligence, but broad connectivity to business systems and executable workflows.

Reusable pattern:

```text
AGENT INTENT
 ↓
ACTION GRAPH
 ↓
APPLICATION CONNECTORS
 ↓
AUTHORIZATION
 ↓
SIDE EFFECT
 ↓
RESULT / AUDIT
```

This maps directly to OmniCore's Capability Broker and external data/action fabric.

## 3. Coding-agent and terminal pattern

### Claude Code

The supplied material correctly identifies the architectural class: a terminal-native coding agent that operates over repositories and development tools. The reusable design lesson is provider-independent:

```text
LLM
 ↓
CODING AGENT RUNTIME
 ↓
FILESYSTEM + TERMINAL + TESTS + VCS
 ↓
VERIFICATION GATES
```

The agent's model provider should remain replaceable. Its tool surface should be capability-scoped and auditable.

## 4. ChatGPT as an agent control plane

Current OpenAI documentation confirms that ChatGPT can use custom apps built around MCP to call approved tools and retrieve information from connected services. Full MCP support, including write/modify actions, is being rolled out in beta for Business, Enterprise and Edu plans; workspace administrators control developer-mode access and app deployment.

Therefore the source procedure should be interpreted as a **workspace/plan-dependent integration pattern**, not a universal UI guarantee.

Canonical architecture:

```text
CHATGPT / USER-FACING CONTROL PLANE
              ↓
        MCP APP / CONNECTOR
              ↓
      CAPABILITY BROKER
              ↓
     EXTERNAL AGENT SERVER
              ↓
      AGENT RUNTIME / TOOLS
              ↓
      ARTIFACT + OBSERVATION
              ↓
     VALIDATION / PROVENANCE
              ↓
        CHATGPT SYNTHESIS
```

Important: MCP is the interoperability boundary; it does not by itself establish trust, authorization or safety.

## 5. Agent-as-a-capability doctrine

An external agent should never be treated as a black-box super-tool with unrestricted authority.

Every agent adapter should expose a typed manifest:

```yaml
AgentCapabilityManifest:
  agent_id:
  provider:
  version:
  runtime:
  capabilities:
  input_schema:
  output_schema:
  side_effects:
  persistence:
  data_egress:
  credentials:
  required_scopes:
  risk_class:
  provenance:
  evaluation_profile:
  cost_profile:
  latency_profile:
  cancellation:
  checkpointing:
  artifact_contract:
```

The orchestrator then performs:

```text
DISCOVER
 ↓
PROVENANCE CHECK
 ↓
CAPABILITY FILTER
 ↓
RISK CLASSIFICATION
 ↓
AUTHORIZATION
 ↓
DELEGATION
 ↓
OBSERVE
 ↓
VALIDATE
 ↓
COMMIT / ROLLBACK
```

## 6. Nested autonomy

The major architectural breakthrough across Auto-GPT, coding agents, computer-use agents and workflow agents is that autonomy can be **nested**.

```text
OUTER SUPERVISOR
   │
   ├── RESEARCH WORKER
   │      └── autonomous research loop
   │
   ├── CODING WORKER
   │      └── edit/build/test loop
   │
   ├── COMPUTER-USE WORKER
   │      └── browser/desktop loop
   │
   └── BUSINESS-ACTION WORKER
          └── connector/workflow loop
```

The outer supervisor owns the global budget, authorization and acceptance criteria. Inner agents own local planning but cannot enlarge their authority.

Invariant:

`CHILD AGENT AUTONOMY ≤ DELEGATED CAPABILITY GRANT`

## 7. Autonomy budget

Every autonomous worker should receive a bounded execution budget:

```yaml
AutonomyBudget:
  max_steps:
  max_wall_time:
  max_tokens:
  max_tool_calls:
  max_parallel_workers:
  max_cost:
  max_retries:
  max_state_growth:
  max_data_egress:
  termination_conditions:
  escalation_policy:
```

This generalizes Project 27's reasoning budget from internal solver paths to **external agent delegation**.

## 8. Agent handoff protocol

Agents should exchange structured artifacts rather than opaque natural-language summaries whenever possible.

```yaml
AgentHandoff:
  task_id:
  parent_run_id:
  child_run_id:
  objective:
  constraints:
  authorized_capabilities:
  evidence_refs:
  assumptions:
  work_state:
  outputs:
  artifacts:
  verification_status:
  uncertainty:
  remaining_work:
  rollback_point:
```

This makes delegation resumable and prevents loss of provenance when one agent hands work to another.

## 9. Agent state classes

Agent state must be classified separately:

1. **Ephemeral context** — prompt/session-local reasoning inputs.
2. **Checkpoint state** — resumable workflow state.
3. **Persistent workspace** — files, repositories, browser state, installed tools.
4. **Credential state** — secrets and tokens; never part of ordinary agent memory.
5. **Policy state** — authorization, approvals, scopes and constraints.
6. **Evidence state** — source objects, hashes, provenance and verification status.
7. **Artifact state** — generated code, documents, builds and releases.

This extends the memory-poisoning and persistent-browser-state protections already present in Projects 26, 31, 37 and 39.

## 10. Agent-to-ChatGPT integration security

The integration boundary must defend against:

- malicious or compromised MCP servers;
- prompt injection returned by external agents;
- agent-generated tool instructions masquerading as policy;
- credential exfiltration;
- unauthorized persistent state access;
- cross-tenant state leakage;
- uncontrolled recursion between agents;
- runaway cost and tool-call loops;
- artifact provenance loss;
- false success reports;
- silent data egress to external model providers.

Canonical trust boundary:

```text
UNTRUSTED AGENT OUTPUT
        ↓
PARSE / NORMALIZE
        ↓
PROVENANCE
        ↓
SCHEMA VALIDATION
        ↓
POLICY / CAPABILITY CHECK
        ↓
EVIDENCE VALIDATION
        ↓
TRUSTED ARTIFACT / OBSERVATION
```

## 11. Agent recursion governor

Autonomous agents must not recursively spawn unrestricted agents.

```yaml
DelegationPolicy:
  max_depth:
  allowed_child_types:
  max_children_per_parent:
  inherited_capabilities:
  forbidden_capabilities:
  budget_partition:
  approval_required_for:
  recursion_timeout:
```

The child receives a strict subset of the parent's capabilities and budget unless an explicit policy transition grants more.

## 12. Agent selection / routing

The portfolio should not select an agent by popularity. Route by measured task fitness:

```text
TASK
 ↓
CAPABILITY REQUIREMENTS
 ↓
RISK / CONSEQUENCE
 ↓
PRIVACY / DATA GRAVITY
 ↓
QUALITY REQUIREMENT
 ↓
LATENCY
 ↓
COST
 ↓
PERSISTENCE REQUIREMENT
 ↓
AGENT ROUTING
```

This extends Project 17 from model routing to **agent routing**.

Example capability classes:

| Class | Best-fit worker pattern |
|---|---|
| Research | search-native / evidence agent |
| Coding | repository + terminal + test agent |
| Browser task | browser/computer-use agent |
| Business automation | connector/workflow agent |
| Local desktop | local computer agent |
| Cloud execution | disposable sandbox agent |
| Formal verification | deterministic verifier / compiler pipeline |

The table is a routing taxonomy, not a permanent vendor ranking.

## 13. Agent interoperability contract

Project 40 should standardize an OmniCore `Agent Execution Contract`:

```text
capabilities()
health()
create_session()
plan()
execute()
stream()
observe()
checkpoint()
resume()
cancel()
artifacts()
usage()
provenance()
```

Every adapter may implement only the subset supported by the underlying agent, but unsupported operations must be explicit rather than silently simulated.

## 14. Evaluation of external agents

Each external agent is evaluated independently of its marketing claims.

### Quality
- task success rate;
- factual/evidence accuracy;
- code correctness;
- artifact acceptance rate.

### Reliability
- recovery rate;
- timeout rate;
- false-success rate;
- deterministic replay success.

### Security
- unauthorized capability attempts;
- prompt-injection resistance;
- state isolation;
- credential exposure;
- data-egress violations.

### Economics
- cost per successful task;
- tool-call efficiency;
- wall-clock latency;
- resource consumption.

### Interoperability
- schema conformance;
- cancellation;
- checkpoint/resume;
- provenance preservation;
- graceful degradation.

## 15. Source-derived lessons converted into OmniCore doctrine

1. **Auto-GPT/BabyAGI:** autonomy emerges from a loop; loops require governors.
2. **Devin/Claude Code:** coding autonomy requires an executable workspace plus verification.
3. **Perplexity Computer:** search, context and actions form one task-worker substrate.
4. **Zapier:** connector breadth is a capability plane, not a substitute for policy.
5. **Manus:** computer-use and persistent environments make state security first-class.
6. **ChatGPT + MCP:** the user-facing model can serve as a control plane over approved external capabilities.
7. **MCP:** interoperability does not imply trust.
8. **Multi-agent systems:** nested autonomy is useful only when delegation is bounded.
9. **Agent routing:** route by measurable capability fitness, not vendor prestige.
10. **Agent handoff:** structured artifacts preserve provenance better than free-form summaries.

## 16. Portfolio integration

This knowledge directly strengthens:

- Project 15 — Universal Research Orchestrator
- Project 17 — Adaptive Model Router
- Project 24 — Agentic Prompt Compiler / DSL
- Project 26 — OmniCore Trustworthy Kernel
- Project 27 — Compound Reasoning / Self-Consistency
- Project 28 — Verified Code Generation
- Project 29/30 — Sugra Evidence / OSINT Fabric
- Project 31 — Sovereign Agent Operating Fabric
- Project 33 — Agentic App Builder / Delivery Control Plane
- Project 35 — Context-Aware Intent Security
- Project 37 — Sovereign Edge AI Runtime
- Project 39 — Alibaba Cloud Agent Runtime / Cloud Fabric
- Project 40 — Agent Interoperability / Meta-Orchestration Fabric

## 17. Final invariant

The strongest generalization from the historical agent ecosystem is:

`AGENT != MODEL`

and, more precisely:

`MODEL != AGENT RUNTIME != TOOL FABRIC != EXECUTION SUBSTRATE != AUTHORIZATION`

OmniCore therefore treats external agents as **versioned, measurable, capability-scoped execution workers** behind a common control plane.
