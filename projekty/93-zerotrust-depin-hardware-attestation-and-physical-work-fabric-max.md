# Project 93 — Zero-Trust DePIN Hardware Attestation & Physical-Work Fabric MAX

## Status
PROPOSED → ARCHITECTURE BASELINE → PROJECT GENESIS 2026-09-10

## Mission
Design a hardware-rooted DePIN node architecture in which device identity, software state, physical/computational work and economic rewards are connected through cryptographically verifiable evidence.

The project is not a token-launch specification. It is a security and verification architecture for networks where physical nodes provide measurable resources and where economic incentives must resist cloning, replay, spoofing and reward gaming.

## Why this is a new project
Projects 31, 37, 59, 60, 61, 72 and 80 already contain hardware-root-of-trust, secure execution, driver verification and self-evolving substrate concepts. Project 93 specializes these primitives into a distinct **DePIN economic-attestation layer**, including proof-of-physical-work, external-oracle corroboration, reward integrity and anti-gaming analysis.

## Source-derived foundation
The supplied report connects Zero-Trust hardware, Hardware Root of Trust, secure boot, remote attestation, secure elements, ARM TrustZone, RISC-V/Keystone, microkernel isolation and token incentives. It describes DePIN as networks where physical devices provide economically useful resources. fileciteturn522file7L301-L323

The source's Helium discussion illustrates the evolution from signal-based trust toward hardware-backed identity and external corroboration, including signed radio observations and external network records. fileciteturn522file13L548-L577

## Reference architecture
```text
HARDWARE ROOT OF TRUST
        ↓
SECURE BOOT
        ↓
MEASURED / VERIFIED RUNTIME
        ↓
REMOTE ATTESTATION
        ↓
DEVICE IDENTITY + KEY PROTECTION
        ↓
WORK MEASUREMENT
        ├── compute
        ├── network coverage
        ├── storage
        ├── sensing
        └── other physical resource
        ↓
EVIDENCE PACKAGE
        ↓
EXTERNAL CORROBORATION / ORACLE
        ↓
ANTI-GAMING ENGINE
        ↓
REWARD ELIGIBILITY
        ↓
AUDITABLE ECONOMIC RECORD
```

## Hardware trust chain
Candidate implementations may use:
- ARM TrustZone/TEE;
- RISC-V with PMP and Keystone-style enclaves;
- Open or auditable roots of trust where available;
- secure elements for private-key protection;
- measured/verified boot;
- remote attestation.

The source contrasts ARM's maturity and ecosystem availability with RISC-V's openness and auditability. fileciteturn520file9L383-L424

## Attestation object
```yaml
NodeAttestation:
  node_id:
  hardware_identity:
  boot_measurements: []
  firmware_measurements: []
  runtime_measurements: []
  software_manifest:
  secure_element_ref:
  attestation_signature:
  timestamp:
  freshness_nonce:
  verifier:
  status:
```

Attestation proves a bounded claim about a measured device/software state. It does not prove every external-world statement made by the node.

## Physical-work evidence
```yaml
WorkProof:
  node_id:
  resource_type:
  workload_or_service:
  local_measurements: []
  hardware_attestation_ref:
  temporal_window:
  location_evidence:
  external_oracle_refs: []
  anti_replay_data:
  confidence:
  reward_eligibility:
```

Reward eligibility requires a combination of evidence rather than a single easily spoofed signal.

## Anti-gaming model
Threat classes:
- cloned device identities;
- replayed measurements;
- spoofed location;
- simulated physical activity;
- colluding nodes;
- compromised host OS;
- oracle manipulation;
- reward farming;
- firmware substitution;
- key extraction;
- Sybil node creation.

Mitigations are evaluated experimentally. No mechanism is assumed secure merely because it is cryptographic.

## Economic control plane
The economic layer separates:

```text
MEASURED WORK
      ↓
VERIFIED EVIDENCE
      ↓
ELIGIBILITY
      ↓
REWARD FUNCTION
      ↓
SETTLEMENT
```

Token issuance is therefore downstream of verification. A token balance cannot itself become evidence that work occurred.

## Security architecture
- least-privilege node services;
- compartmentalized drivers;
- secure key storage;
- signed firmware and staged updates;
- remote attestation;
- revocation;
- replay protection;
- audit logs;
- independent verification for high-value rewards;
- deterministic emergency fallback.

## Regulatory/economic boundary
The supplied source discusses MiCA and financial/regulatory implications. Those claims remain source-derived research material. Any actual token issuance, custody, exchange activity or regulated service requires jurisdiction-specific legal review before deployment.

## Evaluation gates
1. Hardware identity verification.
2. Secure-boot measurement verification.
3. Remote-attestation correctness.
4. Key non-extractability testing.
5. Host-compromise containment.
6. Replay resistance.
7. Sybil resistance.
8. Physical-work spoofing resistance.
9. Oracle-correlation integrity.
10. Reward-function gaming tests.
11. Network partition/recovery tests.
12. Independent verifier reproduction.

## Integration
- Project 26/31 — trusted kernel and sovereign hardware.
- Project 37 — sovereign edge runtime.
- Project 59/60 — autonomous execution and AI Foundry.
- Project 61 — OmniCore hardware/runtime convergence.
- Project 72 — assurance and verification.
- Project 80 — controlled evolution of runtime and drivers.

## Hard invariants
1. Device identity is not economic entitlement.
2. Attestation is not proof of arbitrary external-world claims.
3. Token ownership is not proof of physical work.
4. Model output cannot authorize reward issuance.
5. Compromised host software must not expose hardware-protected private keys.
6. Reward-critical evidence must be replay-resistant and provenance-linked.
7. Security mechanisms require adversarial testing.
8. Economic claims require measured utility and anti-gaming analysis.
9. No financial/regulatory readiness is implied by architecture alone.

## Definition of Done
- reference node threat model;
- hardware trust-chain specification;
- attestation protocol prototype;
- physical-work evidence schema;
- anti-gaming test suite;
- external-oracle verification model;
- reward eligibility engine;
- revocation and incident-response workflow;
- reproducible security evaluation;
- independently verifiable economic evidence pipeline.
