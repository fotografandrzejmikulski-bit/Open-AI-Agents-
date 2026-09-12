# P120 — AegisFleet: Autonomous Logistics & Crisis Coordination

**Status:** CONCEPT / ARCHITECTURE-READY / PROTOTYPE CLAIMS REQUIRE VERIFICATION  
**Domain:** enterprise fleet logistics, crisis response, voice agents, MCP, ERP integration  
**Primary substrate:** CALL-E voice-call capability exposed through MCP  
**Relationship:** vertical application of the repository's enterprise agent-control doctrine.

## 1. Product definition

AegisFleet is a proposed enterprise system for coordinating fleet exceptions and supply-chain incidents through goal-driven voice agents. An incident becomes a bounded operational goal; the system plans and executes authorized calls, extracts structured results, preserves evidence, escalates uncertainty, and only then proposes or performs ERP state changes.

Core loop:

`INCIDENT → GOAL → PLAN → AUTHORIZE → CALL → EVENT → EXTRACT → EVIDENCE → ESCALATE/ACT → ERP → READBACK → VERIFY`

## 2. Primary use case

A road closure or comparable logistics exception creates a need to contact a driver, communicate the operational constraint, negotiate/confirm an alternate route, obtain an updated ETA, and propagate the verified result to enterprise systems.

The architecture must support both single-recipient and batch coordination while preserving per-recipient state, provenance, idempotency, and escalation.

## 3. CALL-E integration model

The supplied source describes an MCP interface containing:

- `plan_call(goal, phone)`;
- `run_call(plan_id, confirm_token)`;
- `get_call_run(run_id)`.

The source describes OAuth, streaming HTTP MCP, asynchronous terminal webhooks, and a server-side SDK. These integration details are **source-reported and require authoritative vendor verification before being treated as current API facts**.

## 4. Control-plane architecture

```text
┌──────────────────────┐
│ Incident / TMS / ERP │
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│ AegisFleet Director  │
│ goal + policy engine │
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│ Capability Registry  │
│ CALL-E / MCP / voice │
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│ Plan → Authorize     │
│ approval boundary    │
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│ CALL-E execution     │
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│ Webhook/Event Intake │
│ untrusted input      │
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│ Schema + Evidence    │
│ + confidence/unknown │
└───────┬───────┬──────┘
        ↓       ↓
     ERP write  Human escalation
        ↓
┌──────────────────────┐
│ Readback + Verify    │
└──────────────────────┘
```

## 5. Structured result contract

AegisFleet should use versioned JSON Schemas as the machine interface between conversational extraction and enterprise workflows.

Example contract:

- `route_acceptance`: `yes | no | unknown`;
- `eta_update_time`: string or a future normalized time representation;
- `escalation_needed`: `urgent | normal | none | unknown`;
- `evidence_summary`: concise source-linked evidence;
- `schema_version`: explicit contract version;
- provenance metadata: run/event identifiers and timestamps.

`unknown` is a first-class operational state, not a failure to be hidden.

## 6. Reliability engineering

### Idempotency

Goal-run creation must carry an idempotency key whose scope, retention, replay semantics and server-side enforcement are explicitly documented.

### Event processing

Webhook ingestion must:

1. authenticate/validate the event according to the provider contract;
2. validate payload schema;
3. correlate event ID, run ID and business entity;
4. deduplicate durably;
5. handle replay/out-of-order events;
6. persist an immutable event record;
7. derive state through a deterministic state transition;
8. permit safe retry.

### State machine

Recommended terminal states:

`PLANNED → AUTHORIZED → RUNNING → COMPLETED | FAILED | UNKNOWN | ESCALATED`

ERP mutation is a separate state transition and must not be inferred solely from call completion.

## 7. Authorization doctrine

AegisFleet inherits the repository control doctrine:

`OBSERVE → PLAN → AUTHORIZE → ACT → READBACK → VERIFY`

Specific boundaries:

- the incident detector cannot directly authorize a phone call;
- the LLM cannot directly authorize an ERP mutation;
- MCP exposes capabilities but is not the policy authority;
- a valid JSON object is not sufficient evidence of truth;
- human approval must be represented as an auditable state transition where required;
- emergency or safety-critical actions must fail closed or escalate when authority is ambiguous.

## 8. Evidence model

Every consequential result should preserve:

`EVENT → SOURCE → TRANSCRIPT/EXTRACTION → CLAIM → EVIDENCE → DECISION → ACTION → POSTCONDITION`

The supplied `evidence_summary` pattern is useful, but exact quotation or summary alone is not independent verification. For disputes, regulated workflows, or insurance claims, retention and provenance requirements must be defined explicitly.

## 9. Multi-agent extension

A production implementation can decompose into bounded agents:

- **Incident Agent** — detects/normalizes exception state;
- **Planning Agent** — generates contact/route goals;
- **Voice Agent** — executes the authorized conversational task;
- **Extraction Agent** — maps the call result to the schema;
- **Evidence Agent** — checks source/evidence completeness;
- **Policy Agent** — evaluates escalation and permitted action;
- **ERP Agent** — performs only authorized writes;
- **Verification Agent** — reads back state and checks postconditions;
- **Audit Agent** — records provenance and decision lineage.

Agent boundaries must not create implicit authorization chains.

## 10. Business viability measurement

Do not use generic claims of "autonomy" or lower per-minute cost as proof of viability. AegisFleet requires an evidence-driven evaluation framework:

- dispatcher minutes saved per incident;
- time-to-first-contact;
- time-to-resolution;
- successful contact rate;
- structured-result validity rate;
- unknown/escalation rate;
- duplicate-call rate;
- ERP postcondition success rate;
- human override rate;
- cost per resolved incident;
- penalty/late-delivery reduction;
- total operating cost;
- safety/compliance incident rate.

`METRIC ≠ CAUSALITY` and `DEMO SUCCESS ≠ BUSINESS ROI`.

## 11. Prototype assessment

The supplied TypeScript prototype demonstrates the intended SDK-shaped interaction and result schema concept. It should be treated as a **PoC sketch**, not verified production software. Before implementation claims are promoted, verify the actual package, SDK methods, API version, authentication mechanism, webhook semantics, idempotency behavior, result schema support, and `taskCompleted` semantics against authoritative CALL-E documentation and a live test environment.

## 12. Relationship to existing portfolio

P120 is a new vertical product project, while its primitives are reused from:

- **P100** — enterprise agentic control plane, MCP, capability registry, policy/authorization, provenance and DevSecOps;
- **Voice-agent knowledge base** — realtime voice/phone agent architecture and hosted MCP capabilities;
- **P115** — identity/communication endpoint separation where required;
- **P119** — mobile agent/device execution and readback where field endpoints are involved;
- **P32** — phone intelligence under bounded authorization/privacy controls.

P120 should therefore not duplicate infrastructure already governed by P100; it should consume those primitives as a logistics-domain application layer.

## 13. Security, privacy and compliance

The product operates on employee/contractor communications and potentially location, route, cargo and operational data. Production design must address:

- least-privilege credentials;
- secret isolation;
- caller identity and recipient verification;
- consent and applicable call-recording/transcription law;
- data minimization and retention;
- regional telephony requirements;
- prompt injection through external conversational content;
- malicious/incorrect instructions from callers;
- human escalation for ambiguous operational states;
- audit integrity;
- tenant isolation for B2B deployments.

## 14. Invariants

- `VOICE ≠ AUTHORITY`
- `MCP ≠ AUTHORIZATION`
- `CALL PLAN ≠ APPROVAL`
- `TRANSCRIPT ≠ FACT`
- `SCHEMA VALIDITY ≠ TRUTH`
- `WEBHOOK ≠ TRUSTED INPUT`
- `CALL COMPLETION ≠ BUSINESS COMPLETION`
- `ERP WRITE ≠ VERIFIED STATE`
- `AUTONOMY ≠ UNBOUNDED ACTION`
- `LOWER COST ≠ PROVEN ROI`

## 15. Next implementation gate

The first implementation milestone is not broad autonomy. It is a **single incident, single driver, single bounded goal** with:

`PLAN → EXPLICIT AUTHORIZATION → CALL → STRUCTURED RESULT → EVENT DEDUPLICATION → HUMAN REVIEW → ERP SANDBOX WRITE → READBACK → VERIFIED POSTCONDITION`.

Only after this path is independently tested should batch calls, automated escalation, and higher autonomy be promoted.
