# P28 Extension — API / Security / Identity Verification Gate

## Parent

**P28 — OmniCore AI Foundry: Verified Code Generation MAX**

## Trigger

Visual corpus on API design, web authentication, network/web security, open-source security tooling and cloud control surfaces.

## Verification expansion

P28's code-verification boundary is extended from syntax/build/test correctness to an explicit application security and identity contract:

```text
SPEC
 ↓
CODE
 ↓
TYPE / PARSE
 ↓
BUILD
 ↓
UNIT / INTEGRATION TEST
 ↓
API CONTRACT TEST
 ↓
AUTHN / AUTHZ TEST
 ↓
SECURITY ANALYSIS
 ↓
DEPENDENCY / SUPPLY-CHAIN CHECK
 ↓
ARTIFACT INTEGRITY
 ↓
RUNTIME READBACK
```

## API verification contract

```yaml
ApiVerification:
  resource_model:
  method_semantics:
  schema_compatibility:
  version_policy:
  idempotency:
  pagination:
  filtering:
  error_contract:
  rate_limit:
  cache_policy:
  authn:
  authz:
  postcondition:
```

## Identity test matrix

Generated services should test, where applicable:

- unauthenticated access is rejected;
- authenticated but unauthorized access is rejected;
- scope/role/attribute restrictions are enforced;
- token audience and issuer are checked;
- access-token expiry is respected;
- refresh/rotation behavior is bounded;
- PKCE/native-app flows preserve the intended verifier boundary;
- CSRF protections match cookie/session semantics;
- secrets are absent from client bundles and logs;
- audit events are emitted for security-relevant changes.

## Security-analysis contract

Security tools are plugged into P28 as evidence producers:

```yaml
SecurityCheck:
  tool:
  target:
  policy:
  finding:
  evidence_ref:
  severity:
  confidence:
  remediation:
  retest:
```

Rule:

`FINDING != VERIFIED EXPLOITABILITY`

and:

`VERIFIED FINDING != AUTOMATIC PATCH AUTHORITY`

## Threat model coverage

Baseline classes from the corpus:

- injection;
- XSS;
- CSRF;
- SSRF;
- broken authentication/authorization;
- insecure token handling;
- weak transport/security headers;
- unsafe file/input handling;
- dependency vulnerabilities;
- brute-force/abuse exposure;
- network-layer exposure.

## Promotion gate

No generated application is promoted solely because compilation and unit tests pass.

Minimum production-oriented gate:

`BUILD + TEST + API CONTRACT + AUTH + SECURITY + DEPENDENCY + ARTIFACT + DEPLOYMENT + READBACK`

## Status

**ARCHITECTURE ENHANCED — IMPLEMENTATION NOT YET VERIFIED**
