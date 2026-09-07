# Cross-Platform Knowledge Extraction: OpenAI, MCP, Cloud & App Builders

> Status: active source-derived knowledge archive.
> Scope requested: `https://openai.github.io`, `https://platform.openai.com`, `https://modelcontextprotocol.io`, `https://cloud.ibm.com`, `https://cloud.activepieces.com`, `https://flutterflow.io/`, `expo.dev`, `replit.com`, `render.com`, `railway.com`, `vercel.com`, `https://developers.openai.com/`.
>
> Date: 2026-09-07.
>
> Coverage note: this is a focused engineering extraction, not a line-by-line crawl of every page. The current connector available in this session can inspect GitHub sources; therefore official repositories/docs mirrors were used where available. For Replit, IBM Cloud and some commercial product surfaces, the available public GitHub evidence was less complete, so claims are kept at the architecture level and are explicitly marked where appropriate.

## 1. OpenAI developer platform: `developers.openai.com` + `platform.openai.com`

The current OpenAI developer surface is best understood as a layered platform rather than a single API. The central model-interaction surface for modern agentic workloads is the Responses API, surrounded by conversation/state handling, streaming/WebSocket transports, structured outputs, tools, hosted capabilities, Agents SDK, realtime/audio, retrieval, MCP, Tool Search, Programmatic Tool Calling, code/shell/computer execution, webhooks and production controls.

### Core architecture

`model interaction -> state -> tools/capabilities -> safety -> orchestration -> execution -> observability/evals`

The key architectural extraction is that the model is not the complete runtime. Agent behavior is composed from explicit instructions, tools, state, routing/orchestration, guardrails, runtime execution and monitoring. The OpenAI Agents SDK follows this model directly: `Agent` plus `Runner` manages turns, tools, guardrails, handoffs and sessions, while direct Responses usage leaves more of the loop under application control. fileciteturn111file0L2-L10

### Modern agent primitives

| Primitive | Architectural role | Use when |
|---|---|---|
| Responses API | Core model interaction | Direct control over model/tool loop |
| Agents SDK | Higher-level orchestration runtime | You want agent objects, runners, tools, handoffs, guardrails and sessions |
| Tool Search | Dynamic capability loading | Tool surface is large and should be deferred |
| Programmatic Tool Calling | Model-generated deterministic tool composition | Many calls require filtering, joining, aggregation or predictable control flow |
| MCP | External capability boundary | Capabilities/data must live outside the model runtime |
| Skills | Static operational knowledge/workflow guidance | The agent must know how to perform a repeated domain task |
| Guardrails / approvals | Risk control | Inputs, outputs or side effects require validation or human review |
| Sandbox / execution | Compute boundary | Agent must run code/commands or inspect a filesystem |

OpenAI's SDK source also indicates that the documentation surface now includes Sandbox Agents as a major capability area across local, containerized and hosted environments. fileciteturn111file11L226-L234

### Production rules extracted for this knowledge base

1. Keep model-visible context incremental, bounded and task-relevant.
2. Use typed schemas at the model/application boundary.
3. Put side effects behind explicit tools and authorization, not only natural-language instructions.
4. Choose one continuation/state strategy per conversation unless there is a clear reason to combine them.
5. Separate deterministic orchestration from model-directed agent loops.
6. Treat observability and evaluation as runtime lifecycle components, not only release gates.

### Evidence from official OpenAI repositories

The Python SDK documentation explicitly distinguishes orchestration from the underlying Responses API and assigns turns, tools, guardrails, handoffs and sessions to the SDK runtime. fileciteturn111file0L2-L10 The SDK also publishes a current `llms.txt` index covering agents, running agents and core concepts for downstream retrieval. fileciteturn111file9L177-L185

---

## 2. MCP: `modelcontextprotocol.io`

MCP provides the protocol boundary between an AI host/client and external capability servers. The architectural model is:

`Host -> Client -> MCP Server -> external system`

The separation matters because the host remains responsible for permissions, consent, lifecycle and policy while the server owns domain capabilities.

### MCP primitives

| Primitive | Control owner | Typical meaning |
|---|---|---|
| Prompts | User/application | Templates and reusable instructions |
| Resources | Application/server | Contextual or reference data |
| Tools | Model/application through host policy | Executable capabilities / side effects |

The current SDK ecosystem exposes tools, resources and extensions as first-class server capabilities; for example the Python server APIs accept tool and resource registrations and support change notifications. fileciteturn112file3L69-L76 fileciteturn112file4L93-L100

### Authorization

Current MCP authorization material includes OAuth 2.1-oriented flows and protected-resource metadata. The TypeScript SDK has explicit OAuth client-credentials examples where the MCP resource identifier is treated as an exact server URL, which reinforces that authorization is resource-specific rather than a generic bearer-token passthrough. fileciteturn112file2L47-L54

The MCP project also documents client-credentials support with `client_id` and `client_secret` for simpler deployments. fileciteturn112file8L178-L185

### Important current 2026 direction

The MCP repository contains an active sessionless-MCP proposal focused on making MCP work behind load balancers and without sticky routing. This is useful architectural evidence that production MCP deployments need to minimize hidden affinity assumptions and separate protocol capability from transport/session infrastructure. fileciteturn112file6L139-L147

### Reusable rule

Design an MCP server as a capability boundary, not as a thin wrapper around a database. Keep tools narrowly scoped, make authorization server-side, return structured data, and make destructive operations distinguishable from reads.

---

## 3. IBM Cloud: `cloud.ibm.com`

### Architectural position

IBM Cloud is oriented toward enterprise governance, identity, regulated workloads, managed services and infrastructure automation. The strongest directly relevant pattern for this project is the separation between application execution, platform identity and API governance.

### Code Engine

Public IBM material consistently positions Code Engine as a managed serverless/container execution layer. A representative public reference describes it as a Kubernetes-based Containers-as-a-Service and Functions-as-a-Service offering. fileciteturn128file1L18-L26

For agent infrastructure, the important distinction is workload semantics:

| Workload | Preferred primitive |
|---|---|
| HTTP agent/API | Managed application |
| Batch or run-to-completion work | Job |
| Short function-style execution | Function |
| Queued / compute-heavy workloads | Fleet / worker-style execution |

### IBM agentic architecture pattern

IBM examples show external MCP servers being deployed to Cloud environments and then registered into agent platforms such as watsonx Orchestrate. One IBM tutorial explicitly describes deploying the MCP server and then adding its `/mcp` endpoint to watsonx Orchestrate. fileciteturn124file1L36-L58

Another IBM agentic control-plane reference distinguishes the inter-agent and tool layers: A2A for agents, MCP for tools, and standardized model APIs for models hosted in different providers. fileciteturn124file2L62-L69

### Reusable rule

Use IBM-style enterprise boundaries when the agent is expected to cross identity, governance and production infrastructure domains: model/runtime, MCP tools, cloud execution, secrets and policy should remain separable.

---

## 4. Activepieces: `cloud.activepieces.com`

Activepieces is architecturally interesting because it combines deterministic automation and agentic behavior in one system.

### Core abstractions

- **Flows**: deterministic trigger -> actions/steps.
- **Agents**: model-driven task execution using connected applications/capabilities.
- **Tables**: structured business data.
- **Pieces**: reusable application capabilities; current source describes 280+ open-source pieces and states that each piece can also function as an MCP server. fileciteturn113file0L2-L18

### Why this matters

The platform creates a practical hybrid architecture:

`Agent decides -> Flow executes deterministic sequence -> Table persists business state`

That is often stronger than asking an agent to directly execute every step.

### MCP pattern

The MCP surface is built around discovery plus capability execution. Discovery/read-only actions can inspect connected flows, connections, tables, runs and validation before mutation. The critical security rule is that credentials remain connection-layer state and are not emitted as model-visible payloads.

### MCP as deterministic integration

A notable Activepieces pattern is that an MCP client can call external MCP tools without an LLM. That means MCP is not synonymous with agentic reasoning: it can also be used as a deterministic integration protocol inside a workflow.

### Reusable rule

Use an LLM only where reasoning or selection is required. Keep known sequences deterministic and persist business state in structured data stores rather than in chat history.

---

## 5. FlutterFlow: `flutterflow.io`

FlutterFlow is a visual application-development platform centered on widget composition, Action Flow logic, custom actions/widgets, API integrations, Firebase/Supabase, design systems and Flutter code export.

### AI agent architecture

FlutterFlow's AI Agents integrate conversational and multimodal capabilities into application actions. The application invokes the configured agent with system instructions, preloaded messages and model settings; conversation continuity is maintained through a conversation identifier.

The engineering insight is that the agent is treated as an application capability, not as the entire application architecture.

### AI coding-agent pattern

FlutterFlow's current agent tooling is also instructive: AI coding agents can be given project context, local tooling can be verified/installed, an AI workspace can be initialized/reused, and the FlutterFlow MCP server can be registered for authenticated project operations. The user can review the agent's plan before project changes are applied.

### Source evidence

The public FlutterFlow documentation repository contains current guidance for configuration files, Firebase initialization and passing library values/API keys into snippets, confirming the importance of separating project-level configuration from reusable code customizations. fileciteturn114file0L1-L16

### Reusable rule

Visual composition, agent reasoning and backend execution should remain separable. AI-generated project modifications should be reviewable changes rather than invisible writes.

---

## 6. Expo: `expo.dev`

Expo has become especially relevant to agent-builder architecture because its current documentation explicitly covers AI agents, Expo Skills and the Expo MCP Server.

### Current AI tooling

Expo's docs describe an **Expo MCP Server** as companion AI tooling giving coding agents direct access to Expo and EAS services. fileciteturn129file0L1-L10

The current MCP docs also describe AI-assisted local verification, including screenshot/interaction workflows for a running app. fileciteturn129file1L23-L31

For Codex specifically, Expo documents `codex mcp login expo` as the authentication setup path for the Expo MCP integration. fileciteturn129file4L118-L128

Expo also explicitly states that Cursor and other agents do not have to rely on an official Expo plugin: Expo Skills and the Expo MCP Server can be installed separately. fileciteturn129file2L42-L50

A useful 3-layer pattern appears in the docs for `agent-device`: Expo Skills teach the agent how to implement features, Expo MCP provides current Expo/EAS context, and `agent-device` verifies the running app. fileciteturn129file7L206-L214

### EAS architecture

Expo EAS separates:

`Build -> Submit -> Update -> Workflows -> Hosting`

EAS CLI documentation states that EAS Update supports branches, channels, runtime versions, rollouts and rollbacks. fileciteturn115file12L310-L318

The standard EAS build workflow can also handle Android signing credentials. fileciteturn115file1L18-L25

### Agent-builder lesson

Expo demonstrates an unusually clean separation of concerns:

`Skills = implementation knowledge`
`MCP = live project/platform capabilities`
`device automation = verification`
`EAS = build/release/update infrastructure`

That is a canonical pattern for mobile agent systems.

---

## 7. Replit: `replit.com`

Direct official GitHub documentation was less accessible through the current connector than for Expo/Railway/Vercel, so this section is intentionally more conservative.

### Product architecture

Replit's core value proposition is compressed development-to-deployment flow:

`natural-language intent -> AI Agent -> generated full-stack project -> integrated services -> publish`

Public documentation references confirm that the platform combines app building with databases, hosting and environment/secrets management.

### Environment and secrets

The important architectural rule is to distinguish editor/development state from published runtime state and keep secrets outside source code. Public references discussing Replit's deployment model also distinguish autoscale/static deployment categories and deployment configuration in `.replit`. fileciteturn120file12L236-L244

### Reusable rule

Replit is a strong example of a "compressed platform" in which the agent can act across application code and infrastructure. For a production implementation, preserve the same separation boundaries even when the platform hides them from the user: source, secrets, database, deployment and runtime should remain explicit architectural objects.

---

## 8. Render: `render.com`

Render exposes application infrastructure through service primitives and infrastructure-as-code.

### Service primitives

The platform model includes web services, static sites, private services, background workers, cron jobs and workflow-style execution, plus managed data services.

Its current AI/coding-agent integrations are also becoming first-class: Render publishes agent skills/plugins for infrastructure work. The Render Blueprint skill specifically covers databases, private services, Key Value, projects/environments, preview environments and YAML validation, and points to separate deploy/MCP skills for runtime operations. fileciteturn123file0L1-L20

### Architectural lesson

Render treats infrastructure configuration as a typed declarative object that an agent can reason about before deployment. This is preferable to having an agent issue arbitrary shell commands against production.

### Reusable rule

Expose deployment as a structured capability:

`inspect -> plan -> validate -> approve -> deploy -> observe`

rather than:

`agent -> arbitrary production command`

---

## 9. Railway: `railway.com`

Railway is one of the strongest matches for an agent-managed infrastructure model because its documentation now explicitly covers MCP, Agent Skills and sandboxes.

### Core model

The platform is organized around:

`Project -> Environment -> Services -> Variables -> Deployments`

The official docs expose CLI commands for deploy, redeploy, restart, templates and deployment inspection. fileciteturn118file0L1-L12

### Environment isolation

A key architectural property is environment scoping. Staging and ephemeral PR environments can mirror topology without becoming the same operational environment.

### Dependency-aware deployment

Railway uses service references to infer deployment ordering: when one service depends on another, the dependent deployment waits for the referenced service to finish. fileciteturn118file4L129-L137

### Agent tooling

Railway publishes an MCP server that lets AI assistants create projects, deploy templates and manage environments. fileciteturn118file7L199-L208

Railway also documents Agent Skills as an open format for extending coding assistants with domain knowledge about deploying services, managing environments and querying metrics. fileciteturn118file8L227-L235

Its sandbox primitive provides environment-scoped isolated on-demand compute on a Railway VM primitive. fileciteturn118file11L307-L315

### Reusable rule

Railway demonstrates the desirable combination of:

`Skills -> knowledge`
`MCP -> live infrastructure capability`
`Environment -> isolation`
`Sandbox -> untrusted/ephemeral compute`
`Deploy -> explicit side effect`

---

## 10. Vercel: `vercel.com`

Vercel's current platform architecture is particularly relevant to agentic systems because its platform and AI tooling are being designed together.

### Core agent stack

The current Vercel surface combines AI SDK, AI Gateway, Sandbox, Workflows, Fluid Compute, observability and security primitives.

A useful conceptual distinction is:

**Workflow** = application-controlled durable control flow with model calls embedded.

**Agent** = model-directed iterative control flow where the model chooses subsequent actions.

### Sandbox

Vercel positions Sandbox as isolated compute for untrusted, user-generated or AI-generated code. The architectural purpose is to move arbitrary code execution away from the trusted application process.

### Fluid Compute

Fluid Compute is designed for concurrent invocation sharing and dynamic scaling, making it well suited to I/O-heavy AI services where traditional one-request-per-instance serverless execution can be inefficient.

### AI SDK / MCP

The Vercel AI SDK ecosystem directly integrates MCP tooling; current source contains `@ai-sdk/mcp` as a workspace dependency and provider-executed/deferred tool handling. fileciteturn122file1L22-L38 fileciteturn122file0L2-L18

Vercel also publishes a platform plugin for coding-agent workflows. Its current knowledge base references Vercel Functions, AI Gateway, deployment access protection, a Vercel MCP server, and an agent-builder skill. fileciteturn119file0L1-L20 fileciteturn119file1L23-L34

### Reusable rule

For long-running agent systems use a durable workflow as the reliability backbone, isolate untrusted code in a sandbox, keep model access behind a well-defined provider interface, and expose deployment through authenticated platform APIs/MCP rather than unrestricted credentials.

---

## 11. Cross-platform architectural synthesis

The strongest recurring patterns across OpenAI, MCP, IBM Cloud, Activepieces, FlutterFlow, Expo, Replit, Render, Railway and Vercel are not vendor-specific. They form a common reference architecture for production agents.

### A. Separate reasoning from execution

The model decides; deterministic services, APIs, workflows, MCP servers, sandboxes and deployment systems execute.

### B. Separate capability from knowledge

`Skills = what the agent knows how to do`

`MCP/tools = what the agent can actually access or change`

Expo makes this explicit through Skills + MCP + device verification. fileciteturn129file7L206-L214

Railway does the same through Agent Skills + MCP. fileciteturn118file8L227-L235

### C. Treat infrastructure as typed state

Projects, environments, services, deployments, domains, variables, sandboxes and databases should be represented as explicit objects. This enables plan/validate/approve/deploy workflows.

### D. Use layered state

```text
conversation state
    ↓
agent/session state
    ↓
workflow state
    ↓
application/business state
    ↓
infrastructure state
```

Each layer requires different ownership and retention semantics.

### E. Make side effects explicit

Deployment, infrastructure mutation, user-data writes, code execution, checkout and account changes should be represented as explicit capabilities with authorization and, where appropriate, approval.

### F. Isolate environments

Preview, staging, production and untrusted execution should not be treated as one shared runtime. Railway and Render make environment separation a core operational primitive; Expo does the same for build/update channels and runtime versions.

### G. Build recovery into the runtime

Retries, rollback, preview environments, resumability, staged changes, dependency-aware deployment and durable workflows all reduce the blast radius of model/runtime errors.

### H. Optimize the full system

Latency, cost, safety, observability, model quality and developer experience are coupled system properties. Better models do not eliminate the need for better runtime design.

---

## 12. Canonical architecture for this project

```text
                 USER / EVENT / WORK ITEM
                           |
                           v
              +---------------------------+
              | POLICY / INSTRUCTIONS     |
              | MODEL SPEC / SKILLS       |
              +-------------+-------------+
                            |
                            v
              +---------------------------+
              | AGENT RUNTIME              |
              | Responses / Agents SDK     |
              +---+-------------------+-----+
                  |                   |
        +---------+---------+         |
        |                   |         |
        v                   v         v
+---------------+   +--------------+  +----------------+
| STATE/MEMORY  |   | GUARDRAILS  |  | ORCHESTRATION   |
+-------+-------+   +------+-------+  | Workflows      |
        |                  |          +-------+--------+
        +---------+--------+                  |
                  v                           |
           +-------------+                    |
           | TOOLS / MCP |<-------------------+
           +------+------+ 
                  |
       +----------+----------+----------------+
       |          |          |                |
       v          v          v                v
     APIs/DB   Workflows   Sandbox        Cloud/Deploy
       |          |          |                |
       +----------+----------+----------------+
                  |
                  v
        +-----------------------+
        | OBSERVABILITY / EVALS |
        | traces / metrics / QA |
        +-----------------------+
```

### Platform mapping

| Layer | Best evidence from analyzed platforms |
|---|---|
| Model/runtime | OpenAI Responses + Agents SDK |
| Knowledge | OpenAI Skills, Expo Skills, Railway Agent Skills |
| External capability boundary | MCP |
| Deterministic automation | Activepieces Flows, Railway/Render workflows |
| Mobile execution/verification | Expo MCP + device tooling |
| Untrusted compute | Vercel Sandbox, Railway Sandboxes, OpenAI Sandbox Agents |
| Cloud/application deployment | Render, Railway, Vercel, IBM Code Engine |
| Visual app composition | FlutterFlow |
| Compressed AI app builder | Replit |
| Enterprise governance | IBM Cloud + IAM/API governance |
| Release/update | Expo EAS |
| Evaluation/observability | OpenAI traces/evals plus platform telemetry |

## 13. Decision framework extracted from the platforms

Use **OpenAI Responses/Agents SDK** when the primary problem is agent reasoning and orchestration.

Use **MCP** when the primary problem is exposing live external capabilities through a standardized boundary.

Use **Skills** when the primary problem is repeatable domain knowledge or operational method.

Use **deterministic workflows** when the execution sequence is known.

Use a **sandbox** when the agent must execute arbitrary or untrusted code.

Use **Render/Railway/Vercel/IBM** when the agent must manage actual production infrastructure; do not collapse infrastructure mutation into arbitrary shell access.

Use **Expo** when the target is React Native/mobile and the agent must understand EAS, device verification and app-release state.

Use **FlutterFlow** when the visual application layer is itself part of the development workflow.

Use **Activepieces** when business automation and agentic branching need to coexist around explicit data tables and application connections.

Use **Replit-like compressed builders** when minimizing the distance between user intent, code generation and first deployment is the priority.

## Source-quality statement

This document is an architecture-oriented synthesis of current official/public technical material available to the session. It is deliberately conservative where the connector could not directly inspect a vendor's full documentation corpus. It should be treated as a durable knowledge layer for future design decisions, while implementation details such as current API signatures, quotas, pricing and exact product limits must still be verified against the live vendor documentation at implementation time.
