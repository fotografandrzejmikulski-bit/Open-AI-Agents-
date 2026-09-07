# OpenAI Agents Knowledge Base

This directory is the durable project archive for documentation supplied during the research/ingestion phase.

## Current status

The repository is intentionally documentation-first. Implementation and architecture synthesis begin only after the user explicitly confirms that the documentation corpus is complete.

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

## Source principle

The supplied documentation is treated as the primary source of truth for this project. During later synthesis, exact details should be verified against the archived source materials rather than guessed from memory.

## Phase rule

Do not begin implementation, final architecture synthesis, deployment design, or broad recommendations until the user explicitly indicates that all required documentation has been provided.
