# Voice Agents

## Overview
Voice Agents provide low-latency spoken interfaces over OpenAI speech-to-speech models. The Agents SDK wraps Realtime API concepts with `RealtimeAgent`, `RealtimeSession`, and transport helpers. The same Realtime concepts remain applicable underneath.

## Browser quickstart and credentials
- Recommended package: `@openai/agents` (requires Zod v4).
- Browser apps should obtain a short-lived ephemeral client token from a backend using `POST /v1/realtime/client_secrets` with the server OpenAI API key, then pass the returned `ek_...` value to `session.connect(...)`.
- Long-lived API keys must not be exposed in browser code.
- Secure hosted MCP configuration/credentials needed by the realtime session should be included server-side when minting the ephemeral client secret.

## RealtimeAgent and RealtimeSession
- `RealtimeAgent` is similar to a regular `Agent`.
- A voice agent runs continuously inside `RealtimeSession`, which manages the conversation, connection, audio processing, interruptions, and lifecycle.
- Browser `OpenAIRealtimeWebRTC` is the default low-friction browser transport and manages microphone capture/playback.
- In server runtimes the default path falls back to WebSocket; application code then handles audio capture/playback.

## Session configuration
Prefer the nested modern configuration shape:
- `outputModalities: ['audio']` for speech-to-speech (audio output plus transcripts).
- `audio.input.format` / `audio.output.format`.
- `audio.input.transcription` for transcription model/context.
- `audio.input.turnDetection` for VAD/turn control.
- `reasoning.effort` for supported reasoning-capable realtime models.
- `parallelToolCalls` to allow/disallow parallel tool calls.
- `providerData` for raw/new session fields not represented by `RealtimeSessionConfig`.

Useful `RealtimeSession` options include local context, audio-history storage, output guardrails, tracing configuration, workflow/group trace metadata, automatic MCP-response triggering, tool error formatting, and realtime tool execution settings.

## Conversation lifecycle
- Realtime sessions are long-lived.
- `RealtimeSession` tracks local conversation history, listens to transport events, executes tools and output guardrails, and synchronizes active-agent configuration.
- Realtime sessions currently have a 60-minute limit.
- `session.connect()` readiness semantics differ by transport: WebRTC attempts to wait for `session.updated` after initial config; WebSocket resolves after socket open and initial config send, so `session.updated` may arrive afterward.
- Model cannot change mid-conversation. Voice changes only work before the session has produced audio output. Tracing should be decided up front.
- Input transcription is asynchronous and may arrive after response generation has started.

## Turn detection and interruptions
- Built-in VAD is enabled by default through `audio.input.turnDetection`.
- Common modes: `semantic_vad` for natural boundaries and `server_vad` for threshold-driven behavior.
- Set turn detection to `null` for full manual control.
- With VAD enabled, speaking over the agent can interrupt the response.
- WebRTC clears buffered output audio automatically; on WebSocket, application code must stop local playback and handle the relevant interruption/truncation events.
- For moderation/validation before response generation, VAD can remain enabled while `createResponse` and `interruptResponse` are disabled.

## Text and image input
- `sendMessage()` sends typed/structured user content into the live conversation.
- `addImage()` attaches image input. `triggerResponse: false` allows batching before a later response.
- This supports mixed text/voice interaction, explicit clarifications, and multimodal flows.

## Handoffs
- Realtime voice agents support handoffs between `RealtimeAgent` configurations.
- A realtime handoff updates the active agent configuration within the same live session, so the new agent has the ongoing conversation history.
- Input filters are currently not applied during realtime handoffs.
- The session's model remains unchanged across a realtime handoff.
- Voice changes follow the underlying Realtime rule: only before any audio output has been produced.
- If a different backend/model is required, use delegation through a tool instead of a realtime handoff.

## Tools
Voice Agents support:
- local function tools;
- hosted MCP tools.

Function tools execute wherever `RealtimeSession` executes. Therefore browser-side sessions execute function tools in the browser. Sensitive operations should use the function tool as a thin backchannel to backend logic, where privileged work is performed server-side.

Programmatic Tool Calling is not available directly in Realtime sessions: function-tool `outputSchema` and `allowedCallers` values including `programmatic` are rejected, as are programmatic callers for hosted MCP tools. Delegate such work to a Responses agent/backend workflow.

Hosted MCP tools execute remotely through the Realtime API. Active availability is reflected by `session.availableMcpTools` and the `mcp_tools_changed` event. Secure hosted MCP configuration should be treated as a pre-connect, server-side concern in browser applications.

## Tool execution and background results
- While a tool executes, the voice agent cannot process new user requests.
- `backgroundResult(output)` can return tool output without immediately triggering another model response.
- Function-tool timeout settings support configurable timeout behavior.
- Function tool calls can inspect a snapshot of the conversation history at call time, but the latest user transcription may not yet be available.

## Human approval
- `needsApproval: true` causes `tool_approval_requested` before execution.
- UI can call `session.approve(request.approvalItem)` or `session.reject(...)`.
- Function tools can use sticky approval/rejection behavior for repeated calls during the session.
- Hosted MCP approvals do not support sticky approve/reject; restrict them with hosted MCP `allowedTools` instead.
- By default function-tool input guardrails run after approval. `toolExecution.preApprovalInputGuardrails: true` runs them before the approval event as well; if rejected, approval is skipped.
- While waiting for approval, the voice agent cannot process new user requests.

## Output guardrails
- Realtime output guardrails monitor streamed output and can immediately cut off unsafe output.
- Text sessions evaluate output text deltas; audio sessions evaluate output audio transcripts/transcript deltas.
- Guardrail events include `guardrail_tripped` and identifying details.
- Default cadence is every 100 characters and again at final transcript availability; `debounceTextLength: -1` runs only once on the final transcript.

## History
`RealtimeSession` automatically keeps a local history snapshot containing user messages, assistant output, tool calls, and truncation state.
- `history_updated` fires when history changes.
- `session.history` can be inspected/rendered.
- `updateHistory()` requests synchronized history changes through the transport.
- Current limitations include inability to edit function-tool calls after the fact, dependence of assistant text on available transcripts, truncated interruption responses lacking a final transcript, and input transcription being only an approximate guide to what the user said.

## Delegation through tools
A realtime browser agent can delegate a complex or privileged task to a backend Responses/Agents SDK agent through a local function tool. The browser-side tool can pass the request plus a history snapshot; the server runs a separate backend `Agent`/`run()` workflow and returns the result to the voice session. This is the recommended pattern when another model or server-side policy is needed.

## Transport selection
| Scenario | Recommended transport |
|---|---|
| Browser speech-to-speech | `OpenAIRealtimeWebRTC` |
| Browser audio, server-side Realtime controls | Browser audio-only WebRTC + server-side `RealtimeSession` |
| React Native | App-owned native WebRTC transport through `RealtimeTransportLayer` |
| Server-side voice/custom audio | `OpenAIRealtimeWebSocket` |
| SIP/telephony | `OpenAIRealtimeSIP` |
| Cloudflare Workers/workerd | Cloudflare extension transport |
| Twilio | Twilio extension transport |

## WebRTC
- Default browser transport handles microphone capture/playback and uses a data channel for Realtime events.
- Application-provided `MediaStream` remains application-owned; transport close does not stop caller-supplied tracks.
- `changePeerConnection` provides a lower-level customization escape hatch.
- Omitting a browser data channel is not an access-control boundary; a modified client can change code/SDP.

## Browser audio with server-side controls
For stronger server-side control:
1. Browser creates audio-only WebRTC peer connection and sends SDP offer to the application server.
2. Server authenticates user, applies SDP policy, and creates the Realtime call with server API credentials.
3. Server obtains the call ID and creates a server-side `RealtimeSession` using WebSocket transport as a sideband/control connection.
4. Server handles Realtime events, tools, and business logic; browser carries audio directly to Realtime.
5. Server returns only allowlisted application events to browser when status updates are needed.
6. Privileged tool authorization must use trusted authenticated application/session context, never model-supplied tool arguments.

## React Native
- Built-in browser WebRTC transport is not the React Native path.
- Use an app-owned native WebRTC implementation connected through a custom `RealtimeTransportLayer`.
- Expo Go is not supported when the native WebRTC dependency requires native code; a development build is required.
- Only ephemeral tokens should reach the mobile app.

## WebSocket
- Server-side/default server transport.
- Application manages raw PCM16 audio input/output.
- `OpenAIRealtimeWebSocket` supports custom socket connectors.

## SIP / telephony
- `OpenAIRealtimeSIP` attaches `RealtimeSession` to an existing SIP-created call using `callId`.
- SIP call acceptance supports only a subset of Realtime turn-detection fields and rejects threshold/prefix-padding/silence-duration fields during initial call configuration.

## Cloudflare Workers
workerd cannot use the global WebSocket constructor for outbound WebSockets. Use the Cloudflare realtime transport extension, which performs a fetch-based upgrade.

## Twilio
RealtimeSession can connect to Twilio through raw WebSockets or the dedicated Twilio transport. The dedicated transport is the preferred default when the SDK should handle interruption timing and media forwarding.

## Custom and raw transport control
- Implement `RealtimeTransportLayer` when integrating another speech-to-speech API/custom transport.
- `session.transport` exposes all raw events through `'*'` and allows `sendEvent()` for low-level operations such as `session.update`, `response.create`, and `response.cancel`.
- The transport can also be used alone when automatic tools/guardrails/history are not required.
