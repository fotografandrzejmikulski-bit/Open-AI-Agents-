# OpenAI Agents Knowledge Base

This directory is the durable project archive for documentation and repository knowledge extracted for building OpenAI-based agents, MCP integrations, coding agents, RAG systems, realtime/voice agents, safety layers, and evaluation harnesses.

## Current status

The repository is documentation-first. Source-derived knowledge is archived here before it is used as implementation guidance.

## Materials currently absorbed

- OpenAI Plugins / Apps architecture: Skills, MCP servers, optional UI, packaging, testing, submission, metadata optimization, security/privacy.
- MCP server design: tools, schemas, annotations, structured results, auth, OAuth 2.1, skills import, deployment and review requirements.
- MCP Apps / ChatGPT UI bridge: shared MCP Apps standard, `window.openai` extensions, UI resources, state, file handling, CSP, rendering patterns.
- Checkout API concepts and constraints.
- OpenAI API / Responses API fundamentals, model selection, prompts/instructions, function calling and structured outputs.
- Agents SDK fundamentals: Agent definitions, tools, MCP, handoffs, agents-as-tools, sessions, running agents, results/state, guardrails and human review, tracing.
- Tool Search and Programmatic Tool Calling.
- Models/providers and transport configuration.
- TypeScript Agents SDK quickstart and configuration.
- Sandbox Agents architecture and execution model.
- Sandbox concepts: `SandboxAgent`, `Manifest`, capabilities, sandbox sessions, `RunState`, `sessionState`, snapshots, lifecycle ownership, skills/memory/compaction, filesystem/shell, mounts, permissions, path grants, credential boundaries, exposed ports and sandbox clients.
- Sandbox client options: Unix local, Docker, hosted providers, session ownership, resume/snapshot semantics, materialization limits and mount credential safety.

## Repository-derived knowledge

- `openai/codex`, `openai/symphony`, `openai/plugins`, `openai/openai-mcpkit`, `openai/openai-apps-sdk-examples` and other high-value OpenAI repositories have been mined for reusable engineering patterns.
- The consolidated repository map is in `docs/knowledge-base/openai-org-repository-knowledge.md`.
- Earlier extractions from `openai/whisper`, `openai/evals`, `openai/openai-python`, `openai/tiktoken`, and `openai/openai-node` are archived separately.

## Key architectural themes

1. Agent reasoning is only one layer: production systems also need explicit tools, state/memory, authorization, safety, sandboxing, observability and evaluation.
2. Side effects require stronger controls than read-only retrieval.
3. Context should be incremental, bounded and task-relevant.
4. Typed schemas should bridge probabilistic model output and deterministic application logic.
5. Specialize agents when instruction/tool/policy surfaces materially diverge.
6. Treat evaluations and traces as part of the runtime lifecycle, not merely release-time tests.
7. Keep authoritative business state server-side and treat UI/widget state as ephemeral.

## Source principle

The supplied documentation and repository source are treated as the primary evidence for this project. Later synthesis should verify exact details against archived source materials rather than guessing from memory. Where this knowledge base summarizes repository content, it should not be read as a claim that every file in every OpenAI repository has been exhaustively analyzed.
