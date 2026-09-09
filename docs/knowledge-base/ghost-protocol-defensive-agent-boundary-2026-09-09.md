# Ghost Protocol — Defensive Agent / Tool Boundary Review — 2026-09-09

## Status
`SOURCE_DERIVED → SECURITY_REVIEW → PROPOSED`

The two supplied Ghost Protocol files are near-duplicates and are consolidated here. They contain a local Ollama/Gemma agent, a command-oriented persona and active network reconnaissance logic. This artifact records the architecture and security lessons without turning the reconnaissance component into an operational intrusion toolkit.

## 1. Architecture observed in the source

Ghost v2 uses a local Ollama chat endpoint and a Gemma 2 27B model label. The agent stores conversation history, sends it to Ollama, detects a special scan token in model output, executes a network scan, inserts the scan result into the conversation context and asks the model for a final analysis. fileciteturn118file2L46-L88 fileciteturn118file2L139-L197

The source therefore implements an early form of:

```text
LLM
 ↓
TOOL INTENT TAG
 ↓
TOOL EXECUTION
 ↓
RESULT INJECTION
 ↓
LLM ANALYSIS
```

## 2. Security findings

The source has a dangerous trust boundary: model-generated text can trigger active reconnaissance. It also contains a direct command-execution mode in the original Ghost variant. The v2 scanner resolves a host, opens TCP connections and probes a fixed set of ports using multiple threads. fileciteturn118file2L90-L138

For a production agent, this must become:

```text
MODEL REQUEST
 ↓
PARSE AS UNTRUSTED DATA
 ↓
TARGET / SCOPE / AUTHORIZATION CHECK
 ↓
POLICY DECISION
 ↓
OPTIONAL HUMAN APPROVAL
 ↓
SANDBOXED TOOL
 ↓
LIMITED RESULT
 ↓
POSTCONDITION + AUDIT
```

## 3. Reusable design contribution

The useful idea is not autonomous scanning itself. It is the explicit **LLM → tool → result → re-evaluation** control loop. This can be generalized to benign tools such as repository inspection, local diagnostics, test execution and controlled data analysis.

## 4. Required controls for OmniCore integration

- no model-generated arbitrary shell execution;
- explicit capability allowlists;
- authorization bound to the target and operation, not merely to the session;
- network actions constrained to declared scopes;
- timeouts, rate limits and resource ceilings;
- immutable audit events;
- authoritative tool results separated from model claims;
- human approval for consequential operations;
- postcondition verification;
- replayable execution traces.

## 5. UI and local inference

The Ghost and Gemma artifacts together demonstrate a useful operator-console pattern: local model status, command input, staged processing indicators and a visible tool boundary. The reasoning display should expose safe telemetry, not private chain-of-thought.

## 6. Integration

Primary mappings: Projects 10, 12, 26, 35, 47, 58 and 72. No new offensive-security project is created from this material.
