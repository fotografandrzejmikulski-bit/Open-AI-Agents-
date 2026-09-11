# Knowledge Corpus — 2026-09-11 — AI Business / DevSecOps / Serverless / Network / Database

## Scope

Ten supplied visual references were reviewed as one engineering corpus. One developer-tools image is duplicated; it is retained as corroborating source material rather than counted as a separate capability surface.

The corpus covers:
- AI tools for business;
- common cyber-attack patterns;
- developer tooling and AI-assisted development;
- an AI-engineer learning path;
- DevOps fundamentals;
- serverless/AWS Lambda execution;
- cybersecurity tooling;
- network-security layers and threats;
- database indexing.

The images are teaching/reference artifacts. Tool rankings, product availability, exact service behavior, security claims, and version-specific details must not be promoted to current production truth without independent verification.

## 1. AI tools for business

The business-tool map groups capabilities into presentation, chatbots, email assistance, coding, spreadsheets, image generation, workflow automation, meeting notes, scheduling and writing generation.

### Engineering value
- strengthens the provider/skill/capability registry already present in P100/P16;
- reinforces capability-first routing instead of vendor-first routing;
- supports business workflow decomposition into atomic capabilities;
- supports tool substitution when a provider is unavailable or disallowed;
- provides a useful taxonomy for evaluating connected AI providers.

### Required normalization
A visual list of products is not an authorization list. A connected provider, installed integration, or advertised capability does not imply that a specific operation is authorized.

## 2. Cyber-attacks explained

The reference covers phishing, ransomware, man-in-the-middle, SQL injection, XSS and zero-day exploitation as simplified attack flows.

### Engineering value
- strengthens P28 verified-code/security testing;
- maps attack classes to preventative controls and verification tests;
- supports threat-model generation from application/network architecture;
- reinforces security-lab boundaries and authorized-target scope;
- connects detection, mitigation, retest and evidence provenance.

### Canonical security model

```text
THREAT CLASS
  ↓
ATTACK SURFACE
  ↓
PRECONDITION / TRUST ASSUMPTION
  ↓
CONTROL
  ↓
DETECTION
  ↓
EVIDENCE
  ↓
REMEDIATION
  ↓
RETEST
  ↓
VERIFIED STATE
```

The diagrams are conceptual. They do not constitute operational exploit instructions and should not be treated as proof that a specific implementation is vulnerable.

## 3. Developer tools

The developer-tool reference groups:
- editors/IDEs: VS Code, IntelliJ IDEA, PyCharm, Eclipse, Cursor;
- version control: Git, GitHub, GitLab, Bitbucket, AWS CodeCommit;
- testing: JUnit, Selenium, Cypress, Playwright;
- CI/CD: Jenkins, CircleCI, GitHub Actions, CodePipeline, Travis CI;
- containers: Docker, Kubernetes, Podman, containerd, Rancher;
- project management: Jira, Trello, Asana, ClickUp, Notion;
- API testing: Postman, Swagger, Insomnia, Hoppscotch;
- AI development: ChatGPT, Claude Code, Copilot, Cursor, Qodo.

### Engineering value
This extends the existing development control plane into a typed toolchain graph:

```text
IDE / AGENT
  ↓
SOURCE CONTROL
  ↓
BUILD / TEST
  ↓
CI/CD
  ↓
ARTIFACT
  ↓
CONTAINER / RUNTIME
  ↓
OBSERVABILITY
  ↓
SECURITY / PROVENANCE
```

Every tool edge needs lifecycle, compatibility, authorization and evidence metadata.

## 4. AI engineer learning path

The reference proposes a progression through:
1. Python foundations;
2. mathematics/statistics;
3. machine-learning algorithms;
4. deep learning;
5. NLP;
6. transformers/LLM architectures;
7. fine-tuning/custom training;
8. LangChain;
9. LangGraph/RAG;
10. MCP and agentic systems.

### Engineering value
- strengthens P16 skill ontology;
- connects prerequisites to projects and tools;
- supports competency-aware agent routing;
- connects learning state to evidence rather than self-reported completion;
- reinforces the repository's model → system → verification progression.

## 5. DevOps fundamentals

The reference covers CI/CD, pipelines, artifacts, IaC, immutable infrastructure, blue-green and canary deployment, rollback, Git, secrets/configuration management, monitoring, alerting, logging, containers, orchestration, service discovery, load balancing, reverse proxy, scaling, auto-scaling, failover, SLI/SLO/SLA and chaos engineering.

### Engineering value
This materially strengthens P100's release-assurance architecture and P37's infrastructure substrate.

Critical lifecycle:

```text
COMMIT
 → BUILD
 → TEST
 → SECURITY CHECKS
 → ARTIFACT
 → DEPLOY
 → READBACK
 → HEALTH / SLO CHECK
 → PROMOTE or ROLLBACK
```

Deployment strategy is itself policy-controlled state, not merely an implementation detail.

## 6. Serverless / AWS Lambda

The reference models function packaging, triggers, execution environments, cold starts, runtime initialization, handler execution, resource limits, external service access, response return, warm reuse, horizontal scale, isolation, monitoring, retries and usage-based billing.

### Engineering value
- strengthens P100/P40 serverless execution adapters;
- adds event-driven execution as a first-class capability;
- reinforces ephemeral runtime and cold-start state;
- requires explicit trigger identity and downstream authorization;
- supports cost/budget controls as execution policy.

Canonical abstraction:

```text
EVENT
 ↓
TRIGGER POLICY
 ↓
AUTHORIZED FUNCTION
 ↓
ISOLATED EXECUTION ENVIRONMENT
 ↓
DEPENDENCY / EGRESS POLICY
 ↓
RESULT
 ↓
POSTCONDITION
 ↓
TELEMETRY / PROVENANCE
```

The image contains simplified provider-specific limits and behavior. Those values must be verified against current provider documentation before implementation.

## 7. Cybersecurity tools

The reference highlights Nmap, Metasploit, Burp Suite, Aircrack-ng, John the Ripper, SQLMap, Maltego, Nikto, BeEF and Empire.

### Engineering value
- strengthens P28 security capability adapters;
- extends P100 security-toolchain metadata;
- supports defensive validation in explicitly authorized environments;
- enables capability classification by discovery, web testing, exploitation simulation, credential auditing and OSINT/relationship analysis.

### Safety contract

```yaml
SecurityToolInvocation:
  tool:
  target_scope:
  authorization:
  operation:
  safety_profile:
  rate_limit:
  audit_id:
  evidence:
  verification_state:
```

Tool availability never equals authorization. A security scanner or exploitation framework must remain bounded by target scope, policy and audit correlation.

## 8. Network security

The reference maps security concerns across the OSI layers:
- application;
- presentation;
- session;
- transport;
- network;
- data link;
- physical.

It associates representative threats including SQL injection/XSS/DDoS, encoding/TLS issues, session attacks, UDP/SYN floods, IP spoofing, routing manipulation, ARP/MAC spoofing, switch flooding, eavesdropping and physical tampering.

### Engineering value
- strengthens layered threat modeling;
- provides a control-to-layer taxonomy for P28/P37/P100;
- supports network observation schemas and defense-in-depth verification;
- prevents collapsing application, transport and physical security into one generic 'network security' label.

The OSI mapping is pedagogical; modern systems frequently cross or abstract multiple layers.

## 9. Database indexing

The reference covers primary, secondary, composite and unique indexes; B-tree/B+ tree/hash/full-text structures; clustered/non-clustered and covering indexes; left-prefix, cardinality, range-stop and selectivity rules; cases where indexing is counterproductive; partial indexes; query-plan analysis; and index bloat.

### Engineering value
- materially strengthens P114 memory/data substrate;
- supports query-performance evidence and index lifecycle metadata;
- connects database design to workload-aware verification;
- complements vector-index work by separating relational query indexing from vector retrieval.

Canonical database-performance loop:

```text
QUERY / WORKLOAD
 ↓
EXPLAIN / PLAN
 ↓
INDEX HYPOTHESIS
 ↓
BENCHMARK
 ↓
WRITE / STORAGE COST CHECK
 ↓
DEPLOY
 ↓
READBACK METRICS
 ↓
KEEP / MODIFY / REMOVE
```

The claim that indexing is universally the '#1' performance lever is not treated as an engineering invariant; workload, query plan, storage engine and data distribution determine the outcome.

## Unified synthesis

```text
BUSINESS CAPABILITY
        ↓
AI PROVIDER / TOOL REGISTRY
        ↓
AGENT / IDE / WORKFLOW
        ↓
SOURCE CONTROL + CI/CD
        ↓
ARTIFACT / SERVERLESS / CONTAINER RUNTIME
        ↓
API / NETWORK / DNS / EDGE
        ↓
DATABASE / VECTOR / MEMORY SUBSTRATE
        ↓
SECURITY CONTROLS + THREAT VALIDATION
        ↓
OBSERVABILITY
        ↓
PROVENANCE + POSTCONDITION VERIFICATION
        ↓
DURABLE MEMORY / AUDIT
```

## Security and authority invariants

- product listed ≠ capability currently available;
- provider connected ≠ operation authorized;
- tool installed ≠ permission to invoke it;
- security tool ≠ authorization to test a target;
- vulnerability pattern ≠ vulnerability finding;
- attack diagram ≠ exploit authorization;
- deployment success ≠ runtime health;
- serverless invocation ≠ downstream authorization;
- network-layer classification ≠ complete threat model;
- index exists ≠ query is faster;
- benchmark result ≠ universal performance truth;
- artifact exists ≠ artifact provenance is verified;
- generated state ≠ promoted state.

## Project mapping

| Project | Impact | Reason |
|---|---|---|
| P100 | HIGH | AI toolchain registry, DevSecOps, CI/CD, serverless, security adapters, release provenance |
| P40 | HIGH | capability broker, event-driven execution, API/egress policy and authorization |
| P28 | HIGH | attack-class testing, security-tool adapters, layered threat verification |
| P114 | HIGH | database/indexing and durable memory/query substrate |
| P37 | MEDIUM-HIGH | network, runtime, serverless and infrastructure substrate |
| P16 | MEDIUM-HIGH | AI-engineer skill ontology, prerequisites and learning evidence |
| P102 | MEDIUM | cloud/edge deployment, observability and service architecture |
| P33 | MEDIUM | secure web/API/database defaults |

## Project genesis decision

**NO NEW NUMBERED PROJECT.**

The corpus does not establish a clean new product boundary. It deepens existing development, security, infrastructure, skill and memory/data lineages.

## Verification backlog

1. P100: model the complete toolchain as typed capabilities with lifecycle and authorization state.
2. P100/P40: add event-trigger/serverless execution contracts including egress, budget and postcondition policy.
3. P100/P28: map threat classes to controls, evidence, retest and verified state.
4. P100/P37: extend layered network observations and control coverage.
5. P114: add workload/query-plan/index benchmark metadata and index lifecycle state.
6. P16: encode AI-engineer prerequisites as a dependency graph with evidence-backed competency state.
7. P100: integrate CI/CD deployment strategies with artifact provenance and runtime readback.
