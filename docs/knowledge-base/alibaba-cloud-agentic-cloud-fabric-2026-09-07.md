# Alibaba Cloud Agentic Cloud Fabric — Knowledge Synthesis

## Scope

Źródła oficjalnej dokumentacji Alibaba Cloud przeanalizowane 2026-09-07. Zakres: Model Studio, Qwen, MCP, AgentBay, Browser/Computer Use, ACK, GPU/heterogeneous compute, RAM/STS, OSS, SLS, ECS, Function Compute i Container Registry.

## 1. Model Studio

Model Studio jest warstwą usług modeli obejmującą Qwen i wybrane modele zewnętrzne, z interfejsami natywnymi oraz OpenAI-compatible. Obsługuje także multimodalne scenariusze tekst/obraz/audio/video. citeturn0search1turn0search8turn0search13

**Architectural lesson:** model provider powinien być adapterem pod provider-neutral execution contract.

```text
APPLICATION CONTRACT
        ↓
MODEL ADAPTER
        ↓
QWEN / THIRD-PARTY MODEL
```

## 2. Responses + MCP

Model Studio pozwala dodawać serwery MCP do Responses API; dokumentacja wskazuje SSE jako obsługiwany protokół oraz limit 10 serwerów MCP w żądaniu. citeturn0search0

Wzorzec dla OmniCore:

```text
DISCOVER
 ↓
TRUST / PROVENANCE
 ↓
ALLOWLIST
 ↓
AUTHORIZE
 ↓
CALL
 ↓
VALIDATE
 ↓
AUDIT
```

MCP jest capability boundary, nie mechanizmem zaufania samym w sobie.

## 3. AgentBay

AgentBay jest pozycjonowany jako cloud infrastructure dla AI Agents. Dostarcza runtime, MCP services, izolowane środowiska i mechanizmy zachowania stanu użytkownika. citeturn1search22

Jego MCP tools obejmują tworzenie sandboxów, runtime URLs, screenshoty, shell i środowiska BrowserUse/ComputerUse/MobileUse/CodeSpace. citeturn2search5turn2search6

Canonical execution:

```text
TASK
 ↓
EPHEMERAL SANDBOX
 ↓
MINIMAL STATE
 ↓
CAPABILITY-SCOPED EXECUTION
 ↓
ARTIFACT COLLECTION
 ↓
VERIFICATION
 ↓
PERSIST APPROVED ARTIFACT
 ↓
SANDBOX RELEASE
```

## 4. Persistent browser state

AgentBay może zachowywać cookies, cache, local/session storage, browser preferences i extensions między sesjami. citeturn2search0

To należy klasyfikować jako **high-sensitivity persistent state**. Persistence nie może automatycznie oznaczać prawa modelu do odczytu, eksportu lub przenoszenia stanu.

## 5. Browser / Computer Use

AgentBay dostarcza cloud browser oraz Computer Use dla aplikacji desktopowych bez API. citeturn2search9turn2search12

W OmniCore ekran, DOM, OCR, pliki i stan aplikacji są traktowane jako untrusted multimodal input:

```text
UNTRUSTED INPUT
 ↓
INTERPRETATION
 ↓
CAPABILITY CHECK
 ↓
ACTION PREVIEW
 ↓
EXECUTION
 ↓
RESULT VERIFICATION
```

## 6. ACK heterogeneous compute

ACK zarządza heterogenicznymi zasobami, m.in. GPU, ASIC i eRDMA. Wspiera GPU scheduling, autoscaling, GPU sharing i computing-power fencing. citeturn2search13turn2search8

Wniosek dla Project 37: local/edge/cloud jest jednym continuum wykonawczym, a nie trzema niezależnymi światami.

```text
LOCAL → EDGE → ON-PREMISE GPU → CLOUD GPU → SPECIALIZED MODEL
```

Routing powinien uwzględniać jakość, latency, privacy, energy, cost, data gravity i capability.

## 7. Kubernetes GPU safety

ACK wskazuje standardowy mechanizm Kubernetes resource requests jako właściwą drogę alokacji GPU i ostrzega przed obchodzeniem scheduler/resource model przez bezpośrednie żądanie GPU na node. citeturn2search3

To wzmacnia portfolio invariant:

**resource policy must be enforced by the substrate scheduler, not by informal agent conventions.**

## 8. RAM / STS

RAM stosuje deny-by-default, a explicit Deny overrides Allow. Polityki używają `Effect`, `Action`, `Resource`, `Condition` oraz `Principal` tam, gdzie ma zastosowanie. citeturn1search3turn1search5turn1search12

RAM roles korzystają z tymczasowych credentials przez STS zamiast długoterminowych sekretów. citeturn1search21

To jest bezpośredni wzorzec dla OmniCore Capability Grant:

```yaml
subject:
action:
resource:
conditions:
expiry:
purpose:
approval:
audit_id:
```

Resource groups pozwalają ograniczać zakres do projektu, środowiska lub zespołu. citeturn1search6

## 9. OSS

OSS oferuje wiele klas storage od Standard do Deep Cold Archive, wersjonowanie obiektów oraz lifecycle management. citeturn1search2turn1search11turn1search14

Obsługuje także server-side/client-side encryption, TLS i mechanizmy integrity/security. citeturn1search8turn1search17

Dla OmniCore:

```text
RAW ARTIFACT
 ↓
SNAPSHOT
 ↓
HASH + METADATA
 ↓
EVIDENCE ID
 ↓
VERSIONED DERIVATIVES
 ↓
RETENTION / LIFECYCLE
```

## 10. SLS

Simple Log Service obejmuje logs, metrics, traces i events; posiada Logstore, Metricstore i Eventstore. citeturn2search1turn2search2

Alerting zapewnia monitoring, noise reduction, incident management i correlated monitoring. citeturn2search10

Canonical AgentEvent:

```yaml
trace_id:
span_id:
agent_id:
session_id:
model:
capability:
policy_decision:
input_provenance:
output_provenance:
latency:
tokens:
cost:
error:
security_event:
artifact_id:
```

## 11. Function Compute

Function Compute rozdziela control-plane authorization od data-plane execution, korzysta z RAM i izolacji kodu/layers; data plane stosuje TLS 1.2+ i może być ograniczony do VPC. citeturn0search9turn0search2

Najlepszy wzorzec agentowy:

```text
EVENT → POLICY → BOUNDED FUNCTION → VALIDATE → AUDIT
```

Nie należy traktować serverless jako zgody na nieograniczoną autonomię.

## 12. Container Registry / supply chain

ACR może automatycznie skanować obrazy i blokować obrazy wysokiego ryzyka w CI/CD. citeturn1search4

Wzorzec Project 28:

```text
GENERATE → BUILD → SBOM → SCAN → POLICY GATE → SIGN → STAGE → OBSERVE → PROMOTE/ROLLBACK
```

## 13. ECS trust tiers

ECS dokumentuje memory encryption, vTPM/trusted computing oraz confidential computing z remote attestation na wspieranych instancjach. citeturn0search4

Możliwy trust ladder:

```text
STANDARD
 ↓
HARDENED
 ↓
TRUSTED BOOT / vTPM
 ↓
TEE
 ↓
REMOTE ATTESTATION
```

Attestation wzmacnia trust boundary, ale nie zastępuje application authorization.

## 14. RAG and workflow

Model Studio knowledge base wykorzystuje RAG do pobierania relevant chunks przed generacją, a workflow pozwala łączyć LLM nodes, APIs i Function Compute w uporządkowane kroki. citeturn1search0turn1search10turn1search18

OmniCore zachowuje własne evidence/policy layer jako nadrzędną warstwę kontroli.

## 15. Strategic synthesis

Alibaba Cloud wnosi do portfolio nie pojedynczy produkt, lecz **pełny referencyjny pion agentic cloud**:

```text
MODEL
 ↓
MCP
 ↓
AGENT RUNTIME
 ↓
SANDBOX / COMPUTER USE
 ↓
COMPUTE SCHEDULER
 ↓
STORAGE
 ↓
IDENTITY
 ↓
OBSERVABILITY
 ↓
SUPPLY-CHAIN SECURITY
 ↓
TRUSTED / CONFIDENTIAL COMPUTE
```

Najważniejsza lekcja: warstwa agentowa powinna być projektowana jako system wykonawczy z kontrolą tożsamości, capability, stanu, compute, danych, obserwowalności i release — nie jako sam model + prompt.

## 16. Portfolio invariants

1. Cloud provider is substrate, not policy authority.
2. Model choice does not grant authorization.
3. MCP requires trust/provenance filtering.
4. Sandbox isolation is not authorization.
5. Persistent browser state is privileged state.
6. Credentials should be short-lived and purpose-bound.
7. GPU resources require scheduler-mediated allocation.
8. Evidence storage requires provenance and retention policy.
9. Generated containers require supply-chain verification.
10. Agent telemetry must correlate cognition, capability, policy and artifact.
11. Cloud features must not bypass the OmniCore control plane.
12. Edge-to-cloud routing is a measurable optimization problem.

## Related projects

- Project 17 — Adaptive Model Router
- Project 26 — OmniCore Trustworthy Kernel & Agentic Safety Lab
- Project 28 — OmniCore AI Foundry / Verified Code Generation
- Project 30 — OmniCore Sugra Evidence/OSINT Control Fabric
- Project 31 — OmniCore Sovereign Agent Operating Fabric MAX
- Project 37 — Sovereign Edge AI Runtime & Zero-Cost Delivery Fabric MAX
- Project 39 — OmniCore Alibaba Cloud Agent Runtime & Cloud Fabric MAX
