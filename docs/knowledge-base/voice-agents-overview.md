# Voice Agents — Overview

Source: OpenAI Agents SDK TypeScript documentation supplied in conversation.

## Core model
Voice Agents provide low-latency spoken interfaces on top of OpenAI speech-to-speech models. The Agents SDK keeps the Realtime API mental model while adding a TypeScript-first layer around `RealtimeAgent`, `RealtimeSession`, and transport helpers.

## Realtime foundations
Underlying Realtime concepts remain applicable, including WebRTC, realtime conversations, and voice activity detection (VAD). The SDK abstracts transport/event handling so application code can focus on product logic.

## What the SDK adds
- Browser-first WebRTC setup with ephemeral client tokens.
- Server-side WebSocket and SIP transport options.
- Automatic interruption handling and local conversation-history updates.
- Multi-agent orchestration through realtime handoffs.
- Function tools, hosted MCP tools, approvals, and delegation patterns.
- Output guardrails and tracing for live spoken interactions.

## Transport choices
Relevant paths include:
- WebRTC for browser clients.
- WebSocket for server-side realtime connections.
- SIP for telephony-oriented realtime connections.
- Twilio integration for phone/telephony experiences.
- Cloudflare Workers/workerd runtimes.
- Custom transports when required.

## Speech-to-speech rationale
Speech-to-speech models process user audio directly, avoiding a required per-turn STT → text reasoning → TTS chain. This reduces latency and supports more natural interruptions, mixed text/voice input, and tool calls in realtime applications.

## Diagram semantics captured
The supplied architecture diagram shows:
`User audio → App → Voice Agent (speech-to-speech model) → App → Agent audio`,
with the agent able to perform tool calls to function tools, search, and handoffs.

## Documentation navigation
- Voice Agents Quickstart: browser/WebRTC setup with ephemeral tokens.
- Building Voice Agents: session lifecycle, VAD, interruptions, multimodal input, tools, and history.
- Realtime Transport Layer: WebRTC/WebSocket/SIP/custom transport decisions.
- Voice Agents on Twilio: telephony.
- Voice Agents on Cloudflare: workerd/Cloudflare Workers.
