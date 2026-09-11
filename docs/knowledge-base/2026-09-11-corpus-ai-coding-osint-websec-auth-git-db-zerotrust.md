# Corpus Audit — AI Coding, OSINT, Web Security, Git, SQL & Zero Trust

Date: 2026-09-11
Source type: 10 uploaded visual references
Decision: integrate into existing portfolio; no new numbered project

## 1. Corpus inventory

The batch contains ten distinct references:

1. AI coding-tool decision matrix: Cursor, GitHub Copilot, Windsurf, Claude Code; workflow, constraints and scale as selection dimensions.
2. Information-gathering/OSINT tool map: Maltego, theHarvester, Fierce, Photon, Recon-ng, Censys, Nmap, Nikto, Shodan.
3. JSON primer: key/value structure, API exchange, application configuration and structured data.
4. Git internals: objects, blobs, trees, commits, refs, snapshots, branches, merge, reset, stash, rebase, push/pull.
5. Free hacking-learning resources: TryHackMe, Hack The Box, PortSwigger, Hack This Site, Cybrary, Try2Hack, HackThis!, picoCTF, UltraEdit, Root Me.
6. Web security cheat sheet: SQLi, XSS, CSRF, SSRF; JWT/OAuth/MFA/RBAC; symmetric/asymmetric crypto, hashing, TLS; CORS/CSP/HSTS/cookies; input validation, parameterized SQL, allowlists, dependency audits and rate limiting.
7. Web authentication overview: sessions/cookies, tokens/JWT, SSO and OAuth-style authorization flows.
8. OSI vs TCP/IP plus defense-in-depth, segmentation, stateful firewall, proxy, IDS/IPS, NAT, VPN, TLS and split tunneling.
9. SQL cheat sheet: SELECT, filtering, joins, aggregation, clauses, dates, subqueries, CASE and query-performance interview concepts.
10. Zero Trust seven-pillar model: identity, devices, applications/data, network, data protection, visibility/analytics, automation/orchestration; explicit verification, least privilege and assume-breach principles.

## 2. Deduplication

No exact duplicate was detected inside this batch. Several references are intentionally overlapping: web/network security appears in multiple views, and Git/AI coding are represented both conceptually and operationally. These are retained as complementary evidence rather than treated as duplicates.

## 3. High-value synthesis

The strongest new architectural connection is a complete developer-agent security supply chain:

DISCOVER CAPABILITIES
→ SELECT TOOL/AGENT
→ AUTHENTICATE IDENTITY
→ AUTHORIZE ACTION
→ READ REPOSITORY STATE
→ PLAN CHANGE
→ EXECUTE IN SANDBOX/CONTROLLED RUNTIME
→ TEST
→ BUILD ARTIFACT
→ RECORD PROVENANCE
→ DEPLOY WITH STRATEGY
→ OBSERVE
→ VERIFY POSTCONDITION
→ PROMOTE / ROLLBACK

This directly reinforces the existing OBSERVE → PLAN → AUTHORIZE → ACT → READBACK → VERIFY doctrine.

## 4. AI coding-tool decision layer

The source frames tool choice as a decision problem rather than a popularity ranking. Useful dimensions are:

- workflow: IDE-native, existing GitHub stack, VS Code-centric, terminal/autonomous-agent;
- constraints: compliance, budget, credit efficiency, reasoning vs speed;
- scale: solo/prototype, team/large codebase, enterprise/regulated, complex multi-step work.

Portfolio implication: P100 should treat AI coding tools as interchangeable capability adapters with typed metadata, policy constraints, compatibility and evidence—not as hard-coded authorities.

The claims in the infographic (benchmarks, certifications, user counts, model versions and pricing) are not accepted as current facts without independent verification.

## 5. OSINT and security reconnaissance

The OSINT/tool map expands the existing security capability registry with distinct reconnaissance classes:

- graph/entity relationship discovery;
- passive collection and metadata harvesting;
- DNS/domain reconnaissance;
- web crawling;
- certificate/asset discovery;
- network/service discovery;
- web-server assessment.

Security invariant:

LOOKUP / RECON RESULT ≠ IDENTITY PROOF

Reconnaissance output must carry source, timestamp, collection method, confidence and scope. Active scanning must remain explicitly authorized and bounded to owned/authorized targets.

This reinforces P32's evidence separation and passive-first posture.

## 6. JSON as an agent protocol primitive

The JSON reference is basic but strategically relevant. In the portfolio, structured JSON should be treated as a typed interchange representation between planner, tool adapter, executor, verifier and registry layers.

Required distinction:

JSON validity ≠ semantic validity ≠ authorization.

A syntactically valid model response must still pass schema validation, policy validation, capability validation and postcondition verification before consequential execution.

## 7. Git object model as provenance substrate

The Git reference reinforces a critical repository-state model:

- blob = content object;
- tree = directory/snapshot structure;
- commit = immutable-ish snapshot plus metadata and parent links;
- branch = movable reference to a commit;
- merge = new commit with multiple parents;
- rebase = reconstructed history with new commit objects.

This is directly useful for P100 and the repository-wide evidence model. Agent decisions should bind to explicit commit/tree/blob identities where possible rather than to mutable filenames alone.

Security/provenance invariant:

WORKING DIRECTORY VIEW ≠ CANONICAL HISTORY

A consequential agent mutation should record base commit, changed paths, resulting commit/tree identity, tests, verification status and promotion decision.

## 8. Web security control plane

The batch provides a compact control taxonomy:

ATTACK SURFACE
→ AUTHN/AUTHZ
→ INPUT VALIDATION
→ TRANSPORT/HTTP SECURITY
→ CRYPTOGRAPHY
→ SECRET MANAGEMENT
→ DEPENDENCY SECURITY
→ RATE LIMITING
→ OBSERVABILITY
→ INCIDENT RESPONSE

Important controls include parameterized SQL, allowlists, secure cookies, CSP/HSTS, MFA/RBAC, dependency auditing and least privilege.

These should be represented as policy/check types rather than as a static checklist only.

## 9. Authentication model

The authentication visual distinguishes session/cookie state, bearer/token state, JWT, SSO and OAuth-style flows. For the portfolio this becomes a typed identity lifecycle:

IDENTITY → AUTHENTICATION → SESSION/TOKEN → AUTHORIZATION → EXPIRATION/REVOCATION → AUDIT

Critical invariant:

AUTHENTICATED ≠ AUTHORIZED

and:

TOKEN VALID ≠ ACTION ALLOWED

The authorization policy must be evaluated against subject, resource, operation, context, credential state and current policy—not merely the presence of a token.

## 10. Network and Zero Trust synthesis

The OSI/TCP-IP and Zero Trust references complement the existing zero-trust agent doctrine. The relevant architecture is layered defense with explicit trust boundaries:

IDENTITY
→ DEVICE
→ APPLICATION
→ DATA
→ NETWORK SEGMENT
→ OBSERVABILITY
→ AUTOMATION

Network controls include segmentation, firewall policy, proxy mediation, IDS/IPS, VPN and TLS. NAT is correctly framed as address translation rather than a security control by itself.

For agents, MCP/tool gateways should be treated similarly to network policy enforcement points: they expose capabilities, but authorization remains an independent policy decision.

## 11. SQL and database performance

The SQL references reinforce two separate concerns:

### Correctness
SELECT, WHERE, JOIN, GROUP BY, HAVING, aggregation, subqueries and CASE.

### Performance
Index selection, cardinality/selectivity, query plans, write amplification, stale/bloated indexes and workload-specific benchmarking.

This complements the previous database-indexing/TurboVec work. A database optimization claim should be evidence-backed by EXPLAIN/ANALYZE or equivalent measurements under a representative workload; a cheat sheet is not performance evidence.

## 12. DevSecOps integration

The batch closes several boundaries already present in P100:

AI coding agent
→ Git state
→ tests
→ CI/CD
→ security analysis
→ artifact
→ provenance
→ deployment
→ runtime observation
→ rollback.

Deployment strategies from the previous corpus (rolling, blue-green, canary) should be selected as policy-controlled promotion strategies with explicit rollback criteria, not as automatic defaults.

## 13. Project mapping

| Source theme | Primary project(s) | Action |
|---|---|---|
| AI coding decision matrix | P100, P117 | capability/provider selection matrix |
| OSINT reconnaissance | P32 | extend reconnaissance capability taxonomy and evidence contract |
| JSON/structured protocol | P100, P119 | schema-first tool/agent messages |
| Git internals | P100, P117 | immutable provenance and state identity |
| security learning resources | P32, P100 | training/evaluation corpus; authorized labs only |
| web security controls | P100, P119 | policy/check catalog |
| authentication | P100, P119 | typed identity/authz lifecycle |
| network security / OSI | P100, P119 | layered policy and trust-boundary model |
| SQL | P100 + database substrate | query correctness/performance verification |
| Zero Trust | P32, P100, P119 | explicit verification, least privilege, assume-breach |

## 14. New-project decision

No new numbered project is warranted.

The material strengthens existing boundaries rather than creating an independent system. The highest-value action is cross-project normalization of capability, identity, policy, provenance and verification contracts.

## 15. Evidence boundaries

- infographic ranking ≠ benchmark evidence;
- advertised product feature ≠ verified current capability;
- authentication ≠ authorization;
- token possession ≠ permission;
- recon finding ≠ identity proof;
- valid JSON ≠ trusted instruction;
- Git working-tree state ≠ immutable provenance;
- successful SQL execution ≠ optimal query;
- TLS/VPN ≠ complete Zero Trust;
- security tool availability ≠ authorization to target a system.

## 16. Required follow-up backlog

1. Add typed AI coding-tool selection metadata to P100/P117.
2. Add OSINT collection-method and authorization metadata to P32.
3. Standardize JSON schemas for agent/tool observations and decisions.
4. Bind repository mutations to commit/tree identities and verification records.
5. Add web-auth lifecycle states to the authorization model.
6. Add network-layer and Zero Trust controls to policy evaluation.
7. Add SQL query-plan evidence to database optimization gates.
8. Keep all external product/model/version claims lifecycle-aware and independently verified.
