# P100 Extension — Realtime Voice Agents & Secure Agent Harness

**Parent:** P100 — NeXus AI Code / OMEGA-X
**Date:** 2026-09-12
**Classification:** Existing-project extension

## Mission

Integrate realtime speech agents, specialist-agent handoff and secure execution harness concepts into P100 without treating any vendor-specific interface as architectural authority.

## Realtime voice pipeline

`USER AUDIO → APP → SPEECH AGENT → TOOL CALL / SEARCH / HANDOFF → AGENT AUDIO → APP → USER`

The architecture supports a frontline voice agent routing to bounded specialist agents. Handoffs must preserve task identity, authorization scope, session identity, provenance and postconditions.

## Capability classes

- speech input/output;
- speech-to-speech interaction;
- realtime session;
- tool calling from voice sessions;
- search from voice sessions;
- specialist-agent handoff;
- TTS generation;
- interruption/timeout handling.

## Secure agent harness

```text
SERVER / AGENT
      ↓
AGENT HARNESS
      ↓
AGENT LOOP
      ↓
MCP / TOOLS
      ↓
SANDBOX
      ↓
FILESYSTEM
      ↓
CONTROLLED NETWORK GATEWAY
      ↓
DATA / APIs / WEB
```

Secrets remain behind a dedicated secret boundary. Network access is explicitly mediated. An agent cannot turn arbitrary tool access into unrestricted network or credential access.

## Control invariants

`VOICE ≠ AUTHORITY`

`HANDOFF ≠ PRIVILEGE ESCALATION`

`TOOL CALL ≠ TRUST`

`NETWORK ACCESS ≠ AUTHORIZATION`

`THINKING TIME ≠ CORRECTNESS`

## Reasoning budget

Extended-thinking controls become a governed resource policy:

`TASK COMPLEXITY → REASONING BUDGET → COST/LATENCY → EVALUATION`

Reasoning budget changes may affect latency/cost but do not bypass policy, authorization or independent verification.

## Prompt-injection defense

The hidden-text CV example is represented as an adversarial-input test case. P100 should detect instruction-bearing content embedded in untrusted documents and keep document data separate from executable instructions.

Required controls include:

- hidden-content detection where technically feasible;
- untrusted-input labeling;
- instruction/data separation;
- sanitization and normalization;
- adversarial evaluation;
- no automatic privilege escalation from retrieved/document content.

## Verification

- session and agent identity;
- handoff envelope integrity;
- capability lease continuity;
- tool-call provenance;
- network egress enforcement;
- secret isolation;
- sandbox containment;
- voice interruption and timeout behavior;
- prompt-injection resistance;
- speech artifact provenance;
- cost/latency measurement.

## Decision

Existing P100 extension. No standalone project.
