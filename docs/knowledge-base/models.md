# OpenAI Agents SDK - Models

Source: `Models _ OpenAI Agents SDK.pdf` (27 pages)

## Default model and model selection
- If an `Agent` does not specify a model, the current default is `gpt-5.6-luna`, with `reasoning.effort: "none"` and `text.verbosity: "low"` for efficient, high-volume workloads.
- A process-wide fallback can be set with `OPENAI_DEFAULT_MODEL`.
- A `Runner` can define a default model; it is used when an agent does not specify one.
- GPT-5.x models receive SDK default `modelSettings` unless customized. Example: `reasoning.effort` and `text.verbosity` can be set explicitly.
- For latency/cost-sensitive workloads, start with the default Luna configuration or `reasoning.effort: "none"`, then raise reasoning effort only when needed.
- Non-GPT-5 models without custom settings use generic model settings compatible with any model.

## OpenAI provider
- `setDefaultOpenAIKey()` sets the SDK-wide API key.
- `setDefaultOpenAIClient(client)` allows a custom OpenAI client; directly supplied clients require `openai` 7.2+ according to this source.
- `OpenAIProvider` supports `apiKey`, `baseURL`, `websocketBaseURL`, `openAIClient`, `organization`, `project`, `useResponses`, `useResponsesWebSocket`, `cacheResponsesWebSocketModels`, `responsesWebSocketOptions`, and `strictFeatureValidation`.
- `baseURL` cannot be combined with `openAIClient`; `websocketBaseURL` cannot be combined with `openAIClient`; `openAIClient` cannot be combined with `apiKey`, `baseURL`, or `websocketBaseURL`.
- `useResponses` chooses Responses API vs Chat Completions for provider-resolved string model names.
- Responses WebSocket can be enabled globally or per provider. Concrete model instances retain their own transport choice.
- Cached WebSocket-backed Responses wrappers should be closed with `provider.close()` during shutdown.
- `strictFeatureValidation` can turn unsupported Responses-only features on Chat Completions into `UserError` instead of warnings/ignoring them.

## Chat Completions audio
- Audio-capable Chat Completions models accept endpoint-specific modality/audio fields through `modelSettings.providerData`.
- Normalized output can retain assistant audio content; raw provider metadata is available in provider data/raw responses as described in the source.
- For low-latency bidirectional audio, the source directs applications to the Realtime API / Voice Agents instead.

## Responses WebSocket transport
- Enable via `setOpenAIResponsesTransport('websocket')` or `OpenAIProvider({ useResponses: true, useResponsesWebSocket: true })`.
- Existing `run()` / `Runner.run()` usage continues to work; a dedicated WebSocket session helper is only needed for explicit connection lifecycle optimization.
- `withResponsesWebSocketSession(...)` is a transport lifecycle helper and is unrelated to the SDK memory `Session` interface.
- Proxy/gateway usage may require `websocketBaseURL` or `OPENAI_WEBSOCKET_BASE_URL`.
- `responsesWebSocketOptions` provides ping/pong keepalive controls.

## Deferred tool loading / tool search
- `toolSearchTool()`, `toolNamespace()`, and deferred function/MCP tools require the OpenAI Responses API.
- Chat Completions rejects namespaced/deferred function tools; the AI SDK adapter does not support deferred Responses tool-loading flows.
- Tool search requires GPT-5.6 Sol or newer Responses models supporting it.
- When deferred tools are present, add `toolSearchTool()` to the same agent and leave `modelSettings.toolChoice` as `auto`.
- The SDK does not let the application force `tool_search` or a deferred tool by name; the model decides when to load definitions.

## Hosted Multi-agent (experimental)
- `OpenAIHostedMultiAgentModel` lets GPT-5.6 models create/coordinate a tree of hosted subagents through the Responses API.
- This differs from SDK handoffs and agents-as-tools: the application does not instantiate/schedule local `Agent` objects for those hosted subagents.
- The hosted root agent delegates, the service coordinates subagents, and `/root` synthesizes the final answer.
- The experimental model uses a persistent Responses WebSocket. Keep the same model instance for the full run and close it afterward.
- Default `maxConcurrentSubagents` is currently 3 when omitted.
- Local function calls are executed by the normal SDK runner; the Responses API call ID is the routing token and must be preserved when injecting matching `function_call_output`.
- `getHostedAgentMetadata(details)` is useful for logs/authorization but must not be used as the routing key.
- Side-effecting tools should be idempotent by call ID so interrupted continuation cannot repeat the effect.
- Only the hosted `/root` message with `phase: final_answer` becomes ordinary assistant output / `finalOutput`.
- Hosted collaboration records and subagent messages remain on the active WebSocket; they are exposed through raw model streaming but are not added to normal SDK history.
- Consume streamed hosted runs through their terminal event. Stopping early abandons the hosted response; a later run starts a new one.
- Continuation state for an in-progress hosted response belongs to the `OpenAIHostedMultiAgentModel` instance. Recreating it loses continuation state.
- One hosted model instance supports one active run at a time.
- Do not combine the experimental hosted model with SDK handoffs, `reasoning.summary`, or `max_tool_calls` per the source. Stable `OpenAIResponsesModel` remains compatible with SDK handoffs and agents-as-tools.

## ModelSettings
Fields documented by the source include:
- `temperature`
- `topP`
- `frequencyPenalty`
- `presencePenalty`
- `toolChoice`
- `parallelToolCalls`
- `truncation`
- `maxTokens`
- `timeoutMs`
- `store`
- `promptCacheRetention`
- `promptCacheOptions`
- `contextManagement`
- `reasoning.effort`
- `reasoning.mode`
- `reasoning.context`
- `reasoning.summary`
- `text.verbosity`
- `providerData`
- `preserveRawUsage`
- `retry`

`reasoning.mode` and `reasoning.context` are Responses-only; `reasoning.effort` remains available on supported Chat Completions models.

## Model settings precedence and merging
- Settings can be attached to an agent or runner.
- Runner-level settings override conflicting per-agent settings.
- Nested `reasoning`, `text`, `promptCacheOptions`, and `retry` values are merged unless an inherited value is explicitly cleared with `undefined`.
- A model timeout aborts the current model request attempt. Retry policy decides whether another attempt is allowed.
- `preserveRawUsage: true` requests best-effort preservation of provider-specific usage data / distinction between omitted and normalized zero values.

## GPT-5.6 reasoning and prompt caching
- GPT-5.6 adds request-level reasoning modes and explicit prompt-cache breakpoints.
- `reasoning.mode` and `reasoning.context` are Responses-only.
- `promptCacheOptions` works on both Responses and Chat Completions model paths in the described SDK.
- Implicit prompt-cache mode allows OpenAI to choose an automatic breakpoint in addition to explicit breakpoints.
- Explicit mode uses only marked content parts and the source states a current minimum cache lifetime of 30 minutes.

## Model retries
- Retries are runtime-only and opt-in: configure `modelSettings.retry` and a policy that returns a retry decision.
- `ModelRetrySettings`: `maxRetries`, `backoff`, `policy`.
- `RetryPolicyContext` includes attempt/maxRetries, stream, raw error, normalized status/retry data, provider advice, and replay-safety/statefulness facts.
- Policies can return `true`/`false`, or an object including `retry`, optional `delayMs`, `reason`, and `approveUnsafeReplay`.
- Helpers: `retryPolicies.never()`, `providerSuggested()`, `networkError()`, `httpStatus([...])`, `retryAfter()`, `any(...)`, `all(...)`.
- `providerSuggested()` is described as the safest first building block because it preserves provider vetoes and replay-safety approvals when available.
- Stateful follow-ups using `previousResponseId` or `conversationId` are treated conservatively; network/HTTP predicates alone are insufficient without a replay-safe provider approval.
- `approveUnsafeReplay: true` explicitly acknowledges that a non-streaming retry may duplicate provider work/response. It does not override abort handling or unsafe streamed replay.
- Runner/agent retry settings are deep-merged; partial agent overrides inherit the rest from the runner unless cleared with `undefined`.

## Stored prompts
- Agent `prompt` selects a server-stored prompt configuration and is supported with the OpenAI Responses API per this source.
- Fields: `promptId`, `version`, `variables`.
- Variables may be strings or content inputs such as text, images, and files.
- Additional agent configuration such as tools/instructions can override stored prompt values.
- When a stored prompt defines the model, the SDK does not send the agent default model unless explicitly overridden.

## Custom providers and AI SDK
- Custom providers implement `ModelProvider` and `Model`, then are supplied to `Runner` or made the SDK-wide default with `setDefaultModelProvider()`.
- The Vercel AI SDK adapter can connect non-OpenAI models directly to the Agents runtime without a custom provider implementation.

## Tracing
- Tracing is enabled by default in supported server runtimes in the source.
- `setTracingExportApiKey()` selects a separate credential for trace export to the OpenAI dashboard when needed.
