# Knowledge Corpus — AegisFleet / CALL-E / Logistics Crisis Coordination

Date: 2026-09-12
Source type: user-provided grant application and technical prototype specification.
Classification: product architecture + voice-agent orchestration + enterprise reliability.

## 1. Executive extraction

AegisFleet is proposed as a B2B fleet/logistics crisis-coordination system using CALL-E voice agents through Model Context Protocol (MCP). The operational pattern is goal-driven phone coordination with drivers/warehouse personnel, structured result extraction, ERP integration, and event-driven completion handling.

The source describes a target track named `Fortified Enterprise Fleet` and a claimed Grand Prize target of USD 50,000. The source also states that the referenced Devpost submission deadline was 31 August 2026; this date and prize/track claims are source assertions and are not independently verified here.

## 2. Core architecture extracted from the source

`INCIDENT → GOAL → CALL PLAN → HUMAN/AGENT AUTHORIZATION BOUNDARY → CALL RUN → ASYNC EVENT → RESULT SCHEMA VALIDATION → EVIDENCE → ERP UPDATE → AUDIT`

CALL-E MCP surface described by the source:

- `plan_call(goal, phone)` — creates/refines a conversation plan without initiating the call; returns `ready_to_run`, `plan_id`, and `confirm_token` according to the source.
- `run_call(plan_id, confirm_token)` — executes a previously planned call and returns `run_id`; the source explicitly notes that this tool does not accept a webhook URL.
- `get_call_run(run_id)` — retrieves run state/result.

The source additionally describes OAuth authorization, streaming HTTP MCP, asynchronous terminal webhooks, and integration with enterprise systems.

## 3. Structured result contract

The source proposes JSON Schema as the boundary between conversational inference and deterministic enterprise data handling.

Key patterns:

- `additionalProperties: false` to reject undeclared output fields.
- String enums for business decisions rather than unconstrained booleans.
- Explicit `unknown` state where conversational evidence is insufficient.
- Required `evidence_summary` / `evidence` field to preserve an auditable rationale tied to the conversation.
- Optional `recipient_result_schema` for batch/multi-recipient calling, as described by the source.

Canonical example fields in the supplied prototype:

- `route_acceptance`: `yes | no | unknown`
- `eta_update_time`: string
- `escalation_needed`: `urgent | normal | none | unknown`
- `evidence_summary`: string

Important verification rule: a schema constrains shape; it does not itself establish that the extracted claim is true. Evidence must remain distinct from model interpretation.

## 4. Reliability patterns

The source emphasizes distributed-systems reliability:

### Idempotency

Each Goal Run creation is described as carrying an `Idempotency-Key`, allowing safe retry without intentionally creating a duplicate call.

### Event deduplication

Terminal webhook events are treated as untrusted input. The proposed implementation compares the `CALL-E-Event-Id` header with the event/body identifier before persisting state into ERP.

This is a strong pattern, but it should be implemented as an explicit event-ingestion state machine with replay handling, signature/authentication validation where supported, schema validation, ordering rules, and durable idempotency records.

### State authority

`WEBHOOK OBSERVATION ≠ AUTHORIZATION`
`MODEL RESULT ≠ ERP WRITE AUTHORIZATION`
`SCHEMA VALIDITY ≠ FACTUAL TRUTH`

ERP mutation should therefore pass through policy, authorization, postcondition verification, and audit logging.

## 5. CALL-E + MCP capability boundary

The source provides a useful capability architecture for the broader knowledge base:

`LOGISTICS ORCHESTRATOR → MCP CLIENT → CALL-E CAPABILITY SERVER → VOICE EXECUTION → EVENT STREAM → RESULT CONTRACT → POLICY GATE → ERP`

MCP should be treated as a capability transport/interface, not as the authority that decides whether a consequential business action is allowed.

## 6. Enterprise workflow model

Recommended normalized workflow derived from the source:

`INCIDENT DETECTION → IMPACT ANALYSIS → CONTACT SELECTION → GOAL FORMULATION → CALL PLAN → AUTHORIZATION → CALL EXECUTION → TRANSCRIPT/EVENT INGESTION → STRUCTURED EXTRACTION → EVIDENCE CHECK → HUMAN ESCALATION OR ACTION → ERP WRITE → READBACK → POSTCONDITION VERIFICATION → AUDIT/PROVENANCE`

This extends the repository doctrine:

`OBSERVE → PLAN → AUTHORIZE → ACT → READBACK → VERIFY`

## 7. Crisis logistics use cases

Source-supported examples include:

- road closure / route renegotiation;
- contacting drivers during operational incidents;
- obtaining updated ETA;
- escalating unclear or urgent conditions;
- propagating verified structured results into ERP;
- batch coordination with multiple recipients.

The broader concept is an event-driven voice operations layer for time-critical fleet exceptions.

## 8. Technical corrections / evidence discipline

The supplied application contains strong architecture ideas but also uses language stronger than the evidence supports. The knowledge base must normalize these claims:

- `JSON Schema ≠ hallucination elimination`;
- `additionalProperties: false ≠ factual correctness`;
- `evidence_summary ≠ independent evidence verification`;
- `Idempotency-Key ≠ universal duplicate prevention unless the server honors the contract correctly`;
- `event ID comparison ≠ complete webhook security`;
- `successful call ≠ successful business outcome`;
- `taskCompleted ≠ independently verified postcondition`;
- `lower call cost ≠ proven ROI` without measured baseline and total cost of ownership.

The supplied TypeScript is a proof-of-concept sketch, not independently verified production code. SDK version, API semantics, exact authentication flow, webhook contract, and result behavior must be verified against authoritative CALL-E documentation before implementation claims are promoted to verified facts.

## 9. Relationship to existing projects

Strongest integrations:

- P100 — Nexus AI Code / enterprise agentic control plane: MCP capability registry, authorization, typed workflows, provenance, CI/security and enterprise orchestration.
- Voice-agent knowledge base: realtime voice, phone/telephony, hosted MCP tools, approvals, tracing and server-side credentials.
- P115 — OmniPrivacy / identity relay: provider-neutral communication identity and endpoint lifecycle, where privacy requirements apply.
- P119 — OmniMAS Local Android Agent Runtime: mobile agent/device action/readback patterns when driver-side mobile endpoints are involved.
- P32 — phone intelligence: contact/phone intelligence should remain bounded by authorization and privacy policy.
- P97 — OmniMedia recursive production factory: only tangentially relevant for demo/video production, not core architecture.

## 10. New architectural insight

AegisFleet warrants a dedicated vertical project because it combines the repository's mature primitives into a concrete high-consequence enterprise domain:

`EVENT → LOGISTICS STATE → VOICE GOAL → MCP CAPABILITY → AUTHORIZED CALL → STRUCTURED RESULT → EVIDENCE → HUMAN ESCALATION → ERP ACTION → READBACK → VERIFIED POSTCONDITION`

The central design principle is **voice-mediated operational actuation with explicit authorization and evidence boundaries**.

## 11. Security and safety invariants

- `MCP ≠ AUTHORIZATION AUTHORITY`
- `CALL PLAN ≠ CALL AUTHORIZATION`
- `CONFIRM TOKEN ≠ BUSINESS APPROVAL unless explicitly bound to policy`
- `VOICE TRANSCRIPT ≠ VERIFIED FACT`
- `STRUCTURED JSON ≠ TRUSTED DATA`
- `WEBHOOK ≠ TRUSTED INPUT`
- `CALL COMPLETION ≠ BUSINESS COMPLETION`
- `ERP WRITE ≠ VERIFIED STATE`
- `AUTONOMOUS NEGOTIATION ≠ UNBOUNDED AUTONOMY`
- `SYNTHETIC CALL ≠ REAL-WORLD EVIDENCE`

For real deployments, consent, call recording/transcription law, data minimization, retention, regional telephony rules, worker safety, escalation policy, and emergency-call restrictions require explicit legal/product review.
