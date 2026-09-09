# Project 74 — iCar Agentic Vehicle Diagnostics & Evidence Fabric MAX

## Status
PROPOSED → ARCHITECTURE BASELINE → PROJECT GENESIS 2026-09-09

## Mission
Turn the supplied iCar/OBD2 material into a governed vehicle-diagnostics platform that connects mobile OBD2 acquisition, structured vehicle state, diagnostic evidence, agentic reasoning and reproducible reports.

The system is a **diagnostic evidence platform**, not an autonomous repair or safety-critical vehicle-control system.

## Source-derived basis
Primary source-derived repository artifact:

- `docs/knowledge-base/icar-obd2-mobile-diagnostics-reference-2026-09-09.md`

Relevant portfolio integrations:

- Project 31 — Sovereign Agent Operating Fabric
- Project 37 — Sovereign Edge AI Runtime
- Project 40 — Agentic Development & Visual Intelligence Fabric
- Project 41 — Repository/Multimodal Action Fabric
- Project 57 — Multimodal Intelligence & Cognitive Interface Fabric
- Project 58 — Monitorability-Aware Oversight & Verification
- Project 69 — Adversarial Continuity & Mobile AI Defense
- Project 72 — Cross-Framework Agent Assurance & Runtime Verification

## Product thesis
The core transformation is:

```text
OBD2 DEVICE
   ↓
MOBILE CONNECTION
   ↓
RAW VEHICLE DATA
   ↓
NORMALIZATION
   ↓
DIAGNOSTIC EVIDENCE
   ↓
MULTI-HYPOTHESIS REASONING
   ↓
VERIFICATION / CROSS-CHECK
   ↓
DIAGNOSTIC REPORT
   ↓
HUMAN DECISION
```

The platform must never turn a single diagnostic code into a definitive mechanical diagnosis without sufficient evidence.

## 1. Device boundary

The source material describes iCar2/iCar3/iCar Pro-class OBD2 devices and mobile/desktop usage across supported operating environments. Device capabilities, pairing behavior and protocol compatibility remain source-derived until verified on the actual hardware/vehicle combination.

The architecture therefore separates:

```text
DEVICE PROFILE
CONNECTION PROFILE
VEHICLE PROFILE
PROTOCOL PROFILE
APPLICATION PROFILE
```

No capability is inferred solely from the product name.

## 2. Acquisition layer

```yaml
AcquisitionSession:
  session_id:
  device_id:
  device_firmware:
  host_device:
  host_os:
  vehicle_identity:
  connection_type:
  protocol:
  start_time:
  end_time:
  raw_frames_hash:
  acquisition_status:
```

Raw acquisition data is retained independently from normalized diagnostic interpretation.

## 3. Connection state machine

```text
DISCONNECTED
   ↓
DEVICE_DETECTED
   ↓
PAIRED
   ↓
LINK_ESTABLISHED
   ↓
PROTOCOL_NEGOTIATED
   ↓
READING
   ↓
VALIDATING
   ↓
CLOSED
```

Failure states include:

`PAIRING_FAILED | LINK_LOST | PROTOCOL_UNKNOWN | VEHICLE_UNSUPPORTED | DATA_CORRUPT | SESSION_TIMEOUT`

Recovery must be explicit and observable.

## 4. Vehicle identity

```yaml
VehicleProfile:
  make:
  model:
  model_year:
  engine_variant:
  drivetrain:
  market:
  vin_reference:
  ecu_set:
  supported_protocols: []
  known_service_history_refs: []
```

Sensitive identifiers must be minimized and protected. The diagnostic model should operate on the minimum data necessary for the requested task.

## 5. Diagnostic evidence model

```yaml
DiagnosticObservation:
  observation_id:
  ecu:
  pid_or_code:
  raw_value:
  normalized_value:
  unit:
  timestamp:
  acquisition_session:
  source:
  quality:
  repeat_count:
  corroborating_observations: []
  contradictory_observations: []
```

Diagnostic statuses:

`OBSERVED | REPEATED | CORROBORATED | INFERRED | SUSPECTED | UNRESOLVED`

A code or sensor value is evidence, not automatically a diagnosis.

## 6. Agentic diagnostic reasoning

The agent operates as a bounded hypothesis engine:

```text
OBSERVATIONS
    ↓
NORMALIZE
    ↓
GENERATE CANDIDATE CAUSES
    ↓
RANK BY EVIDENCE
    ↓
REQUEST NEXT SAFE OBSERVATION
    ↓
COMPARE HYPOTHESES
    ↓
UPDATE CONFIDENCE
    ↓
REPORT
```

The agent may recommend additional **non-invasive diagnostic observations** where supported. It must not silently authorize mechanical work, disable safety systems or control the vehicle.

## 7. Evidence-weighted diagnosis

Each candidate diagnosis is represented as:

```yaml
DiagnosticHypothesis:
  id:
  description:
  supporting_evidence: []
  contradictory_evidence: []
  missing_evidence: []
  confidence:
  confidence_basis:
  alternative_hypotheses: []
  verification_plan: []
```

Confidence is a property of the evidence state, not of model fluency.

## 8. Repeated-observation protocol

A stochastic or intermittent signal cannot be promoted from one anomalous sample to a stable fault claim.

Required pattern:

```text
ANOMALY
 ↓
REPEAT
 ↓
COMPARE CONDITIONS
 ↓
CHECK CORRELATED SIGNALS
 ↓
CLASSIFY
```

This inherits the repository's stochastic-integrity doctrine.

## 9. Diagnostic timeline

The system maintains a temporal graph of:

- fault-code appearance;
- sensor anomalies;
- ignition cycles;
- connection sessions;
- user observations;
- service events;
- environmental/context variables where available.

This enables the agent to reason about sequence rather than isolated values.

## 10. Mobile-first interface

Primary surfaces:

1. **Connection** — device, vehicle and session state.
2. **Live Data** — selected signals with units and freshness.
3. **Faults** — codes with evidence context.
4. **Hypotheses** — ranked candidate explanations.
5. **Tests** — safe observation requests.
6. **Timeline** — temporal correlation.
7. **Report** — evidence-backed summary.
8. **Session Archive** — reproducible diagnostic sessions.

The UI must clearly distinguish:

`RAW VALUE → NORMALIZED VALUE → MODEL INTERPRETATION`.

## 11. Offline/local-first operation

A core design requirement is operation without mandatory cloud inference:

```text
DEVICE
 ↓
ANDROID / IOS / LOCAL HOST
 ↓
LOCAL NORMALIZER
 ↓
LOCAL DIAGNOSTIC MODEL
 ↓
LOCAL EVIDENCE STORE
```

Cloud reasoning is an optional escalation path for non-sensitive or explicitly authorized data.

## 12. Multimodal evidence

The platform may later accept:

- dashboard photographs;
- engine-bay photographs;
- maintenance documents;
- user-described symptoms;
- diagnostic codes;
- sensor traces;
- audio recordings;
- service invoices.

Each modality remains separately provenance-tagged.

No visual model output may silently overwrite measured OBD2 data.

## 13. Safety boundary

Project 74 is strictly diagnostic/analytical.

The platform does not provide autonomous execution for:

- steering;
- braking;
- throttle control;
- disabling safety systems;
- immobilizer bypass;
- unauthorized ECU modification;
- emissions-control defeat;
- security-control bypass.

Any future actuation research requires a separate safety-critical architecture, explicit authorization and independent verification.

## 14. Security architecture

Threat model includes:

- malicious or compromised diagnostic adapters;
- forged vehicle data;
- stale session data;
- replayed observations;
- malicious mobile applications;
- prompt injection in imported service documents;
- corrupted diagnostic reports;
- unauthorized vehicle identity exposure.

Controls:

```text
UNTRUSTED INPUT
 ↓
PARSER / SCHEMA VALIDATION
 ↓
PROVENANCE
 ↓
CAPABILITY POLICY
 ↓
SANDBOXED ANALYSIS
 ↓
AUTHORITATIVE SESSION STATE
 ↓
REPORT
```

## 15. Evidence integrity

Each session receives a verifiable manifest:

```yaml
DiagnosticManifest:
  session_hash:
  raw_data_hash:
  normalized_data_hash:
  model_version:
  ruleset_version:
  vehicle_profile_hash:
  evidence_refs: []
  report_hash:
  generated_at:
```

This permits later replay and dispute analysis.

## 16. Agent assurance

Project 72 integration requires:

- capability ≠ authorization;
- memory ≠ authorization;
- model confidence ≠ evidence truth;
- generated report ≠ authoritative vehicle state;
- recommendation ≠ execution;
- postcondition verification for any future consequential integration.

The diagnostic agent must fail closed on unknown protocol, ambiguous vehicle identity or unsupported capability.

## 17. Diagnostic report contract

```yaml
DiagnosticReport:
  vehicle:
  session:
  observations: []
  confirmed_findings: []
  probable_findings: []
  unresolved_questions: []
  alternative_explanations: []
  recommended_non_invasive_checks: []
  evidence_manifest:
  limitations: []
  model_disclaimer:
```

The report must state what was actually measured, what was inferred and what remains unknown.

## 18. Verification ladder

```text
V0 CONNECTION TEST
V1 DATA INTEGRITY
V2 PROTOCOL / PID VALIDATION
V3 REPEATABILITY
V4 CROSS-SIGNAL CONSISTENCY
V5 HYPOTHESIS CONSISTENCY
V6 REPORT PROVENANCE
V7 HUMAN REVIEW
```

No level may be skipped merely because the language model reports high confidence.

## 19. Testing

### Unit
- parsers;
- PID/code normalization;
- unit conversion;
- session state machine;
- evidence hashing.

### Integration
- device pairing;
- reconnect;
- protocol negotiation;
- live-data acquisition;
- session persistence.

### Adversarial
- malformed frames;
- stale data;
- contradictory values;
- replayed sessions;
- forged metadata;
- injected instructions in documents.

### Diagnostic reasoning
- known synthetic cases;
- ambiguous cases;
- repeated intermittent cases;
- negative findings;
- conflicting evidence.

## 20. Manufacturing / hardware evolution

If the project later moves from software-only diagnostics to hardware development, every hardware claim must be validated on production-intent batches. Device compatibility must be measured rather than inferred from marketing specifications.

## 21. Product roadmap

### Phase 1 — Evidence foundation
- iCar connection profiles;
- session recording;
- raw/normalized data separation;
- diagnostic evidence schema.

### Phase 2 — Diagnostic intelligence
- hypothesis engine;
- repeated-observation protocol;
- timeline correlation;
- evidence-backed reports.

### Phase 3 — Multimodal diagnostics
- photo/document ingestion;
- cross-modal provenance;
- local multimodal reasoning.

### Phase 4 — Assurance fabric
- Project 72 event contract;
- replay;
- policy enforcement;
- monitorability-aware agent supervision.

### Phase 5 — Production
- device compatibility matrix;
- automated regression suite;
- privacy/security audit;
- real-world validation across controlled vehicle cohorts.

## Definition of Done

1. A supported iCar-class device can create a reproducible diagnostic session.
2. Raw acquisition data is preserved separately from interpretation.
3. Vehicle/protocol/device identity is explicit.
4. Diagnostic hypotheses contain supporting, contradictory and missing evidence.
5. Intermittent anomalies require repeated observation before escalation.
6. Local-first operation works for the core diagnostic workflow.
7. Reports distinguish measured facts from inference and uncertainty.
8. Session manifests permit replay and integrity verification.
9. Malformed, stale and forged inputs are handled defensively.
10. The agent cannot directly actuate safety-critical vehicle controls.
11. Unsupported capabilities fail closed.
12. Real-world diagnostic accuracy is measured on controlled test cases before production claims.
13. Human review remains the final gate for consequential repair decisions.

## Maximum-evolution target

Project 74 is the portfolio's concrete bridge between **edge devices, mobile AI, multimodal evidence, agentic reasoning and runtime assurance**. It converts the iCar source from an operating manual into a reusable diagnostic system architecture while preserving the repository's evidence/authorization/verification doctrine.
