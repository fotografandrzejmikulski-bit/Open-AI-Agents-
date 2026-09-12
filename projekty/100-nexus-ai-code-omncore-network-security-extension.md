# P100 Extension — OmniCore Agents Builder + Network Security Control Plane

## Parent
P100 — NeXus AI Code OMEGA-X Agentic Development Environment MAX

## Trigger
Six visual infographics plus four supplied OmniCore Agents Builder / Agents Builder architecture documents.

## Architectural finding
The corpus does not establish a new product boundary. It strengthens P100 as the desktop agent Control Plane and adds explicit capability domains for network/proxy/security tooling, source admissibility, sandboxed sidecars and OCN-style agent construction/evolution.

## OmniCore builder model

The supplied OCN 49.0/50.1/51.1 documents describe:
- agent metadata and a strict nine-file unit;
- cognitive loops and planning;
- DGM with immutable L-Genes and mutable D-Genes;
- AB-MCTS search/decision visualization;
- Dream Team Orchestrator and swarms/legions;
- MCP tool mediation;
- bitemporal graph memory;
- Tauri v2 + Rust + React/TypeScript;
- Zenoh SHM as a proposed zero-copy transport;
- Z3/SMT as a proposed formal-verification layer;
- Python sidecars and Windows packaging;
- GGUF, WebRTC and Arti/Tor adapters.

These are source-derived design/code claims, not proof of local compilation or runtime correctness.

## Canonical P100 flow

```text
AGENT / SWARM INTENT
 ↓
CAPABILITY DISCOVERY
 ↓
POLICY CLASSIFICATION
 ↓
AUTHORIZATION
 ↓
SANDBOXED EXECUTION
 ↓
OBSERVATION / READBACK
 ↓
VERIFICATION
 ↓
PROVENANCE
 ↓
MEMORY / EVOLUTION
```

## Capability registry

```yaml
Capability:
  provider:
  tool:
  domain: ai|network|security|research|automation|media|developer
  capability:
  modality:
  access: free|paid|api_key|oauth|local|unknown
  connected: false
  healthy: unknown
  authorized: false
  allowed: false
  trust_domain:
  scope:
  lifecycle:
  source:
  verified_at:
```

`CONNECTED ≠ HEALTHY ≠ AUTHORIZED ≠ ALLOWED`

## Network / proxy layer

The network-security infographic contributes a seven-layer threat taxonomy covering application, presentation, session, transport, network, data-link and physical threats. The proxy infographic contributes Squid, TinyProxy, Privoxy, 3proxy, ShadowSocks, Tor SOCKS, Psiphon, FreeProxy and CCProxy as example proxy capabilities.

Proxy architecture:

```text
INTENT
 ↓
ROUTE POLICY
 ↓
CAPABILITY DISCOVERY
 ↓
TRUST / PRIVACY / LOGGING CHECK
 ↓
AUTHORIZATION
 ↓
NETWORK EXECUTION
 ↓
READBACK
 ↓
EVIDENCE
```

Required invariants:

`REACHABLE ≠ AUTHORIZED`  
`OPEN PORT ≠ TRUSTED SERVICE`  
`TLS ≠ AUTHORIZATION`  
`VPN ≠ ZERO TRUST`  
`NAT ≠ SECURITY CONTROL`  
`PROXY ≠ TRUST BOUNDARY`

The infographic is conceptual context; it does not prove any control is configured or effective.

## AI security-agent layer

The AI-pentesting infographic contributes a discovery taxonomy, but its names/numbering are inconsistent and duplicated. Named tools remain unverified until independently checked.

Any security-testing capability in P100 must carry:
- authorized target scope;
- environment classification;
- authorization state;
- operation class;
- rate/concurrency limits;
- sensitive-data policy;
- stop conditions;
- evidence requirements;
- remediation/retest path.

Default:

```text
AUTHORIZED SCOPE
 ↓
PASSIVE ENUMERATION
 ↓
CONTROLLED TEST PLAN
 ↓
BOUNDED / SANDBOXED TEST
 ↓
FINDING + PROVENANCE
 ↓
REMEDIATION
 ↓
RETEST
```

## Source-selection layer

The AI citation-frequency infographic becomes a discovery prior only. Citation frequency is not a universal quality score.

```text
DISCOVERY FREQUENCY
 + AUTHORITY
 + CLAIM RELEVANCE
 + FRESHNESS
 + INDEPENDENCE
 + PRIMARY-SOURCE STATUS
 + LICENSING
 + CORROBORATION
 → EVIDENCE ADMISSIBILITY
```

This aligns with P30's external evidence plane.

## AI tool-pack taxonomy

The paid/free tool infographics strengthen capability classification for ideation, research, images, video, transcription, writing, design, avatars and automation. Static rankings, pricing and free/paid labels are not architectural truth.

Provider choice becomes:

`CAPABILITY → MODALITY → ACCESS → HEALTH → AUTHORIZATION → POLICY → COST → LATENCY → PROVENANCE`

## Sidecar security

The supplied 51.1 manifest declares an external Python binary. P100 therefore treats sidecars as separate trust domains:

```text
CONTROL PLANE
 ↓
POLICY
 ↓
SANDBOX / RESTRICTED PROCESS
 ↓
SIDECAR
 ↓
NARROW IPC
 ↓
OUTPUT VALIDATION
 ↓
READBACK
```

Localhost is not authority.

## Zero-copy / formal verification claims

Zenoh SHM and Z3/SMT remain candidate mechanisms requiring evidence. Dependency presence does not establish end-to-end zero-copy or safety proof.

Measure:
- copy count;
- serialization cost;
- latency/throughput;
- memory lifetime;
- isolation;
- failure recovery.

Formal verification path:

`PROPERTY → SOLVER RESULT → INDEPENDENT TEST → RUNTIME OBSERVATION`

## Explicit negative findings from the source code corpus

The supplied code contains or describes several constructs that cannot be promoted to security guarantees without replacement/verification:
- a `verify_voice(_voice) -> true` stub is not authentication;
- acoustic XOR-style RAM manipulation is not established encryption;
- linguistic transformation does not eliminate prompt injection by itself;
- opening GGUF files does not prove direct hardware embedding;
- importing Zenoh SHM does not prove all paths are zero-copy;
- MSI configuration does not prove signed/reproducible distribution;
- Z3 dependency does not prove arbitrary generated behavior is safe;
- autonomous self-modification requires immutable invariants, staging, rollback and independent verification;
- Tor/Arti routing does not guarantee identity protection for every application path.

## Cross-project mapping

- **P100:** primary integration — agent builder, capability registry, network/proxy mediation, security-agent policy, sidecar isolation and release assurance.
- **P30:** source authority/freshness/independence and citation discovery prior.
- **P32:** authorized passive OSINT/network evidence and proxy policy.
- **P114:** bitemporal memory and provenance-bearing retrieval.
- **P117/P119:** desktop-to-mobile agent bridge with explicit authorization/readback.

## New-project decision

**NO NEW NUMBERED PROJECT.**

The corpus is cross-cutting architecture and fits existing control-plane/evidence/security/memory/mobile boundaries.

## Status

**ARCHITECTURE ENHANCED — IMPLEMENTATION NOT YET VERIFIED**
