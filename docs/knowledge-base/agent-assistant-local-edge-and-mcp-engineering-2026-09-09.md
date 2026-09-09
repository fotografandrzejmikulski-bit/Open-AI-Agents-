# Agent Assistant Engineering — System Prompts, Knowledge Bases, MCP & Local/Edge Inference — 2026-09-09

## Status

`SOURCE_DERIVED → ENGINEERING_SYNTHESIS → PROPOSED`

This artifact consolidates the supplied small-business AI assistant, MCP integration, UC Berkeley AI-business and local/edge architecture materials. Provider-specific claims and numerical performance claims remain source-derived and time-bounded; they are not treated as universal benchmarks.

## 1. Agent constitution

The supplied assistant guide frames the system prompt as the agent's constitutional layer. A reusable structure is:

```text
ROLE / IDENTITY
↓
GOAL / MISSION
↓
WORKFLOW / ACTION PROCESS
↓
KNOWLEDGE SOURCES
↓
LIMITATIONS / CONSTRAINTS
↓
VERIFICATION / ESCALATION
```

The workflow should identify the request, retrieve relevant knowledge, cite the source when available, answer within scope and refuse guessing when evidence is insufficient. fileciteturn76file3L224-L258

## 2. Knowledge-base engineering

The source recommends thematic segmentation, explicit file naming/tagging, structured Markdown/CSV/JSON where appropriate, access restrictions, anonymization of PII and recurring freshness checks. These are useful engineering patterns, but source-stated percentage improvements are retained only as source-derived claims. fileciteturn76file15L862-L904

A production architecture should additionally track:

```yaml
KnowledgeAsset:
  id:
  domain:
  version:
  effective_from:
  effective_to:
  authority:
  provenance:
  access_policy:
  pii_class:
  freshness:
  validation_state:
```

## 3. Tool and MCP boundary

MCP is treated as an integration mechanism, not as an authorization authority. The supplied material describes connectors to databases, CRM and communication systems and recommends testing integrations with dummy queries, using OAuth/rate limits where supported and keeping credentials in a vault rather than hard-coding them. fileciteturn76file1L91-L110

OmniCore integration rule:

```text
MODEL INTENT
 → CAPABILITY FILTER
 → AUTHORIZATION
 → MCP CALL
 → OUTPUT VALIDATION
 → POSTCONDITION CHECK
 → AUDIT EVENT
```

## 4. Local / edge / cloud model routing

The local-first material demonstrates a provider abstraction in which application logic is separated from the selected inference backend. Its example uses Genkit with a local Ollama model and structured JSON output, allowing the model provider to be changed without rewriting business logic. fileciteturn76file6L406-L433

The reusable architecture is:

```text
APPLICATION LOGIC
      ↓
MODEL INTERFACE / CONTRACT
      ├── LOCAL INFERENCE
      ├── EDGE / DEVICE INFERENCE
      └── CLOUD FALLBACK
```

Routing should be based on capability, latency, privacy, cost, context requirements and reliability rather than vendor identity alone.

## 5. Mobile inference

The supplied Android material describes on-device inference using AICore and MediaPipe LLM Inference, including GPU execution and downloading model artifacts at first launch rather than packaging large model files directly in the APK. fileciteturn76file11L645-L689

For production, model artifacts require integrity verification, version pinning, storage permissions, rollback handling and provenance. Development paths such as `adb push` must not be mistaken for deployment architecture. fileciteturn76file11L667-L691

## 6. Verification pattern

The supplied business-assistant material recommends sandbox testing, guardrails, logs and iterative refinement. fileciteturn76file1L117-L137

The repository generalizes this into:

```text
UNIT TESTS
 → TOOL CONTRACT TESTS
 → PROMPT-INJECTION TESTS
 → KNOWLEDGE RETRIEVAL TESTS
 → AUTHORIZATION TESTS
 → FAILURE / FALLBACK TESTS
 → POSTCONDITION VERIFICATION
 → PRODUCTION TELEMETRY
```

## 7. Portfolio integration

This artifact strengthens the existing assistant, MCP, model-routing, sovereign-edge and runtime-assurance lineage. No new numbered project is justified solely by these materials because the reusable capabilities already belong to those project families.

## Final principle

`An agent is an engineered system when identity, knowledge, tools, authorization, execution and verification are explicit contracts rather than prompt prose.`
