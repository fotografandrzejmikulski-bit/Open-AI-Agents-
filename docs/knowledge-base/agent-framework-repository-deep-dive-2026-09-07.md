# Agent Framework Repository Deep Dive — 2026-09-07

> Scope: repository-level extraction from the user-supplied agent, MCP, orchestration, visual workflow, and application-building projects.
> Method: prioritize first-party repository evidence and extract reusable architecture rather than reproducing vendor marketing.
> Evidence rule: exact current-state claims are limited to repositories actually inspected. Where a supplied repository could not be fetched, that limitation is recorded instead of being silently filled from general knowledge.

## 1. Executive synthesis

The inspected ecosystem is converging on a common architecture, but different projects optimize different layers.

```text
PRODUCT / UI
      |
APPLICATION API / DOMAIN SERVICES
      |
+-----+--------------------+
|                          |
v                          v
AGENT RUNTIME          WORKFLOW RUNTIME
|                          |
+-----------+--------------+
            |
            v
       TOOLS / MCP
            |
   +--------+---------+
   |        |         |
   v        v         v
  APIs     DATA     SANDBOX
            |
            v
     STATE / MEMORY
            |
   +--------+---------+
   |                  |
   v                  v
OBSERVABILITY       EVALS
```

The strongest repositories make one or more of these boundaries explicit:

- MCP defines interoperability and capability exchange, not agent reasoning.
- LangGraph makes stateful, long-running execution durable through graph state and checkpointing.
- CrewAI separates autonomous collaboration (`Crews`) from deterministic/event-driven control (`Flows`).
- OpenAI Agents SDK combines agents, tools, MCP, guardrails, HITL, sessions, tracing and sandbox/realtime runtimes.
- AutoGen demonstrates layered event-driven and task-driven multi-agent APIs, but its repository now explicitly marks the project as maintenance mode and directs new users to Microsoft Agent Framework.
- Dify and ToolJet demonstrate visual application/workflow builders becoming programmable platforms instead of isolated canvases.
- Bolt.new demonstrates an agent controlling an entire browser-native development environment rather than merely generating text.
- Semantic Kernel's repository explicitly points forward to Microsoft Agent Framework as its successor.

The central architectural conclusion is:

> **A production agent is not a prompt. It is a versioned runtime configuration spanning instructions, model, tools, state, policy, execution environment, observability, evaluation and recovery.**

## 2. MCP: interoperability boundary, not an agent framework

The current MCP repository defines the specification, protocol schema and official documentation. The current architecture documentation states that MCP focuses on context exchange and does not prescribe how an AI application uses LLMs or manages supplied context. fileciteturn176file0 fileciteturn186file0

### 2.1 Host/client/server topology

MCP uses a host-client-server model:

```text
AI application / Host
      |
  +---+----------------+
  |   |                |
 Client A          Client B
  |                  |
Server A           Server B
```

A host creates a distinct MCP client per server. Local servers commonly use stdio; remote servers commonly use Streamable HTTP. The protocol therefore separates **AI application ownership** from **capability-provider ownership**. fileciteturn186file0

### 2.2 Two protocol layers

MCP separates:

1. **Data layer** — JSON-RPC semantics, discovery, tools, resources, prompts and notifications.
2. **Transport layer** — connection establishment, framing and authorization over stdio or Streamable HTTP.

This is directly reusable as an architectural rule: business tools should not encode assumptions about the transport, and transport/auth should not become business logic. fileciteturn186file0

### 2.3 Core primitives

The server exposes:

- **Tools** — executable actions.
- **Resources** — contextual data.
- **Prompts** — reusable interaction templates.

Discovery uses `*/list`; execution uses `tools/call`; resources use retrieval semantics; optional extensions may add durable handling for long-running operations. fileciteturn186file0

This implies a particularly strong separation for our architecture:

```text
Knowledge      -> Resources
Capability     -> Tools
Interaction    -> Prompts
```

Do not collapse all three into a single arbitrary tool returning mixed semantics.

### 2.4 Statelessness and discovery

The current architecture documentation describes MCP as stateless at the protocol layer: requests carry protocol and capability metadata rather than relying on hidden history, while `server/discover` can advertise server identity, supported protocol versions and capabilities. fileciteturn186file0

Design consequence:

> Durable business state belongs in the application/service layer, not in an assumption that an MCP connection remembers everything.

### 2.5 Notifications and dynamic capability catalogs

The architecture documentation describes opt-in subscriptions for changes such as tool-list updates. This means capability catalogs can be dynamic rather than immutable at process startup. fileciteturn186file0

That combines naturally with the existing project knowledge around Tool Search and dynamic tool loading:

```text
Discover
  -> cache metadata
  -> load only relevant capabilities
  -> refresh on change
```

### 2.6 MCP security boundary

A tool should be treated as an explicit capability boundary. Discovery is not authorization; visibility of a capability does not imply permission to execute it. The runtime should re-check identity, scope, resource ownership and side-effect policy on every consequential call.

## 3. LangGraph: durable state machine for long-running agents

The current LangGraph repository describes itself as a low-level orchestration framework for stateful agents and explicitly lists durable execution, human-in-the-loop, comprehensive memory, debugging/observability and production deployment as first-class concerns. It also positions Deep Agents as a higher-level layer built on LangGraph for planning, subagents and filesystem-heavy tasks. fileciteturn177file0

### 3.1 Architectural role

LangGraph should be treated as a **workflow/state runtime**, not merely a prompt wrapper.

```text
State
  |
  +--> node
  +--> transition
  +--> checkpoint
  +--> interrupt / resume
  +--> next node
```

The project's earlier source extraction confirms persistence through checkpointed graph state, interrupts that pause and resume execution, pending writes for recovery, and per-thread accumulation.

### 3.2 Durable execution

The fundamental LangGraph lesson is that long-running agentic work needs a durable execution substrate. Checkpointing converts an otherwise ephemeral chain of model calls into a recoverable state machine.

For our canonical architecture:

```text
RunState
  |
  +--> durable checkpoint
  +--> current node
  +--> tool outputs
  +--> pending human input
  +--> resume
```

### 3.3 Human-in-the-loop as a state transition

LangGraph's interrupt model reinforces the requirement that human approval should be represented as execution state, not just as a UI popup.

Canonical pattern:

```text
PLAN
  |
  v
PROPOSE
  |
  v
INTERRUPT / APPROVAL
  |
  +---- reject -> RECOVER / END
  |
  +---- approve -> EXECUTE
```

### 3.4 Memory model

Long-running agent systems require at least two distinct classes of state:

- working/thread state;
- persistent memory across sessions.

Do not use conversation text as the sole database.

## 4. CrewAI: autonomy versus control

The current CrewAI repository explicitly separates **Crews** from **Flows**. Crews are role-based autonomous multi-agent collaboration; Flows are event-driven workflows with fine-grained execution control, state management and branching. The README also describes a commercial control plane for deployment, tracing, governance and security. fileciteturn178file0

### 4.1 Core abstraction

```text
FLOW = control
CREW = autonomy
```

This is one of the strongest cross-framework architectural lessons in the entire corpus.

When the path is predictable, use a deterministic workflow. When delegation or strategy selection is genuinely uncertain, introduce agent autonomy.

### 4.2 State and typed project artifacts

The repository's JSON-first project scaffold separates agent configuration, crew configuration, knowledge, skills, tools and runtime environment. fileciteturn178file0

That suggests a desirable project representation:

```text
agents/
  *.jsonc
crew/workflow definition
knowledge/
skills/
tools/
.env / environment configuration
```

This makes agent configuration versionable and inspectable rather than embedding it in opaque UI state.

### 4.3 Official Skills as an agent-development substrate

CrewAI's repository now explicitly describes official Skills that teach coding agents how to scaffold, design agents/tasks and consult current docs through MCP. fileciteturn178file0

This validates the project-wide principle:

> **Skills teach the method; tools/MCP supply the capability.**

## 5. OpenAI Agents SDK: reference runtime architecture

The current OpenAI Agents SDK README defines a lightweight framework for multi-agent workflows and lists agents, sandbox agents, realtime/voice agents, agents-as-tools/handoffs, tools including MCP, guardrails, HITL, sessions and tracing as core concepts. fileciteturn180file0

### 5.1 Agent primitive

An agent is configured with instructions, tools, guardrails and handoff behavior. This is the correct abstraction boundary for application-level agent behavior.

### 5.2 Sandbox Agent

The README explicitly positions `SandboxAgent` for tasks that inspect files, run commands, apply patches and preserve workspace state over longer horizons. fileciteturn180file0

This yields a clean split:

```text
Agent reasoning
      |
      v
Sandbox execution boundary
      |
      +--> filesystem
      +--> shell
      +--> patches
      +--> repository
```

The sandbox is not merely a convenience feature; it is an execution boundary.

### 5.3 Multi-agent composition

Two complementary patterns are exposed:

- **Agents as tools** — manager keeps final-answer ownership and calls specialist agents as capabilities.
- **Handoffs** — ownership of the user-facing run transfers to another agent.

Architecture should choose deliberately based on who owns the conversation contract.

### 5.4 Sessions and continuity

Sessions make conversation history management explicit instead of requiring each application turn to reconstruct all context manually. This aligns with the broader separation between durable application state and transient LLM context. fileciteturn180file0

### 5.5 Voice and realtime

Realtime and voice are represented as distinct runtime modes. The SDK therefore treats transport/media concerns as a separate agent execution surface rather than pretending text and voice have identical operational semantics. fileciteturn180file0

### 5.6 Tracing and safety

Tracing, guardrails and HITL are core SDK concepts, not afterthought integrations. This supports the rule that production agent architecture should include evaluation/observability before deployment rather than adding them after incidents.

## 6. AutoGen: useful architecture, strategic migration signal

The current AutoGen README is especially important because it now explicitly labels the project **maintenance mode**, recommends Microsoft Agent Framework for new projects and identifies Microsoft Agent Framework as the production-ready successor. fileciteturn179file0

### 6.1 Layered architecture

AutoGen separates:

- Core API — message passing, event-driven agents, runtime;
- AgentChat API — higher-level task-oriented multi-agent interactions;
- Extensions API — model/tool/code-execution extensions;
- AutoGen Studio — visual prototyping;
- AutoGen Bench — evaluation/benchmarking.

This is a strong example of layering abstraction levels instead of forcing one API to serve every engineering use case. fileciteturn179file0

### 6.2 MCP integration

The README includes a Playwright MCP example and explicitly warns to connect only to trusted MCP servers because they may execute local commands or expose sensitive information. fileciteturn179file0

The reusable security conclusion is straightforward:

> MCP is an execution boundary when tools are executable; trust assessment must happen before connection, not after the first tool call.

### 6.3 AutoGen Studio boundary

The repository explicitly says AutoGen Studio is for rapid prototyping and is not production-ready without the developer implementing authentication, security and other application features. fileciteturn179file0

This is a valuable warning for every visual agent builder: **prototype capability does not equal production security posture**.

### 6.4 Strategic consequence

For new Microsoft-oriented systems, archive AutoGen as historical architecture and migration knowledge, while treating Microsoft Agent Framework as the successor line.

## 7. Dify: visual LLM application platform

The current Dify repository describes itself as an open-source LLM application development platform combining visual AI workflows, RAG, agent capabilities, model management, observability and APIs/BaaS. It explicitly supports cloud and self-hosted deployment. fileciteturn181file0

### 7.1 Architecture

Dify converges several layers in one product:

```text
Prompt IDE
Workflow canvas
RAG pipeline
Agent tools
Model providers
Observability
API surface
Deployment
```

This makes Dify useful as a product-development environment, while the internal architecture should preserve the same boundaries separately.

### 7.2 Agent model

The README describes agent definitions around function-calling or ReAct patterns and built-in/custom tools. fileciteturn181file0

### 7.3 RAG + LLMOps

The combination of document ingestion/retrieval with production logging and annotation-driven improvement is especially important. A production knowledge system should include:

```text
Documents
 -> ingestion
 -> indexing
 -> retrieval
 -> answer
 -> logs/evaluation
 -> improvement
```

### 7.4 Self-hosting

Dify's Docker-based self-host route makes it useful as a reference for packaging complex AI application stacks as reproducible infrastructure. fileciteturn181file0

## 8. Flowise: visual composition, now archived

The current Flowise README states that the project has been archived and points users to a future-of-Flowise discussion. It still documents a visual AI-agent builder, a monorepo with server/UI/components/API documentation, and self-host/deployment routes. fileciteturn182file0

### 8.1 Architectural value

Even as historical architecture, Flowise demonstrates a clean visual-system separation:

```text
UI canvas
  |
server API
  |
component/node integrations
  |
external models/tools
```

### 8.2 Strategic status

Treat Flowise as **archived reference architecture**, not as a preferred foundation for a new production build, unless a specific compatibility requirement dictates otherwise.

## 9. ToolJet: builder + MCP-addressable business application

The current ToolJet README is particularly relevant to our repository because it explicitly states that its coding-agent integration uses MCP so external agents can build pages, queries and components against ToolJet's real component/data contracts. It also separates ToolJet AI from ToolJet MCP and advertises self-hosting, RBAC, environments, GitSync/CI/CD, audit logs and enterprise controls. fileciteturn185file0

### 9.1 Strong architectural pattern

```text
External coding agent
        |
        v
     ToolJet MCP
        |
        v
ToolJet governed contracts
        |
   +----+----+
   |         |
  UI       Data
   |         |
 Workflows / Actions
```

The key lesson is that an agent should build against **typed, governed platform contracts**, not infer internal implementation details.

### 9.2 MCP is not just an integration add-on

ToolJet illustrates a stronger pattern: MCP can make a product itself **agent-addressable**.

This should influence our own system design. Expose durable, semantic capabilities over MCP rather than exposing internal database primitives.

### 9.3 Environment and governance

ToolJet's explicit dev/stage/prod model, GitSync, access controls and audit logs demonstrate the operational layer needed once an AI-generated application becomes a real business system. fileciteturn185file0

## 10. Semantic Kernel: successor signal matters as much as the framework

The current Semantic Kernel README begins with an explicit migration notice: Semantic Kernel is now Microsoft Agent Framework, which is described as the enterprise-ready successor with stable APIs, long-term support, multi-provider models and A2A/MCP interoperability. fileciteturn183file0

### 10.1 Architectural value retained from Semantic Kernel

Semantic Kernel emphasizes:

- model-agnostic SDK integration;
- agents and multi-agent systems;
- plugins/functions;
- MCP;
- structured outputs;
- vector databases;
- multimodal inputs;
- local deployment;
- structured process/workflow modeling;
- observability/security.

It therefore remains valuable as an architectural reference even while Microsoft is steering new development toward Agent Framework. fileciteturn183file0

### 10.2 Plugin contract lesson

The Python example shows functions exposed as typed kernel functions with descriptions and then consumed by an agent with structured response formats. fileciteturn183file0

This is another confirmation of the principle:

> Model output is probabilistic; the tool/function interface should be deterministic and typed.

## 11. Bolt.new: agent-controlled browser-native development

Bolt.new's repository defines itself as an AI-powered web-development agent capable of prompting, running, editing and deploying full-stack applications directly in the browser. Its implementation combines AI models with StackBlitz WebContainers and gives the AI control over filesystem, Node server, package manager, terminal and browser console. fileciteturn184file0

### 11.1 Execution-plane insight

Bolt makes the development environment part of the agent's tool surface:

```text
Agent
 |
 +--> filesystem
 +--> package manager
 +--> terminal
 +--> server
 +--> browser console
 +--> deployment
```

That is a materially different architecture from a text-only code generator.

### 11.2 Sandbox lesson

Once an agent can install packages and run arbitrary application code, **sandboxing becomes a first-class security requirement**. Development credentials, production secrets and unrestricted host access must not be conflated.

### 11.3 Prompt design lesson

The repository itself recommends specifying stack constraints and scaffolding basics before advanced features. This reflects a broader reliability rule: reduce the solution space before asking the agent to solve higher-order problems. fileciteturn184file0

## 12. SuperAGI: repository availability limitation

The supplied `TransformerOptimus/SuperAGI` repository could not be fetched from the connected GitHub source at the current path; the connector returned a 404 for `README.md`. Therefore no new repository-specific claims are added here beyond knowledge already archived elsewhere in this project.

This is intentional. The repository archive must distinguish **verified current source** from prior knowledge and inference.

## 13. Cross-repository architecture matrix

| System | Primary layer | Strongest contribution | Main caution |
|---|---|---|---|
| MCP | Interoperability | Standardized tools/resources/prompts + discovery | Not an agent runtime |
| LangGraph | Orchestration/runtime | Durable stateful execution | Requires explicit application/security layers |
| CrewAI | Multi-agent orchestration | Autonomy + deterministic Flow separation | Multi-agent is not automatically better |
| OpenAI Agents SDK | Agent runtime | Tools/MCP, guardrails, HITL, sessions, tracing, sandbox | Still requires application-specific domain state/auth |
| AutoGen | Multi-agent framework | Layered event-driven architecture | Maintenance mode; migrate new work |
| Dify | LLM app platform | Workflow + RAG + agents + LLMOps + APIs | Visual convenience can hide operational boundaries |
| Flowise | Visual workflow builder | Visual composition and self-hosting | Repository archived |
| ToolJet | Internal app platform | Governed MCP-addressable business applications | MCP integration is beta per README |
| Semantic Kernel | SDK/orchestration | Plugins + structured outputs + enterprise integration | Successor is Microsoft Agent Framework |
| Bolt.new | Agentic dev environment | Browser execution + full lifecycle control | Powerful execution requires isolation |

## 14. The architecture we should carry forward

The combined source material supports this canonical design:

```text
                         USER
                          |
                          v
                 WEB / MOBILE / VOICE
                          |
                          v
                    APPLICATION API
                          |
             +------------+------------+
             |                         |
             v                         v
        AGENT RUNTIME             WORKFLOW RUNTIME
             |                         |
       +-----+------+            +-----+------+
       |            |            |            |
   model/tools   guardrails   deterministic  retries
       |            |            |            |
       +-----+------+            +-----+------+
             |                         |
             +------------+------------+
                          v
                      TOOLS / MCP
                          |
        +-----------------+------------------+
        |                 |                  |
        v                 v                  v
   DOMAIN APIS        KNOWLEDGE          SANDBOX
        |                 |                  |
        v                 v                  v
     DATABASE         VECTOR/RAG       FILESYSTEM/SHELL
        |
        +-------------------+
                            v
                    AUTHORITATIVE STATE
                            |
                  +---------+---------+
                  |                   |
                  v                   v
             OBSERVABILITY          EVALS
                  |                   |
                  +---------+---------+
                            v
                       DEPLOYMENT
                dev -> stage -> production
```

## 15. Non-negotiable engineering rules distilled from the repositories

### Rule A — Protocol, runtime and product are separate layers
MCP should not become the business domain model. The agent runtime should not become the database. The UI builder should not become the source of truth.

### Rule B — Stateful work needs durable checkpoints
For long-running work, store state and resumable execution boundaries explicitly.

### Rule C — Determinism where possible, autonomy where necessary
Use workflows for known control paths and agent reasoning for uncertain choices.

### Rule D — Tool discovery is not permission
A capability catalog answers "what exists"; authorization answers "what this caller may execute now".

### Rule E — Generated software remains software
Generated code or visual artifacts still require source control, tests, security review, dependency review and rollback.

### Rule F — Execution environments are security boundaries
Filesystem, shell, package installation, browser control and deployment need isolation and scoped credentials.

### Rule G — Human approvals must be resumable
Represent approval as a state transition with stored context and an explicit resume path.

### Rule H — State is layered
Separate UI state, run/thread state, persistent memory, domain state and infrastructure state.

### Rule I — Typed contracts reduce model uncertainty
Functions, tool schemas, structured outputs and domain APIs convert probabilistic model output into deterministic system behavior.

### Rule J — Visual builders need an escape hatch
A production platform should expose inspectable state, version history, export/source control, tests and deployment boundaries.

### Rule K — Evaluation is part of runtime engineering
Logs and traces should feed a continuous loop:

```text
test -> deploy -> trace -> evaluate -> diagnose -> improve -> redeploy
```

### Rule L — Prefer supported successor lines for new projects
The current repositories explicitly flag AutoGen and Semantic Kernel as transition points toward Microsoft Agent Framework; Flowise is archived. These status signals must influence technology selection, not merely feature comparison.

## 16. New design vocabulary added to the knowledge base

The following concepts should be treated as canonical terminology in future work on this repository:

- **Capability plane** — tools, MCP servers and domain actions exposed to agents.
- **Execution plane** — sandbox/compute where agent-directed programs actually run.
- **Control plane** — configuration, policy, approvals, deployment, governance and audit.
- **State plane** — thread/run state, persistent memory, domain state and infrastructure state.
- **Knowledge plane** — resources, RAG indexes, documents and retrieval services.
- **Agent contract** — instructions + model + tools + policy + output schema + continuation semantics.
- **Recovery boundary** — a persisted point from which a failed or interrupted run can safely resume.
- **Agent-addressable application** — a business application whose semantic operations are exposed to agents through governed APIs/MCP.
- **Autonomy envelope** — the explicit set of actions an agent may select and execute without additional human authorization.
- **Prototype-production gap** — the security/operational delta between a visual demo and a deployable business system.

## 17. Verification and source discipline

This document intentionally records exact repository observations alongside architectural synthesis. The current inspected evidence includes MCP, LangGraph, CrewAI, AutoGen, Dify, OpenAI Agents SDK, Semantic Kernel, Bolt.new and ToolJet. The SuperAGI repository fetch failed and is therefore not presented as newly verified.

The project should continue using this rule:

```text
source evidence
    -> extraction
    -> architectural synthesis
    -> implementation rule
    -> repository documentation
    -> prototype
    -> tests/evals
```

That creates a traceable chain from external knowledge to engineering decisions.
