# OpenAI Cookbook — Knowledge Extract

Source repository: https://github.com/openai/openai-cookbook
Snapshot reviewed: current `main` as accessed during this analysis.

## Scope

This file is a knowledge synthesis from the OpenAI Cookbook repository, focused on material relevant to building production OpenAI agents and the broader API/runtime stack. It is intentionally a synthesis, not a verbatim copy of the upstream repository.

The upstream repository is a large examples-and-guides collection for the OpenAI API, primarily Python notebooks/scripts, organized around runnable examples and long-form articles. Its repository guidance emphasizes isolated environments, environment-variable secrets, top-to-bottom notebook validation, lightweight tests, registry metadata, and review of changed material. See upstream `README.md` and `AGENTS.md`.

## Agentic architecture patterns

### Agent improvement flywheel

A strong production pattern shown in the Agents SDK examples is a closed improvement loop:

1. Run real agent workflows and capture traces.
2. Add human feedback and model-generated critique.
3. Turn recurring expectations into executable evaluations.
4. Run a validation/eval gate against current behavior.
5. Analyze traces, feedback, and eval outcomes to rank likely harness improvements.
6. Produce a developer-facing handoff for implementation, for example to Codex.

The important abstraction is the **harness**: the full contract around the model, including instructions, tools, routing, output requirements, and validation checks. The objective is to convert observations from production-like runs into repeatable tests and then into concrete harness changes.

A reviewed change loop is a sensible default: propose changes, inspect the diff, then merge/deploy. Greater automation can be added after the eval gate becomes trusted.

### Parallel fan-out / fan-in

For several independent analyses over the same input, run specialized agents concurrently and then aggregate their outputs with a downstream meta-agent. The cookbook demonstrates this with `asyncio.gather(...)` and separate specialist agents.

Use this pattern when:
- analyses are independent;
- latency matters;
- each specialist has a narrow responsibility;
- a final synthesis step can combine the results.

Typical domains include support triage, content moderation, product-review analysis, and other multi-perspective tasks.

The architectural pattern is:

`shared input -> parallel specialist agents -> labeled outputs -> meta-agent -> final answer`

### Specialist routing and ownership

The Cookbook demonstrates explicit agent specialization for workflows such as dispute resolution:
- a triage agent determines the path;
- an acceptance agent handles clear-cut cases;
- an investigator agent performs deeper evidence gathering.

The general design principle is to make decision ownership explicit and to give each agent only the tools/instructions it needs.

## Sandbox + Agents SDK architecture

A recurring architecture in the newer Cookbook examples is to keep the **trusted harness separate from compute**.

The trusted application runtime owns:
- the agent loop;
- tool registration and orchestration;
- approvals;
- secrets;
- guardrails;
- tracing;
- business-system access.

Sandbox compute is an execution surface for:
- workspace-centric tasks;
- file operations;
- shell/code execution;
- artifact generation;
- executable skills;
- isolated multi-agent work.

This separation keeps sensitive credentials and business authorization outside model-controlled compute. The sandbox receives bounded inputs and produces bounded outputs.

The Cookbook also demonstrates multiple sandboxed services for code migration workflows, with per-service isolation, validation/tests, artifacts, and audit-oriented evidence.

## Skills and workspace guidance

The repository's current guidance reinforces a clean separation:
- agent/product behavior belongs in agent instructions;
- repository/workspace conventions belong in `AGENTS.md`-style guidance;
- reusable workflows belong in Skills;
- longer reference material belongs in bounded reference/assets locations;
- executable skill logic belongs in sandbox-backed execution when required.

The examples around API skills show skills being mounted into execution environments rather than expanding the main prompt unnecessarily.

## Context engineering and long-term memory

The Cookbook contains a state-based personalization pattern using the Agents SDK `RunContextWrapper` concept.

Core model:
- **structured state** for machine-enforceable facts and preferences;
- **unstructured memory notes** for narrative, contextual preferences;
- candidate memories captured during a run;
- consolidation into long-term memory after the run;
- reinjection of relevant state at the beginning of later runs.

The pattern distinguishes:
- **global/user memory** — durable preferences that should influence future sessions;
- **session memory** — temporary context and overrides relevant only to the current interaction.

A useful precedence rule shown in the example is:

`latest user input > session overrides > global defaults`

For personalization, do not dump every internal field into model context. Put only decision-relevant data into visible context. Other trusted fields can stay application-side and be passed to tools as runtime parameters.

The source argues that state-based memory can be preferable to retrieval-based memory in workflows where the agent needs a coherent, authoritative user state with conflict resolution and explicit precedence instead of loosely related historical documents.

## Memory + compaction for long-running agents

The Cookbook includes memory/compaction examples that combine:
- sandbox filesystem state;
- Agents SDK sessions/state;
- context trimming/compaction;
- durable artifacts used across runs.

A practical context-engineering principle shown in the repository is to preserve the most useful recent task context while keeping persistent memory distinct from transient conversation history.

## Responses API patterns

The Cookbook includes dedicated examples for the Responses API, including:
- basic Responses API usage;
- tool orchestration;
- reasoning items;
- file search;
- Deep Research integration;
- MCP-backed private knowledge retrieval;
- per-run usage/spending control.

The examples reinforce the Responses API as a flexible execution surface for agentic workflows with tools, reasoning, and server-managed continuation.

### Tool orchestration

A typical Responses workflow explicitly enables tools, allows tool calls, processes returned tool outputs, and continues until the final response is produced. Parallel tool calls are useful where actions are independent.

### Reasoning

The repository includes examples specifically focused on improving reasoning-model performance through the Responses API. Reasoning items are treated as first-class response artifacts rather than assuming the response is one simple text block.

### File search / RAG

The Cookbook demonstrates the Responses API file search tool for retrieval over uploaded documents. The broader repository also contains vector-search examples using OpenAI embeddings with external vector databases.

The general RAG pipeline is:

`documents -> chunking/indexing/embeddings -> vector or hosted retrieval -> relevant context -> model`

Vector database examples cover multiple external systems, illustrating that embeddings are a reusable primitive while retrieval infrastructure can vary by provider.

### MCP and private knowledge

Cookbook Deep Research examples show that Responses/Deep Research workflows can use MCP-based tools to query private knowledge stores and internal file systems. MCP is therefore presented as an integration boundary for external/internal capabilities rather than merely a local tool format.

## Agents SDK + MCP

The Cookbook includes an example combining the Agents SDK with a Databricks MCP server for a supply-chain copilot. The pattern uses:
- `Agent` / `Runner`;
- streamable HTTP MCP connections;
- MCP tool discovery/execution;
- model settings;
- tracing around the workflow.

This reinforces the architecture of keeping domain/business systems behind typed tools/MCP boundaries while the agent handles planning and orchestration.

## Tool design lessons from real examples

Business actions should be represented as focused functions/tools with explicit parameters and return data suitable for downstream reasoning.

The dispute-management example illustrates tools for:
- retrieving orders;
- retrieving communication records;
- retrieving payment information;
- performing a final side-effecting action (closing a dispute).

The workflow is intentionally decomposed into evidence gathering, decision making, and action. This separation makes it easier to apply approvals or stricter policy to the final side-effecting operation.

Tool exposure and authorization are distinct concepts in the Cookbook's migration examples: exposing a tool does not automatically imply that every execution should be authorized. Availability, approval, and policy should be treated as separate controls.

## Evaluation and observability

The Cookbook strongly emphasizes tracing plus evaluation as a production discipline.

### Online/offline evaluation

Evaluation serves at least these purposes:
- detect failed or suboptimal tasks;
- measure accuracy/reliability;
- monitor latency/cost behavior;
- identify safety and consistency problems;
- turn qualitative feedback into repeatable regression tests;
- support continuous improvement.

The repository contains examples using OpenAI evaluation facilities and third-party observability/evaluation tooling such as Langfuse.

### Agent traces

Trace data should expose enough detail to understand:
- which agent ran;
- which tools were called;
- handoffs;
- model calls;
- latency and usage/cost signals where available;
- guardrail/validation activity.

The Cookbook's evaluation notebooks use these traces as the evidence source for grading and improvement.

### Trace-driven engineering

The practical workflow is:

`run -> trace -> inspect -> grade -> convert findings to evals -> change harness -> rerun`

This is more robust than tuning prompts from isolated anecdotes.

## Reliability and retries

The Cookbook examples reinforce explicit retry and cost controls for agentic systems.

For workflows capable of several model calls per task, per-run budgets can be enforced in application code rather than relying only on project-wide spend limits. The goal is to bound the cost of a single task and stop runaway loops.

Retry policy should distinguish:
- transient transport failures;
- provider retry advice;
- HTTP status conditions;
- requests that are safe to replay;
- stateful or side-effecting operations where replay could duplicate work.

A failed network request is not automatically safe to retry when the provider may already have accepted the request.

## Security and secrets

The Cookbook's repository-level rules and examples reinforce:
- keep API keys in environment variables;
- never hard-code credentials in notebooks or source;
- use isolated environments;
- mock/gate external-service examples where appropriate;
- treat external tool access as a security boundary;
- separate privileged operations from model-controlled input.

In sandbox-oriented architectures, keep credentials in the trusted host/application whenever possible. When model-controlled code needs access to external systems, prefer a controlled gateway/tool boundary instead of giving the model ambient credentials.

## Production engineering patterns

The repository guidelines and examples suggest these operational practices:

- one focused responsibility per agent;
- typed tool inputs and outputs;
- explicit model/provider selection where behavior matters;
- traces enabled and inspectable in development/production as policy allows;
- repeatable eval suites before automating deployment changes;
- notebooks/scripts that can run from a clean environment;
- environment-based configuration instead of embedded secrets;
- bounded, reviewable artifacts for long-running workflows;
- small, composable examples instead of monolithic agent implementations.

## Repository organization lessons

The upstream Cookbook organizes content around runnable examples and articles. Its current `AGENTS.md` recommends:
- `examples/<topic>/` for notebooks/scripts;
- `articles/` for long-form guides;
- `images/` for diagrams/screenshots;
- registry metadata for publishing;
- small requirement sets per sample;
- validation of notebooks before changes are accepted.

For this project, the relevant lesson is to keep knowledge and implementation modular so individual areas can be updated without destabilizing the whole repository.

## Current cookbook areas identified as particularly relevant

The current repository contains dedicated examples/areas for:
- `examples/agents_sdk/`
- `examples/mcp/`
- `examples/evaluation/`
- `examples/responses_api/`
- `examples/deep_research_api/`
- vector database / embeddings integrations
- API safety and production guidance
- skills in API/sandbox contexts
- Codex + Agents SDK workflows

Representative current examples include agent improvement loops, context personalization, memory/compaction, parallel agents, dispute agents, sandboxed code migration, security scanners with Agents SDK, Responses API orchestration, file search, Deep Research + MCP, and Databricks MCP integration.

## Source handling note

The OpenAI Cookbook is a large, actively maintained repository. This extraction focuses on the agent-building, orchestration, sandbox, MCP, memory, evaluation, reliability, security, and Responses API material that is most relevant to the current project. It does not claim exhaustive semantic coverage of every notebook, article, integration, or historical example in the repository.
