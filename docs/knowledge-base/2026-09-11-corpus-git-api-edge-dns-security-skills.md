# Knowledge Corpus — 2026-09-11 — Git / API Gateway / Edge / DNS / Security / AI Skills

## Scope

Ten supplied visual references were reviewed as one engineering corpus. They cover Git internals, API Gateway use cases, Nginx, cybersecurity practice platforms, AI skills, security tooling, network ports and DNS. They are treated as reference/teaching artifacts, not authoritative current registries.

## Findings

### Git internals
The source explains `.git`, blobs, trees, commits, parent links, refs/branches, checkout, log, merge, reset, stash, rebase and push/pull as an object-and-reference model.

Engineering value: strengthens Git-as-provenance, commit/tree/blob/ref lineage, rollback reasoning and the distinction between repository state and the working-tree view.

Normalization: the image presents SHA-1 as universal; architecture must record the actual Git object format rather than assume SHA-1. `stash` is temporary repository state, not literally a normal branch. Checkout/worktree behavior is more nuanced than the simplified diagram.

### API Gateway
The source identifies rate limiting, authentication, request routing, response caching, load balancing and protocol translation. These become separately authorizable capabilities with explicit retry, idempotency and postcondition semantics.

### Nginx / edge
The source models an edge entry point for static files, reverse proxying, redirects, TLS, load balancing, caching, rate limiting, compression, security headers, logs and Kubernetes ingress-style routing. The edge is a policy point, not the sole security boundary.

### Cybersecurity practice
TryHackMe, Hack The Box, PortSwigger, Hack This Site, Cybrary, Try2Hack, HackThis, picoCTF, UltraEdit and Root-Me are presented as practice resources. They strengthen the learning/validation layer; access to a lab does not authorize testing unrelated real systems.

### AI skills
Programming, mathematics, data structures, data wrangling, analysis, ML, evaluation/deployment, NLP, computer vision, deep learning, reinforcement learning, ethics/governance and soft skills form a useful skill ontology for P16. Skills should carry prerequisites, compatibility, lifecycle, evidence and verification state.

### Security tools
The sources group networking, application, cloud and incident-response tools, including Wireshark, Nmap, Snort, Burp Suite, OWASP ZAP, Checkmarx, Veracode and MISP. They are capabilities producing observations/evidence, not authority. Dual-use tooling requires target scope, authorization and audit correlation.

### Network ports
Useful associations include HTTP/80, HTTPS/443, SSH/22, FTP/21, MySQL/3306, Kubernetes API/6443, MongoDB/27017, Nginx/80/443, Grafana/3000, Prometheus/9090, Kafka/9092, Redis/6379, RDP/3389 and Elasticsearch/9200. A conventional port does not prove the running service, authorization or exposure intent. The image contains a duplicated/questionable RDP/9200 row and is non-authoritative.

### DNS
The source models browser/OS cache → recursive resolver → root → TLD → authoritative server, plus forward/reverse lookup and A/AAAA/CNAME/MX/NS/PTR/TXT records, caching, redundancy, hierarchy and DNSSEC. DNS answer ≠ service identity proof.

## Unified architecture

```text
REPOSITORY / GIT OBJECT GRAPH
        ↓
DNS / NETWORK / EDGE
        ↓
API GATEWAY / REVERSE PROXY
        ↓
AUTHN → AUTHZ → POLICY / SCOPE / BUDGET
        ↓
TOOL / SERVICE EXECUTION
        ↓
OBSERVATION / TELEMETRY
        ↓
SECURITY + POSTCONDITION VERIFICATION
        ↓
ARTIFACT / DEPLOYMENT PROVENANCE
        ↓
DURABLE MEMORY / AUDIT
```

## Canonical contracts

```yaml
GitState:
  repository:
  object_format:
  commit:
  parents: []
  tree:
  refs: []
  index_state:
  worktree_state:
  remote_refs: []
  captured_at:
  verification:

ApiGatewayOperation:
  operation_id:
  version:
  route:
  method:
  authn:
  authz:
  rate_limit:
  cache_policy:
  routing_policy:
  load_balance_policy:
  protocol_translation:
  timeout:
  retry_policy:
  idempotency:
  postcondition:

NetworkEndpointObservation:
  host:
  transport:
  port:
  protocol_guess:
  observed_service:
  banner:
  tls_identity:
  exposure_scope:
  captured_at:
  evidence:
  confidence:

DnsObservation:
  qname:
  record_type:
  resolver:
  answers: []
  ttl:
  dnssec_state:
  captured_at:
  provenance:

SecurityCapability:
  capability_id:
  target_scope:
  authorization:
  tool:
  evidence:
  risk:
  audit_id:
  verification_state:

Skill:
  skill_id:
  domain:
  prerequisites: []
  compatible_tools: []
  risk:
  lifecycle:
  evidence:
  verification_state:
```

## Security invariants

- commit lineage ≠ code safety;
- branch/ref ≠ authorization;
- API gateway authentication ≠ downstream authorization;
- open port ≠ identified service;
- DNS resolution ≠ service identity proof;
- scanner output ≠ confirmed vulnerability without evidence/triage;
- skill installed ≠ authority;
- training-lab access ≠ permission to test unrelated systems;
- infographic ≠ current production registry;
- generated/mutated state ≠ verified state.

## Project mapping

| Project | Impact | Integration |
|---|---|---|
| P100 | HIGH | Git provenance, gateway, Nginx/edge, DNS, endpoint observations, security adapters |
| P40 | HIGH | capability broker, network/egress policy, gateway/edge enforcement |
| P28 | HIGH | security testing and API verification |
| P37 | MEDIUM-HIGH | DNS/network/edge substrate across local/edge/cloud |
| P102 | MEDIUM | enterprise gateway/mTLS/edge/observability |
| P114 | MEDIUM | Git/artifact provenance and evidence promotion |
| P16 | MEDIUM-HIGH | AI skill ontology and cybersecurity learning resources |
| P33 | MEDIUM | secure web/API defaults |

## Genesis decision

**NO NEW NUMBERED PROJECT.** The corpus extends existing repository, control-plane, cloud/edge, verified-code, learning and security lineages.

## Verification backlog

1. P100: represent Git object format, refs, worktree/index state and graph transformations.
2. P100/P40: API gateway rate-limit/authn/authz/cache/routing/retry/idempotency/postcondition contracts.
3. P100/P37: DNS observations with TTL, resolver and DNSSEC/provenance state.
4. P100/P40: endpoint observations without service inference from ports alone.
5. P100/P28: security-tool authorization scope, evidence provenance and retest state.
6. P16: prerequisite/compatibility/lifecycle metadata for AI skills and security-learning resources.
