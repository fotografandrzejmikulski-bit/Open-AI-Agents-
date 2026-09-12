# P115 Extension — Disposable Email, Persistent Masks & Platform Alias Capability Model

## Purpose
Extend P115 with a provider-neutral capability model derived from current 10 Minute Mail, Firefox Relay and Apple Hide My Email behavior.

P115 already owns email masks and disposable communication endpoints. This extension makes their lifecycle semantics explicit rather than treating all privacy email products as equivalent.

## Capability classes

### 1. Disposable mailbox
Properties:
- short TTL;
- temporary inbox is the endpoint;
- automatic expiration;
- message deletion at expiration;
- typically receive-first/receive-only;
- no persistent identity relationship required.

Canonical examples: 10 Minute Mail-style services.

### 2. Persistent forwarding mask
Properties:
- stable masked address;
- forwards to a real mailbox;
- user-controlled blocking/revocation;
- optional anonymous replies;
- optional tracker removal and promotional filtering;
- authenticated account/lifecycle management.

Canonical example: Firefox Relay.

### 3. Platform-integrated alias
Properties:
- random address generated inside an ecosystem account;
- forwards to the user's personal mailbox;
- integrated into browser, mail and supported application flows;
- persistent until deactivated/deleted;
- strong platform binding.

Canonical example: Apple Hide My Email.

## Canonical capability schema
```text
email_identity
 ├── identity_id
 ├── provider
 ├── endpoint
 ├── mode: disposable | mask | platform_alias
 ├── owner
 ├── purpose
 ├── ttl
 ├── forwarding_target
 ├── send_policy
 ├── retention_policy
 ├── revocation_policy
 ├── account_dependency
 ├── platform_binding
 ├── attachment_policy
 ├── tracker_policy
 ├── promotional_filter_policy
 ├── provenance
 └── audit_history
```

## Lifecycle extension
`PROPOSED → PROVISIONING → ACTIVE → PAUSED → EXPIRING → REVOKED → DESTROYED`

Disposable mailboxes may transition automatically from `ACTIVE → EXPIRING → DESTROYED` based on TTL. Persistent masks and platform aliases generally remain `ACTIVE` until explicitly blocked/deactivated/deleted or provider lifecycle changes occur.

## Routing model
```text
USER INTENT
    ↓
IDENTITY PROFILE
    ↓
CAPABILITY MATCH
    ↓
PROVIDER ADAPTER
    ↓
PROVISION / ACTIVATE
    ↓
INBOUND ROUTING
    ↓
CONTENT SANITIZATION / POLICY
    ↓
USER MAILBOX
```

The external email address is never the authoritative identity. P115's internal identity object remains authoritative for lifecycle, consent, routing and provenance.

## Provider-neutral comparison contract
Every adapter should report:
- TTL semantics;
- whether extension is possible;
- whether forwarding exists;
- whether sending/replying exists;
- whether an account is required;
- retention behavior;
- deletion/revocation behavior;
- attachment constraints;
- tracker handling;
- promotional filtering;
- geographic/account availability;
- provider policy restrictions.

## Product design consequence
The user-facing P115 experience should offer an intent selector rather than a generic "temporary email" button:

`ONE-TIME / DISAPPEARING`
`LONG-TERM MASK`
`PLATFORM-BOUND ALIAS`

The system then selects providers whose actual capabilities satisfy the requested semantics.

## Verification requirements
Current provider features are live metadata. The capability registry must be refreshed before routing. Provider claims about privacy, logging, storage, anonymity or deletion must remain source-derived unless independently audited.

## Abuse boundary
This extension does not authorize:
- identity-verification bypass;
- bulk account creation;
- spam campaigns;
- fraud;
- evasion of provider anti-abuse controls;
- credential recovery abuse.

Disposable or masked email is a privacy mechanism, not an authorization bypass.

## Integration
- P115 owns the identity lifecycle.
- P100 owns capability/policy orchestration where agents invoke providers.
- P108 can adversarially test lifecycle, leakage and abuse boundaries.
- P114 may provide provenance/semantic memory infrastructure.
