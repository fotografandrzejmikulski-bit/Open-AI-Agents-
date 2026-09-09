# Project 69 — OmniCore Adversarial Continuity & Mobile AI Defense Fabric MAX

## Mission
Build a defensive security system for threats that evolve across turns, modalities, memory and device/runtime boundaries. The project combines the Chain-of-Attack model with mobile-platform trust-boundary analysis and multilingual/encoded jailbreak research.

## Core insight
The supplied Chain-of-Attack report describes attacks whose malicious intent emerges over multiple semantically connected steps. The mobile-surveillance report describes a different but related pattern: persistence and privilege depend on crossing several independent security barriers. Both are best modeled as **attack trajectories**, not isolated events.

## Architecture
```text
INPUT / FILE / WEB / TOOL / MEMORY
                 ↓
        CANONICALIZATION LAYER
                 ↓
      TEMPORAL ATTACK GRAPH
                 ↓
   RISK / POLICY-SURFACE ANALYSIS
                 ↓
  CAPABILITY BROKER / ISOLATION
                 ↓
       EXECUTION OR DENIAL
                 ↓
 AUTHORITATIVE STATE VERIFICATION
                 ↓
      INCIDENT EVIDENCE PACK
```

## Attack trajectory schema
```yaml
Trajectory:
  session_id:
  nodes:
    - user_input
    - external_content
    - memory_write
    - tool_request
    - action
    - state_change
  edges:
    - semantic_transition
    - dependency
    - escalation
    - contradiction
  risk:
  provenance:
  detector_version:
```

## Detection families
- semantic drift toward a previously disallowed objective;
- repeated boundary probing;
- privilege/capability escalation;
- hidden instructions in external content;
- memory poisoning;
- multilingual or encoded policy circumvention;
- multimodal instruction conflicts;
- tool-result injection;
- action/claim mismatch;
- evaluation-aware or monitor-aware behavior.

## Mobile defense
Use iOS/Android trust-boundary concepts as defensive tests:
- code signing and verified boot;
- sandbox isolation;
- entitlement/permission boundaries;
- ASLR/PAC-style memory mitigations;
- SELinux/MAC;
- background execution constraints;
- network and process isolation.

The project does not reproduce surveillance malware. It measures whether analogous boundaries detect or contain an attempted compromise.

## Memory security
Durable writes require provenance, schema validation, authorization and conflict handling. High-impact claims require corroboration before promotion to trusted state.

## Multilingual/encoded normalization
```text
RAW ARTIFACT
→ PRESERVE ORIGINAL
→ NORMALIZE UNICODE / ENCODING
→ EXTRACT MODAL CONTENT
→ BUILD CANONICAL VIEW
→ CLASSIFY
→ NEVER AUTO-EXECUTE
```

## Evaluation gates
A0 single-turn baseline
A1 multi-turn continuity
A2 memory poisoning
A3 indirect prompt injection
A4 multilingual/encoding transformation
A5 multimodal conflict
A6 tool-result poisoning
A7 mobile sandbox simulation
A8 revocation during active run
A9 evaluation-aware behavior
A10 authoritative postcondition verification

## Novel contribution
Project 69 makes the security unit a **trajectory with accumulated state**, connecting AI red-team methodology to endpoint-defense engineering while keeping all privileged operations behind deterministic capability controls.
