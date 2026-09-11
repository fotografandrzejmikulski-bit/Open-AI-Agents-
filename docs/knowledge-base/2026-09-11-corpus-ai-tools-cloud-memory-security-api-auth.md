# Knowledge Corpus — 2026-09-11 — AI Tools / Cloud / Memory / Security / API / Identity

## Scope

Ten supplied visual references were reviewed as one engineering corpus. The sources are treated as capability maps and architectural teaching artifacts, not as authoritative registries of current products, service inventories or security standards.

## Source audit

### 1. AI productivity/tool landscape
The first reference groups AI products into voice-to-text, text-to-speech, presentations, chatbots, design, writing, image generation, AI detection, website creation, UI/UX, meetings, blogging, marketing, video, ideation and automation.

Engineering value:
- confirms the need for a typed, provider-neutral capability catalog;
- reinforces separation of capability class from concrete provider;
- supports bulk provider health/testing and compatibility metadata already emerging in P100;
- generic tool lists remain discovery signals because names, pricing, availability and capabilities change.

### 2. AWS services map
The second reference groups cloud primitives into compute, storage, databases, networking, monitoring, security, developer tools, global infrastructure and analytics.

Engineering value:
- gives a compact substrate taxonomy for capability normalization;
- reinforces the edge/local/cloud continuum in P37/P40;
- enables provider-neutral contracts such as `compute`, `object_storage`, `relational_db`, `kv_db`, `container`, `network`, `secret`, `observability`, `build`, `deploy`, `analytics`;
- the pictured service inventory is not treated as a current AWS catalog.

### 3. RAM vs ROM
The third reference presents volatile/temporary/read-write RAM versus non-volatile/persistent/firmware-oriented ROM.

Engineering value:
- useful as an architectural analogy for ephemeral execution state versus durable state;
- maps directly to agent context, session state, caches and working memory versus persistent memory, configuration, provenance and artifact metadata;
- the analogy must not be copied literally into software because modern persistent storage does not have the same semantics as historical hardware ROM.

### 4. Open-source security tools
The fourth reference covers network discovery, packet analysis, exploitation testing, IDS/IPS, host intrusion detection, vulnerability assessment, password auditing, wireless security, antivirus, network monitoring, malware classification, threat intelligence, forensics, Unix auditing, reverse engineering and web application security scanning.

Engineering value:
- provides a defensive security capability taxonomy;
- supports typed security-tool adapters in P100/P28/P40;
- reinforces that security findings are evidence objects which require provenance, triage and re-analysis;
- dual-use tools should be exposed behind policy and scope boundaries rather than as unrestricted agent primitives.

### 5. API design best practices
The fifth reference presents clear resource names, standard methods, idempotency, versioning, correct HTTP status codes, pagination, filtering/sorting, authentication, rate limiting, caching, documentation and pragmatic REST.

Engineering value:
- directly strengthens P100/P40 capability contracts;
- makes idempotency, pagination semantics, error contracts and version compatibility first-class;
- supports capability schemas that define side effects, retry safety and verification.

### 6. Free developer resources
The sixth reference lists programming education websites, apps, video channels, playgrounds, practice platforms and cheat sheets.

Engineering value:
- discovery/learning corpus only;
- useful as an external resource registry category;
- no production architecture changes by itself.

### 7. Web authentication overview
The seventh reference contrasts username/password web authentication, server sessions/cookies, JWT-like tokens, SSO and several OAuth-style authorization flows.

Engineering value:
- reinforces identity lifecycle as a distinct control plane;
- supports short-lived access tokens, refresh/rotation, delegated authorization, SSO and mobile/native-app boundaries;
- legacy-looking flow labels in the image are retained as source terminology and are not promoted to normative policy.

### 8. Network-security layer cheat sheet
The eighth reference maps representative security threats to OSI/network layers: application, presentation, session, transport, network, data-link and physical.

Engineering value:
- useful for threat-model coverage matrices;
- helps classify telemetry and controls by layer;
- reinforces defense-in-depth rather than a single security scanner.

### 9. Web security cheat sheet
The ninth reference groups top attacks, authentication/authorization, encryption, HTTP security, input validation and operational best practices.

Engineering value:
- directly maps to a default security gate for generated applications;
- supplies a compact checklist spanning injection, XSS, CSRF, SSRF, JWT/OAuth/MFA/RBAC, TLS, CSP/HSTS/secure cookies, validation, allowlists, dependency auditing and rate limiting.

### 10. Authentication and authorization concepts
The tenth reference enumerates AuthN/AuthZ, sessions/tokens, JWT, access/refresh tokens, OAuth2, OIDC, scopes, RBAC, ABAC, SSO, MFA, magic links, social login, stateful/stateless auth, cookies/localStorage, CSRF, PKCE, client credentials, token rotation, 401/403 distinction, email verification and audit logging.

Engineering value:
- creates a reusable identity vocabulary across agent, API, web, mobile and cloud projects;
- separates who the principal is from what the principal is allowed to do;
- reinforces auditability and revocable, short-lived credentials.

## Unified architecture derived from the corpus

```text
DISCOVERY
   ↓
CAPABILITY REGISTRY
   ↓
PROVIDER / SUBSTRATE ADAPTER
   ↓
IDENTITY + AUTHN/AUTHZ
   ↓
POLICY / SCOPE / BUDGET
   ↓
API / TOOL CONTRACT
   ↓
EXECUTION
   ↓
OBSERVATION / TELEMETRY
   ↓
POSTCONDITION / SECURITY VERIFICATION
   ↓
PROVENANCE / AUDIT
   ↓
DURABLE MEMORY / ARTIFACT STATE
```

## Canonical contracts

```yaml
Identity:
  principal:
  authentication_method:
  issuer:
  audience:
  scopes: []
  roles: []
  attributes: {}
  issued_at:
  expires_at:
  revocation_state:
  audit_id:

ApiOperation:
  id:
  version:
  method:
  resource:
  inputs:
  outputs:
  side_effects:
  idempotency:
  pagination:
  rate_limit:
  authn:
  authz:
  error_contract:
  verification:
  provenance:

SecurityFinding:
  id:
  tool:
  target:
  category:
  evidence:
  captured_at:
  severity:
  confidence:
  provenance:
  status: observed|triaged|remediated|retested|dismissed

MemoryTier:
  class: ephemeral|durable
  medium:
  version:
  retention:
  provenance:
  mutability:
  recovery:
```

## Security invariants

- tool listing ≠ current capability availability;
- cloud service name ≠ implementation contract;
- authentication ≠ authorization;
- token possession ≠ unrestricted authority;
- API success response ≠ verified state;
- security scanner output ≠ confirmed vulnerability without triage/evidence;
- memory cache ≠ durable identity;
- ephemeral context ≠ permanent memory;
- static cheat sheet ≠ current security standard;
- external resource list ≠ validated production dependency.

## Project mapping

| Project | Impact | Reason |
|---|---|---|
| P100 | HIGH | provider/capability registry, security gate, API contracts, identity adapters |
| P40 | HIGH | typed capability broker, credential boundary, network/security policy, execution verification |
| P28 | HIGH | secure code generation, API/security verification and promotion gates |
| P37 | MEDIUM-HIGH | provider-neutral local/edge/cloud substrate taxonomy |
| P39 | MEDIUM | Alibaba Cloud remains a concrete substrate; AWS becomes an external comparison, not a scope expansion |
| P114 | MEDIUM | ephemeral vs durable memory hierarchy and provenance-aware memory state |
| P33 | MEDIUM | secure defaults for generated apps, APIs, auth and observability |
| P16 | MEDIUM | learning/discovery registry and reusable prompt/skill knowledge |

## Project genesis decision

**NO NEW NUMBERED PROJECT.**

The corpus strengthens existing control-plane, verified-code, cloud-fabric, memory and application-builder lineages. A separate project for generic AI tools, AWS services, basic security tools or basic authentication would duplicate existing boundaries.

## Verification backlog

1. P100: provider/capability registry should distinguish `CONNECTED`, `HEALTHY`, `AUTHORIZED`, `AVAILABLE`, `ALLOWED` and support bulk test results.
2. P100/P40: API operations require explicit idempotency/retry semantics and postcondition verification.
3. P28: generated-app security gate should cover the source checklist as a baseline, with evidence per control.
4. P40/P100: identity objects need issuer/audience/scope/expiry/revocation/audit correlation.
5. P37/P39: build a substrate-neutral matrix instead of encoding a single cloud vendor's service names into agent policy.
6. P114: model ephemeral, cached and durable memory separately and preserve provenance across promotion.
7. Security adapters: never expose dual-use tooling without capability scoping, target scoping, audit correlation and explicit policy.
