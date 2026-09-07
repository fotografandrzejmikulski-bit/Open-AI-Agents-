# OpenAI Organization Repository Knowledge Map

> Status: active knowledge extraction. This document consolidates high-value engineering patterns extracted from selected public OpenAI repositories. It is intentionally focused on reusable knowledge for building AI agents, MCP integrations, coding agents, RAG systems, realtime/voice agents, safety layers, evaluations, and production harnesses.

## Scope and method

The OpenAI organization exposes a large public repository portfolio spanning current products, SDKs, examples, evaluation suites, research code, and archived projects. The GitHub connector available to this workspace returned a large public-repository inventory, but its search surface does not establish that every repository shown on the organization page was exhaustively fetched. Therefore this document is **not** a claim of line-by-line analysis of all ~270 repositories.

Priority was given to repositories with high leverage for agent architecture and production engineering. Sources were read from repository READMEs and, where useful, targeted specification/engineering files.

## 1. Core architecture: Agent + Tools + Guardrails + State + Observability

### OpenAI Agents SDKs

`openai/openai-agents-python` and `openai/openai-agents-js` define a common agent architecture:

- an **Agent** owns instructions, tools, guardrails and routing/handoff behavior;
- **Tools** connect the agent to functions, MCP servers, or hosted capabilities;
- **Agents as tools** retain control with a manager agent while delegating a bounded subtask;
- **Handoffs** transfer ownership of the user interaction to a specialist;
- **Sessions** manage conversation history across runs;
- **Tracing** makes agent executions inspectable and debuggable;
- **Human-in-the-loop** introduces explicit human intervention into execution;
- **Sandbox Agents** provide a filesystem/command workspace for longer tasks;
- **Realtime Agents** extend the same agent concepts into low-latency spoken interactions;
- Python also exposes **Voice Pipelines** for speech-to-text -> agent workflow -> text-to-speech architectures.

Source: `openai/openai-agents-python/README.md`; `openai/openai-agents-js/README.md`.

**Architectural implication:** do not build a monolithic “agent prompt”. Model the system as explicit responsibilities with separate execution, tool, state, safety, and observability surfaces.

## 2. Harness engineering and coding-agent execution

### OpenAI Codex

`openai/codex` is an open-source local coding agent. Its repository documentation emphasizes a strong engineering-harness model rather than treating the model itself as the whole system.

The repository's `AGENTS.md` contains particularly reusable principles:

- keep crate/public API surfaces small;
- build model-visible context incrementally rather than rewriting history;
- impose hard bounds on injected context;
- avoid unbounded model-visible items and manually review unusually large context fragments;
- prefer integration tests for agent behavior;
- preserve compatibility across CLI, app-server, configuration, raw response events, and session-resume surfaces;
- reuse established abstractions for MCP calls instead of duplicating plumbing;
- keep modules small and separate orchestration from implementation details;
- require formatting, scoped tests, and targeted lint/fix passes as part of the engineering loop.

The README positions Codex as a local coding agent and documents CLI installation plus ChatGPT/API authentication.

Sources: `openai/codex/README.md`; `openai/codex/AGENTS.md`.

**Reusable rule:** the production unit is the **harness**, not merely the model. The harness owns context assembly, tools, sandboxing, state, approvals, tests, and observability.

## 3. Autonomous work orchestration

### OpenAI Symphony

`openai/symphony` provides a language-agnostic specification for a service that continuously turns project-tracker work into isolated coding-agent runs.

Core pattern:

1. read repository-owned `WORKFLOW.md`;
2. parse typed runtime configuration;
3. poll an issue tracker;
4. normalize issues into a stable domain model;
5. dispatch eligible issues with bounded concurrency;
6. create deterministic per-issue workspaces;
7. launch a coding-agent session;
8. stream agent events back into an authoritative orchestrator state;
9. reconcile issue state periodically;
10. retry transient failures with backoff;
11. clean terminal workspaces;
12. expose structured observability.

The specification separates six layers:

- **Policy**: repository-defined workflow instructions;
- **Configuration**: typed settings and environment indirection;
- **Coordination**: polling, eligibility, concurrency, retries, reconciliation;
- **Execution**: workspace + agent subprocess;
- **Integration**: tracker/API adapters and centralized credentials;
- **Observability**: logs and optional status surfaces.

A critical security boundary is that host-side tracker credentials need not be inherited by the coding-agent child process. The orchestrator can expose provider-native tools while keeping raw credentials outside the child environment.

The spec also defines collision-resistant workspace keys, stable issue identifiers, run-attempt metadata, retry entries, and a single authoritative runtime state.

Sources: `openai/symphony/README.md`; `openai/symphony/SPEC.md`.

**Reusable rule:** autonomous agents should run inside an explicit scheduler/state machine with deterministic work identity, per-task isolation, bounded concurrency, retries, reconciliation, and a clear credential boundary.

## 4. Plugins and Skills: capability packaging

### OpenAI Plugins

`openai/plugins` is the current curated repository for Codex plugin examples. Each plugin lives under `plugins/<name>/` and requires `.codex-plugin/plugin.json`. Companion surfaces can include:

- `skills/`
- `.app.json`
- `.mcp.json`
- plugin-level `agents/`
- `commands/`
- `hooks.json`
- `assets/`

The repository contains examples for Figma, Notion, iOS/macOS development, web apps, Expo, Netlify, Remotion and Google Slides.

The older `openai/skills` repository explicitly marks itself deprecated and redirects current users to `openai/plugins` and the current plugin/skill guides.

Sources: `openai/plugins/README.md`; `openai/skills/README.md`.

**Reusable rule:** package a capability as a composable surface. Keep reusable domain instructions in skills; use MCP for live data/authenticated actions; add UI only when visual interaction materially improves the workflow.

## 5. Secure MCP for enterprise systems

### OpenAI MCPKit

`openai/openai-mcpkit` is a blueprint for authenticated MCP servers that expose proprietary enterprise data to ChatGPT.

The reference architecture emphasizes:

- Python and TypeScript server scaffolds;
- authenticated tools;
- Deep Research-compatible `search` and `fetch` tools;
- entitlement checks at the server boundary;
- separation between resource server and authorization server;
- OIDC-compatible identity providers;
- structured logs;
- production deployment after local tunnel-based development;
- preserving existing enterprise authorization rules instead of bypassing them for AI access.

The example uses Auth0 but is designed so another OIDC-compliant identity provider can replace it.

Source: `openai/openai-mcpkit/README.md`.

**Reusable rule:** MCP is an integration boundary, not an authorization shortcut. Every customer-data or write operation must be authenticated and authorized server-side.

## 6. MCP + UI: Apps SDK integration model

### OpenAI Apps SDK examples

`openai/openai-apps-sdk-examples` demonstrates a complete MCP + rich UI architecture.

The core loop is:

1. the MCP server advertises tools with JSON Schema contracts and annotations;
2. ChatGPT chooses and calls a tool;
3. the server returns structured content the model can parse;
4. response metadata identifies UI resources;
5. the Apps SDK renders an inline widget.

Important host/runtime concepts demonstrated by the examples include:

- `toolInput`
- `toolOutput`
- `displayMode`
- `theme`
- `widgetState`
- `setWidgetState`
- `callTool`
- `requestDisplayMode`
- `openExternal`
- `sendFollowUpMessage`
- `_meta.ui.resourceUri`
- `_meta.widgetSessionId`

The repository demonstrates list, carousel, map, checkout, authenticated, shopping-cart, 3D and kitchen-sink patterns. It explicitly warns that production business state should be persisted server-side rather than trusting ephemeral widget state.

Source: `openai/openai-apps-sdk-examples/README.md`.

**Reusable rule:** separate **authoritative business state** from **ephemeral UI state**. Widgets are presentation/interaction surfaces; the server remains the authority for durable state and permissions.

## 7. RAG and knowledge retrieval

### OpenAI Knowledge Retrieval

`openai/openai-knowledge-retrieval` is a config-first RAG starter combining File Search, ChatKit and Evals.

The architecture separates:

- ingestion;
- chunking;
- vector stores;
- query transformation;
- reranking;
- response synthesis;
- evaluation;
- UI.

Supported chunking approaches include:

- recursive;
- heading-aware;
- hybrid;
- XML-aware;
- custom chunkers.

Retrieval stages include:

- query expansion;
- HyDE;
- similarity filtering;
- LLM reranking.

Synthesis can use a selected model, externalized system prompts, structured outputs, and a reasoning-effort setting.

The eval harness can synthesize evaluation questions from ingested chunks or consume curated JSONL records with citation text and ideal answers. Runs can be mirrored to OpenAI Evals.

Source: `openai/openai-knowledge-retrieval/README.md`.

**Reusable rule:** treat retrieval as a pipeline of independently tunable stages, not a single `search()` call. Retrieval quality needs its own dataset and evaluation loop.

## 8. Reliable structured outputs

### Structured Outputs samples

`openai/openai-structured-outputs-samples` demonstrates that Structured Outputs can make model responses and tool calls conform to a developer-defined JSON schema.

The samples cover:

- extraction;
- generative UI;
- multi-turn assistant workflows combining tool calls and structured outputs.

**Reusable rule:** whenever an agent crosses from probabilistic reasoning into deterministic application logic, use a schema boundary rather than parsing free-form prose.

Source: `openai/openai-structured-outputs-samples/README.md`.

## 9. Safety and compliance guardrails

### OpenAI Guardrails

`openai/openai-guardrails-python` and `openai/openai-guardrails-js` provide drop-in wrappers around OpenAI clients plus Agents SDK integration.

The repositories expose guardrails for:

- moderation;
- URL/domain filtering;
- PII detection;
- secret-key/credential detection (Python);
- hallucination detection via vector stores;
- jailbreak detection;
- prompt injection detection (Python);
- NSFW detection;
- off-topic enforcement;
- custom LLM-based checks;
- competitor/keyword checks (Python).

Both implementations include evaluation tooling based on labeled JSONL datasets. The JS implementation explicitly supports precision, recall and F1 metrics and a multi-turn evaluation mode.

Sources: `openai/openai-guardrails-python/README.md`; `openai/openai-guardrails-js/README.md`.

**Reusable rule:** safety is a runtime layer around the agent, not merely a system-prompt instruction. Guardrails should be executable, testable and measurable.

## 10. Realtime voice agent architectures

### OpenAI Realtime Agents

`openai/openai-realtime-agents` demonstrates two especially reusable multi-agent voice patterns.

### Pattern A: Chat-Supervisor

A low-latency realtime agent handles basic conversation and collection tasks, while a stronger text model acts as supervisor for difficult reasoning and tool calls.

Advantages described by the example:

- immediate spoken response;
- reuse of an existing text-agent prompt/tool set;
- incremental migration into realtime;
- lower cost when basic interactions use a smaller realtime model;
- higher intelligence on tool-heavy or difficult tasks.

### Pattern B: Sequential handoffs

The user is moved between specialized realtime agents. Each specialist receives only the instructions and tools required for its domain. This avoids a single agent accumulating excessively long instructions and tool lists.

The customer-service example further shows:

- explicit agent graphs;
- authentication as a separate specialist;
- high-stakes escalation to a stronger reasoning model;
- state-machine prompting for precise identity-data collection;
- output guardrails checked before assistant text is surfaced to the UI.

Source: `openai/openai-realtime-agents/README.md`.

**Reusable rule:** voice systems often benefit from a fast conversational front layer plus specialist backends. Do not force one realtime agent to own every tool, policy and domain.

## 11. Browser computer-use testing

### OpenAI Testing Agent Demo

`openai/openai-testing-agent-demo` shows how a computer-use model can drive Playwright to execute browser test cases against a web application.

Architecture:

- frontend for test configuration and live observation;
- CUA server communicating with the model and controlling Playwright;
- sample web application under test.

The repository explicitly treats computer use as preview technology and recommends test environments rather than authenticated/high-stakes production environments.

Source: `openai/openai-testing-agent-demo/README.md`.

**Reusable rule:** computer-use agents belong inside a test/sandbox boundary by default. Treat UI actions as high-side-effect tool calls and keep production credentials out of the agent runtime unless the security model explicitly permits them.

## 12. Responses API migration lessons

### Completions -> Responses Migration Pack

`openai/completions-responses-migration-pack` is a Codex-driven migration toolkit that detects legacy API usage, proposes or applies changes, updates request/response shapes, runs tests/lints and can open a PR.

The documented migration includes:

- `/v1/completions` -> `/v1/responses`;
- `prompt` -> `input`;
- `max_tokens` -> `max_output_tokens`;
- modern OpenAI client initialization;
- tool/function schema migration;
- streaming preservation;
- multi-turn state migration.

The pack highlights Responses features useful for agents:

- stateful conversations via `store` and `previous_response_id`;
- encrypted reasoning items;
- built-in web/file/custom tools;
- flexible item-array inputs;
- semantic event streams instead of mutating one text field.

It also demonstrates a conservative retention posture by using `store:false` and client-managed context within the migration pack.

Source: `openai/completions-responses-migration-pack/README.md`.

**Reusable rule:** when migrating agent runtimes, preserve the **semantic event/state model**, not just the textual answer. Tool calls, reasoning state, streaming events and multi-turn context all form part of the execution contract.

## 13. Model behavior and instruction authority

### OpenAI Model Spec

`openai/model_spec` publishes the source of the Model Spec and its historical releases. The current source describes a **chain of command** for instruction priority:

1. Root
2. System
3. Developer
4. User
5. Guideline

It also identifies three broad risk classes:

- misaligned goals;
- execution errors;
- harmful instructions.

The spec emphasizes clarifying questions when goals are ambiguous, controlling side effects, expressing uncertainty, staying within bounds, and taking extra care with irreversible actions.

It defines tools as programs called by the assistant and explicitly notes that some tool calls can produce difficult-to-reverse side effects.

Sources: `openai/model_spec/README.md`; `openai/model_spec/model_spec.md`.

**Reusable rule:** an agent's instruction architecture should explicitly encode authority and conflict handling. Tool use should be treated as action, not as mere text generation.

## 14. Evaluation as a lifecycle, not a final test

### OpenAI Evals / Frontier Evals / Simple Evals

The OpenAI repositories collectively show several levels of evaluation:

- `openai/evals`: general evaluation framework and reusable eval construction patterns;
- `openai/simple-evals`: lightweight reference implementations for benchmark-style evaluation;
- `openai/frontier-evals`: isolated end-to-end evaluation projects for difficult capabilities such as paper replication and software engineering;
- `openai/model_spec_evals`, `openai/monitorability-evals`, and guardrail evaluation projects extend this philosophy into policy/monitorability/safety-specific measurement.

`frontier-evals` keeps each eval as an isolated reproducible project with its own README, lockfile, environment and orchestration code.

`simple-evals` emphasizes simple zero-shot evaluation settings and warns that benchmark scores are prompt-sensitive.

**Reusable rule:** maintain separate evaluation layers:

- unit/integration tests for deterministic code;
- golden datasets for agent behavior;
- domain evals for task quality;
- safety/guardrail evals;
- end-to-end benchmark suites;
- trace-level operational metrics such as latency, cost and failure rates.

Sources: `openai/frontier-evals/README.md`; `openai/simple-evals/README.md`; earlier extracted material from `openai/evals`.

## 15. Cross-repository architectural synthesis

Across the current high-value repositories, the same system shape appears repeatedly:

```text
                         ┌──────────────────────┐
                         │   User / Work Item    │
                         └──────────┬───────────┘
                                    │
                         ┌──────────▼───────────┐
                         │   Policy / Prompt     │
                         │  Model Spec / Skills  │
                         └──────────┬───────────┘
                                    │
                    ┌───────────────▼────────────────┐
                    │         Agent Runtime           │
                    │ Agent / Runner / Orchestrator  │
                    └───┬─────────────┬─────────────┘
                        │             │
              ┌─────────▼──────┐   ┌──▼────────────────┐
              │ State / Memory │   │ Tools / MCP / UI  │
              └────────┬───────┘   └──┬────────────────┘
                       │              │
                ┌──────▼──────────────▼──────┐
                │ Authorization / Guardrails  │
                └──────────────┬──────────────┘
                               │
                   ┌───────────▼───────────┐
                   │ Sandbox / Side Effects │
                   └───────────┬───────────┘
                               │
                    ┌──────────▼─────────┐
                    │ Observability /    │
                    │ Evals / Evidence   │
                    └────────────────────┘
```

This is the durable architecture to preserve when adding new capabilities.

## 16. Practical architectural rules extracted

### Rule 1 — Keep responsibilities separate

Agent reasoning, orchestration, tools, memory, UI, authorization, and evaluation should have explicit boundaries.

### Rule 2 — Make side effects explicit

Reads and writes are different tool classes. Writes should have authorization, validation and, when appropriate, explicit approval.

### Rule 3 — Keep credentials outside the model context

Use server-side authorization and host-side secret references. Never expose raw credentials to prompts, widget state, logs, or child processes unnecessarily.

### Rule 4 — Bound context

Every model-visible state fragment should have a hard size limit and a reason for being included. Avoid unbounded transcript growth and avoid injecting irrelevant internal state.

### Rule 5 — Prefer typed state transitions

Use schemas for tool inputs/outputs, normalized work items, runtime state and durable records. Do not make downstream application logic parse prose.

### Rule 6 — Specialize agents when tool/policy surfaces diverge

Use agents-as-tools when the manager should retain control. Use handoffs when a specialist should own the next interaction. Split agents when instructions, tools, policies or required model capability become materially different.

### Rule 7 — Use sandboxing for high-side-effect work

Coding, file modification, shell execution and browser automation should execute in an explicit sandbox/workspace boundary.

### Rule 8 — Treat evaluation as part of the architecture

Every substantial agent feature should ship with a behavioral dataset, expected outcomes, regression tests and operational metrics.

### Rule 9 — Build observability into the execution model

Capture enough structured event state to reconstruct what happened without storing unnecessary secrets or sensitive content.

### Rule 10 — Version the policy

Repository-owned workflow files, plugin manifests, skill packages and configuration should be version controlled and reviewable like source code.

## 17. Repository priority map for continued extraction

### Tier A — Directly reusable for agent construction

- `openai/codex`
- `openai/openai-agents-python`
- `openai/openai-agents-js`
- `openai/symphony`
- `openai/plugins`
- `openai/openai-mcpkit`
- `openai/openai-apps-sdk-examples`
- `openai/openai-knowledge-retrieval`
- `openai/openai-guardrails-python`
- `openai/openai-guardrails-js`
- `openai/openai-realtime-agents`
- `openai/openai-structured-outputs-samples`
- `openai/completions-responses-migration-pack`
- `openai/model_spec`

### Tier B — Evaluation, testing and production quality

- `openai/evals`
- `openai/frontier-evals`
- `openai/simple-evals`
- `openai/monitorability-evals`
- `openai/model_spec_evals`
- `openai/openai-testing-agent-demo`
- `openai/codex-security`
- `openai/gpt-oss-safeguard`
- `openai/privacy-filter`
- `openai/human-eval`
- `openai/mle-bench`
- `openai/SWELancer-Benchmark`

### Tier C — SDK, deployment and product integration

- `openai/openai-python`
- `openai/openai-node`
- `openai/openai-go`
- `openai/openai-java`
- `openai/openai-dotnet`
- `openai/openai-ruby`
- `openai/openai-openapi`
- `openai/openai-cli`
- `openai/codex-action`
- `openai/terraform-provider-openai`
- `openai/chatkit-js`
- `openai/chatkit-python`
- `openai/openai-chatkit-starter-app`
- `openai/openai-chatkit-advanced-samples`

### Tier D — Historical/research lineage

Examples include Whisper, GPT-2, CLIP, DALL-E, Jukebox, guided diffusion, Gym/Universe and older RL/research repositories. These are valuable for understanding model and evaluation lineage but should not be treated as the primary source for current agent architecture.

## 18. Sources analyzed in this extraction pass

- `openai/codex` — `README.md`, `AGENTS.md`
- `openai/openai-agents-python` — `README.md`
- `openai/openai-agents-js` — `README.md`
- `openai/symphony` — `README.md`, `SPEC.md`
- `openai/plugins` — `README.md`
- `openai/skills` — `README.md` (deprecated repository; historical context)
- `openai/openai-mcpkit` — `README.md`
- `openai/openai-apps-sdk-examples` — `README.md`
- `openai/openai-knowledge-retrieval` — `README.md`
- `openai/openai-guardrails-python` — `README.md`
- `openai/openai-guardrails-js` — `README.md`
- `openai/openai-realtime-agents` — `README.md`
- `openai/openai-structured-outputs-samples` — `README.md`
- `openai/openai-testing-agent-demo` — `README.md`
- `openai/completions-responses-migration-pack` — `README.md`
- `openai/model_spec` — `README.md`, `model_spec.md`
- `openai/frontier-evals` — `README.md`
- `openai/simple-evals` — `README.md`

Earlier knowledge already archived separately covers `openai/evals`, `openai/openai-python`, `openai/openai-node`, `openai/tiktoken`, and `openai/whisper` in `docs/knowledge-base/openai-repositories-whisper-evals-sdk-tokenizer.md`.
