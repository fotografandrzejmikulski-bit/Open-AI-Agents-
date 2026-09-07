# 40 — OmniCore Agent Interoperability & Meta-Orchestration Fabric MAX

## Cel projektu

Zbudować warstwę, która pozwala OmniCore/ChatGPT nie tylko korzystać z narzędzi, ale **delegować całe zadania do zewnętrznych agentów** — research agents, coding agents, browser/computer agents, workflow agents, local agents i cloud agents — przy zachowaniu jednego modelu bezpieczeństwa, provenance, budżetów, polityk i weryfikacji.

Projekt wyciąga wspólny wzorzec z historycznych agentów autonomicznych, współczesnych agentów zadaniowych, agentów programistycznych i MCP:

```text
CHATGPT / OMNICORE CONTROL PLANE
              ↓
       AGENT ROUTER
              ↓
      AGENT CAPABILITY
        REGISTRY
              ↓
 ┌────────────┼────────────┐
 │            │            │
Research    Coding      Computer
Agent       Agent       Agent
 │            │            │
 └────────────┼────────────┘
              ↓
      EXECUTION WORKER
              ↓
       OBSERVATION / ARTIFACT
              ↓
    VERIFICATION / PROVENANCE
              ↓
       CONTROL PLANE
```

## 1. Fundamental thesis

History of agentic AI shows a progression:

```text
LLM
 ↓
LLM + TASK LOOP
 ↓
LLM + TOOLS
 ↓
LLM + WORKSPACE
 ↓
LLM + PERSISTENT STATE
 ↓
LLM + MULTIPLE SPECIALIZED WORKERS
 ↓
CONTROL PLANE + AGENT ECOSYSTEM
```

The final abstraction is not “one super-agent”. It is a **governed federation of specialized execution workers**.

## 2. Agent classes

### A. Autonomous-loop agents

Inspired by Auto-GPT/BabyAGI:

- goal decomposition;
- task generation;
- prioritization;
- execution;
- observation;
- iterative replanning.

### B. Coding agents

Inspired by Devin/Claude Code:

- repository inspection;
- terminal execution;
- code editing;
- build/test/repair loop;
- artifact production.

### C. Research agents

Inspired by search-native task agents:

- web search;
- source aggregation;
- evidence graph construction;
- citation/provenance;
- scheduled monitoring.

### D. Computer-use agents

Inspired by Manus and similar general agents:

- browser interaction;
- desktop interaction;
- GUI state observation;
- local/cloud workspace execution.

### E. Workflow agents

Inspired by Zapier-like automation:

- connector discovery;
- application actions;
- multi-step business workflows;
- event-driven execution.

### F. Sovereign/local agents

Derived from Projects 10, 21 and 37:

- local model;
- local filesystem;
- local terminal;
- mobile/edge execution;
- privacy-preserving routing.

## 3. Agent Capability Manifest

Every external agent is represented by a typed manifest:

```yaml
AgentCapabilityManifest:
  agent_id:
  provider:
  version:
  runtime:
  capabilities: []
  input_schema:
  output_schema:
  side_effects: []
  persistence:
  data_egress:
  credentials:
  required_scopes: []
  risk_class:
  provenance:
  evaluation_profile:
  cost_profile:
  latency_profile:
  supported_operations:
  cancellation:
  checkpointing:
  artifact_contract:
```

No external agent is eligible for delegation without a manifest.

## 4. Agent routing

Project 17 routes among models. Project 40 routes among **agents**.

```text
TASK
 ↓
INTENT / CONSEQUENCE
 ↓
CAPABILITY REQUIREMENTS
 ↓
DATA / PRIVACY PROFILE
 ↓
PERSISTENCE REQUIREMENT
 ↓
LATENCY / COST BUDGET
 ↓
AVAILABLE AGENT MANIFESTS
 ↓
ROUTING SCORE
 ↓
DELEGATION PLAN
```

Example scoring vector:

```text
AgentScore =
  quality_fit
+ capability_fit
+ evidence_fit
+ privacy_fit
+ reliability_fit
+ latency_fit
+ recovery_fit
- cost
- risk
- data_egress
```

Weights are task-specific and versioned.

## 5. Delegation contract

The outer controller must never delegate an unbounded objective such as “do whatever is necessary”.

Instead:

```yaml
Delegation:
  parent_run_id:
  child_agent_id:
  objective:
  acceptance_criteria:
  allowed_capabilities:
  forbidden_capabilities:
  data_scope:
  domain_scope:
  max_steps:
  max_wall_time:
  max_cost:
  max_tool_calls:
  max_children:
  max_data_egress:
  persistence_policy:
  approval_requirements:
  termination_conditions:
```

Invariant:

`CHILD AUTHORITY ⊆ DELEGATED AUTHORITY`

## 6. Nested autonomy governor

External agents may internally plan and iterate, but their autonomy remains bounded by the parent control plane.

```text
PARENT
 ↓
DELEGATION GRANT
 ↓
CHILD AGENT
 ↓
CHILD PLAN
 ↓
CHILD TOOL CALL
 ↓
LOCAL POLICY
 ↓
OBSERVATION
 ↓
CHILD RESULT
 ↓
PARENT VALIDATION
```

The child cannot:

- increase its own capability grant;
- create an unrestricted child hierarchy;
- extend credentials beyond expiry;
- alter parent policy;
- silently export protected data;
- mark its own unverified artifact as trusted.

## 7. Agent Execution Contract

Common adapter API:

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

Adapters must report unsupported operations explicitly.

This allows the same OmniCore control plane to supervise very different workers without pretending they are identical internally.

## 8. Structured Agent Handoff

Free-form summaries are insufficient for high-value delegation.

```yaml
AgentHandoff:
  task_id:
  parent_run_id:
  child_run_id:
  objective:
  constraints:
  capabilities_used: []
  evidence_refs: []
  assumptions: []
  observations: []
  outputs: []
  artifacts: []
  verification_status:
  uncertainty:
  failures: []
  remaining_work: []
  rollback_point:
```

Every claim or artifact returned by a child should remain traceable to the child run, tools, sources and policy decisions that produced it.

## 9. State isolation

The fabric distinguishes:

```text
EPHEMERAL CONTEXT
CHECKPOINT STATE
PERSISTENT WORKSPACE
CREDENTIAL STATE
POLICY STATE
EVIDENCE STATE
ARTIFACT STATE
```

Persistent browser state, local files, installed tools and cloud workspaces are privileged capabilities. They are never inferred to be safe merely because an agent is running in a sandbox.

## 10. MCP boundary

MCP is the primary interoperability mechanism for tool-backed agents and external services, but it is not the security policy itself.

Required flow:

```text
DISCOVER
 ↓
PROVENANCE
 ↓
CAPABILITY FILTER
 ↓
TRUST EVALUATION
 ↓
AUTHORIZE
 ↓
MCP CALL
 ↓
OUTPUT VALIDATION
 ↓
AUDIT
```

The same boundary applies when ChatGPT invokes an MCP-backed application or when an OmniCore worker delegates to an external MCP server.

## 11. Prompt-injection and agent-output firewall

External agents can return untrusted content containing instructions that attempt to influence the parent model.

Therefore:

```text
CHILD OUTPUT
 ↓
CANONICALIZE
 ↓
CLASSIFY DATA VS INSTRUCTION
 ↓
PROVENANCE CHECK
 ↓
SCHEMA VALIDATION
 ↓
POLICY CHECK
 ↓
EVIDENCE CHECK
 ↓
PARENT CONTEXT
```

Agent output is data until explicitly promoted to an authorized instruction or artifact.

## 12. Agent recursion firewall

```yaml
RecursionPolicy:
  max_depth:
  max_children_per_parent:
  allowed_child_types: []
  inherited_capabilities: true
  capability_expansion: deny
  max_total_cost:
  max_total_wall_time:
  recursion_timeout:
  approval_threshold:
```

The default is deny for capability expansion and unrestricted recursion.

## 13. Coding-agent integration

Coding agents plug into Project 28 rather than bypass it.

```text
CODING AGENT
 ↓
REQUIREMENTS
 ↓
PLAN
 ↓
EDIT
 ↓
BUILD
 ↓
STATIC ANALYSIS
 ↓
TEST
 ↓
FORMAL / SYMBOLIC CHECK WHERE APPLICABLE
 ↓
SBOM
 ↓
SIGN
 ↓
STAGED RELEASE
```

A successful coding-agent task is not equivalent to a trusted production release.

## 14. Research-agent integration

Research agents plug into Projects 15, 19, 29, 30 and 32:

```text
QUESTION
 ↓
SOURCE PLAN
 ↓
PARALLEL RESEARCH WORKERS
 ↓
EVIDENCE GRAPH
 ↓
COUNTEREVIDENCE
 ↓
CLAIM VERIFICATION
 ↓
SYNTHESIS
```

Search results, generated summaries and agent opinions remain distinct from verified evidence.

## 15. Computer-use integration

Browser/desktop workers plug into Projects 31, 37 and 39:

```text
SCREEN / DOM / FILE
 ↓
UNTRUSTED INPUT
 ↓
INTENT INTERPRETATION
 ↓
CAPABILITY CHECK
 ↓
ACTION PREVIEW
 ↓
EXECUTION
 ↓
RESULT OBSERVATION
 ↓
VERIFICATION
```

Persistent browser contexts require explicit grants and lifecycle management.

## 16. Workflow-agent integration

Workflow agents plug into Projects 33 and 34:

```text
BUSINESS INTENT
 ↓
WORKFLOW SPEC
 ↓
CONNECTOR DISCOVERY
 ↓
AUTHORIZATION
 ↓
ACTION GRAPH
 ↓
EXECUTION
 ↓
IDEMPOTENCY / RESULT CHECK
 ↓
AUDIT
```

Commercial automation must not become a backdoor around security policy.

## 17. AgentBay / cloud sandbox integration

Project 39 provides the concrete cloud substrate:

```text
OMNICORE DELEGATION
 ↓
AGENTBAY / CLOUD SANDBOX
 ↓
CAPABILITY-SCOPED WORK
 ↓
ARTIFACT COLLECTION
 ↓
VERIFICATION
 ↓
PERSIST APPROVED ARTIFACT
 ↓
DESTROY / RELEASE RUNTIME
```

Cloud persistence is an explicit capability rather than a default.

## 18. Edge/local agent integration

Project 37 supplies the execution continuum:

```text
T0 DETERMINISTIC
 ↓
T1 LOCAL
 ↓
T2 DESKTOP / BROWSER EDGE
 ↓
T3 MOBILE / ON-PREMISE EDGE
 ↓
T4 CLOUD GPU
 ↓
T5 SPECIALIST CLOUD AGENT
```

Agent routing can therefore move the same task between substrates while preserving the control-plane contract.

## 19. Observability

Every delegated run receives a distributed trace:

```yaml
AgentTrace:
  trace_id:
  parent_run_id:
  child_run_id:
  agent_id:
  model:
  capability:
  policy_decision:
  input_provenance:
  output_provenance:
  tool_calls:
  latency:
  tokens:
  cost:
  state_changes:
  security_events:
  artifact_ids:
  verification_status:
```

This integrates with Project 39/SLS-style telemetry and the broader OmniCore audit fabric.

## 20. Evaluation suite

### Agent quality

- task success;
- acceptance rate;
- factual/evidence accuracy;
- artifact correctness.

### Agent reliability

- recovery rate;
- timeout rate;
- false-success rate;
- checkpoint/resume success;
- deterministic replay.

### Agent security

- unauthorized capability attempts;
- prompt-injection resistance;
- credential exposure;
- persistent-state leakage;
- cross-tenant leakage;
- recursion violations;
- data-egress violations.

### Economics

- cost per successful task;
- tool calls per success;
- wall-clock latency;
- compute consumption.

### Interoperability

- manifest conformance;
- schema conformance;
- cancellation reliability;
- provenance preservation;
- artifact handoff integrity.

## 21. Failure taxonomy

```text
AGENT_SELECTION_ERROR
CAPABILITY_MISMATCH
AUTHORIZATION_FAILURE
PROMPT_INJECTION
STATE_POISONING
TOOL_FAILURE
SANDBOX_FAILURE
RECURSION_OVERFLOW
COST_BUDGET_EXCEEDED
DATA_EGRESS_VIOLATION
FALSE_SUCCESS
PROVENANCE_LOSS
ARTIFACT_VERIFICATION_FAILURE
CHECKPOINT_CORRUPTION
MODEL_FAILURE
PROVIDER_OUTAGE
```

Every failure class maps to a deterministic recovery strategy or escalation path.

## 22. Security invariants

1. External agents are never trusted merely because they are popular or vendor-operated.
2. MCP interoperability does not imply authorization.
3. Child agents cannot enlarge parent capability grants.
4. Agent output is untrusted data until validated.
5. Persistent state is a privileged capability.
6. Credentials are isolated from ordinary agent memory.
7. Agent recursion is bounded.
8. Generated artifacts require verification before promotion.
9. Provider and model choice are independent from authorization.
10. All consequential side effects pass through the Capability Broker.
11. Evidence provenance survives agent handoff.
12. Cloud/edge/local execution cannot bypass the same policy plane.

## 23. Definition of Done

- typed Agent Capability Manifest;
- agent registry;
- agent router;
- Delegation Contract;
- nested autonomy governor;
- Agent Execution Contract;
- structured handoff protocol;
- recursion firewall;
- persistent-state policy;
- MCP adapter boundary;
- prompt-injection/output firewall;
- coding-agent adapter;
- research-agent adapter;
- browser/computer-use adapter;
- workflow-agent adapter;
- local/edge adapter;
- cloud sandbox adapter;
- unified distributed tracing;
- evaluation harness;
- artifact verification and rollback.

## Strategic result

Project 40 changes the portfolio's abstraction level from **building powerful agents** to **governing an ecosystem of powerful agents**.

The target architecture is therefore:

`CHATGPT / OMNICORE → AGENT ROUTER → SPECIALIZED AGENT → CAPABILITIES → VERIFIED ARTIFACT`

with one invariant across every provider:

`MODEL != AGENT != TOOL FABRIC != EXECUTION SUBSTRATE != AUTHORIZATION`

An agent may be autonomous internally, but it is never autonomous with respect to the OmniCore trust boundary.
