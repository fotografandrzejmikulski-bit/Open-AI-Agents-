# Project 115 — OmniPrivacy Identity Relay & Disposable Communications Fabric MAX

## Status
PROPOSED → ARCHITECTURE BASELINE

## Mission
Build a provider-neutral privacy and identity-separation fabric for legitimate use of alternate phone numbers, VoIP identities, email masks and disposable communication endpoints while preserving authoritative ownership, consent, lifecycle control, provenance and abuse-resistant policy boundaries.

## Distinct boundary
- **P95 — Omni-Entity Sovereign Network & Cyber-Resilience Fabric** owns resilient sovereign connectivity, identity/trust lifecycle and infrastructure continuity; P115 owns user-facing communication-identity abstraction.
- **P112 — OmniCompanion Sovereign Edge & Cognitive Relationship Platform** may consume P115 aliases for companion privacy, but P115 owns the communication identity lifecycle.
- **P111/P100** may orchestrate communication providers through authorized connectors; they do not own the identity-relay product boundary.
- **P108** owns adversarial validation of the boundary, not the relay service itself.

## Core capabilities
1. Alternate phone-number profiles.
2. Email alias/mask profiles.
3. VoIP/SIP identity connectors.
4. Provider-neutral routing abstraction.
5. Lifecycle states: proposed → active → paused → expiring → revoked → destroyed.
6. User-controlled activation windows and retention.
7. Separation of personal, professional, project and public-facing identities.
8. Inbound message/call routing with authoritative delivery state.
9. Consent and authorization ledger.
10. Provenance for provider, number/address, acquisition time and lifecycle events.
11. Privacy-preserving local policy evaluation where feasible.
12. Export/deletion and revocation controls.
13. Defensive abuse-risk scoring and anomaly telemetry.

## Canonical architecture
```text
USER / POLICY OWNER
        ↓
IDENTITY INTENT
        ↓
IDENTITY PROFILE MANAGER
 ├── PHONE ALIAS
 ├── EMAIL MASK
 ├── VOIP / SIP IDENTITY
 └── PROJECT / BUSINESS IDENTITY
        ↓
PROVIDER ADAPTER LAYER
 ├── VIRTUAL NUMBER PROVIDERS
 ├── VOIP / CLOUD PBX
 ├── EMAIL RELAY
 └── LOCAL / SELF-HOSTED ENDPOINTS
        ↓
ROUTING + DELIVERY FABRIC
        ↓
POLICY / CONSENT / RISK GATE
        ↓
AUTHORITATIVE STATE
        ↓
AUDIT / EVIDENCE / USER CONTROL
```

## Identity model
Each communication identity is a versioned object containing:
- stable internal identity ID;
- external provider identifier where applicable;
- channel type;
- owner/tenant;
- purpose;
- consent scope;
- activation window;
- retention policy;
- provider metadata;
- routing rules;
- lifecycle state;
- provenance;
- audit history;
- revocation state.

The external phone number or email address is not the authoritative identity. The authoritative identity is the policy-controlled internal object and its provenance-bearing state.

## Privacy principles
- Minimize disclosure of the primary personal address/number.
- Prefer aliases over duplication of personal identity records.
- Keep sensitive routing metadata local where technically feasible.
- Make retention and deletion explicit.
- Do not infer anonymity from use of an alias.
- Do not treat disposable channels as suitable for critical identity verification unless the provider and policy explicitly support that use.

## Provider classes
### Persistent secondary number
Suitable for long-lived separation of personal/business/project communications.

### Temporary number
Suitable for bounded interactions such as classifieds or short-lived public contact where the user can revoke the identity afterwards.

### Cloud PBX / business VoIP
Suitable for teams, IVR, routing, call recording and analytics subject to applicable consent and legal requirements.

### Email relay/mask
Suitable for reducing exposure of a primary mailbox and controlling forwarding/spam/tracker exposure.

### Disposable mailbox
Suitable only for low-trust, low-value correspondence where loss of the mailbox is acceptable.

## Security and abuse boundary
P115 must not implement:
- caller-ID spoofing;
- fraud/scam calling;
- bulk account creation or activation;
- CAPTCHA or platform anti-abuse bypass;
- credential/session-token extraction;
- evasion of identity verification;
- covert surveillance.

These behaviors may appear as adversarial test cases in P108 to validate detection and policy enforcement.

## Verification plan
1. Provider adapter contract conformance.
2. Identity lifecycle state-machine tests.
3. Revocation propagation tests.
4. Routing correctness and stale-state prevention.
5. Consent boundary tests.
6. Data minimization and deletion tests.
7. Provider failure and number-expiry simulation.
8. Duplicate identity collision tests.
9. Audit/provenance completeness.
10. Privacy leakage tests.
11. Caller-ID and verification-abuse detection regression.
12. Multi-tenant isolation.
13. Recovery and migration tests.
14. Offline/local-policy degradation tests where supported.

## Lineage
P37, P54, P61, P72, P95, P100, P105, P108, P111, P112.

## Primary source cluster
2nr; GetCode; MoreMins; Surfshark Alternative Number/ID material; Firefox Relay; DuckDuckGo Email Protection; YOPmail; 10 Minute Mail; Ringostat; Zadarma/VoIP ecosystem; GitHub VoIP topic; defensive analysis of temporary-number/verification market repositories.
