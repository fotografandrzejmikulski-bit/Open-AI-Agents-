# Edge Runtime, Model Routing & Influence Defense — Knowledge Synthesis

## Scope

Synteza materiałów dostarczonych 2026-09-07 dotyczących: budowy własnych asystentów AI, agentów badawczych, porównania Claude/Gemini, architektury local/edge AI, Android AICore/MediaPipe, Genkit/Ollama, Codex Obscura oraz materiałów o sugestii i wpływie.

## 1. Agent is a system, not a prompt

Materiały o własnym asystencie przedstawiają hierarchiczny system prompt jako konstytucję agenta, knowledge base jako warstwę wiedzy, workflow jako procedurę działania, a ograniczenia jako warstwę bezpieczeństwa. fileciteturn74file14L637-L680

Wniosek architektoniczny:

```text
ROLE / PURPOSE
      ↓
KNOWLEDGE
      ↓
WORKFLOW
      ↓
POLICY / CONSTRAINTS
      ↓
TOOLS / MCP
      ↓
EVALUATION
```

Nie należy utożsamiać promptu z pełnym systemem bezpieczeństwa.

## 2. MCP integration pattern

Źródła pokazują wzorzec: agent → connector/MCP → data/tool → wynik → synteza, z vaultingiem sekretów, testowaniem sandboxowym i fallbackiem przy błędach. fileciteturn74file16L731-L755

Portfolio invariant:

`DISCOVER → FILTER → AUTHORIZE → CALL → VALIDATE → AUDIT`

## 3. Stateful research agents

Materiał o LangGraph opisuje graf stanowy z plannerem, równoległymi workerami, agregatorem, reflection node i finalnym raportem. fileciteturn74file10L465-L494

To wzmacnia Projects 15, 19 i 27:

```text
QUESTION
 ↓
PLAN
 ↓
PARALLEL WORKERS
 ↓
AGGREGATE
 ↓
CRITIQUE
 ↓
NEW QUESTIONS
 ↓
RESEARCH LOOP
 ↓
FINAL REPORT
```

## 4. Model specialization

Porównanie Claude/Gemini przedstawia specjalizacje zamiast jednego zwycięzcy: Claude jest opisany jako mocniejszy w długim tekście, kodzie, ostrożności i praktycznej pracy z długim kontekstem, Gemini jako mocniejszy w szybkości, multimodalności, wyszukiwaniu i integracjach Google. fileciteturn77file8L487-L524

Te obserwacje są **hipotezami routingowymi**, nie trwałymi rankingami. Project 17 powinien je stale walidować na własnych benchmarkach.

## 5. Provider-neutral execution

Architektura „darmowego” stosu proponuje rozdzielenie logiki biznesowej od modelu przez Genkit oraz możliwość użycia Ollama lokalnie. fileciteturn77file2L129-L153

Dodatkowo materiał proponuje edge inference przez browser API oraz mobile inference przez AICore/MediaPipe. fileciteturn77file4L233-L280 fileciteturn77file9L547-L568

Wniosek:

```text
MODEL ≠ PROVIDER ≠ SUBSTRATE
```

To jest kluczowy element Project 37.

## 6. Edge inference resilience

Browser-side AI powinien być opakowany wrapperem odpowiedzialnym za capability detection, lifecycle sesji, streaming, brak dostępności i graceful degradation. fileciteturn77file4L233-L280

Mobile AI powinno rozdzielać system-managed inference od przypadków wymagających własnego modelu. fileciteturn77file9L547-L568

## 7. Zero-cost claims

Źródło przedstawia local/edge architecture jako sposób na ograniczenie kosztu tokenów, latency i data egress. fileciteturn77file11L622-L636 Nie należy jednak traktować deklarowanego „$0.00” ani przyszłych prognoz jako gwarancji ekonomicznej.

Correct engineering target:

`minimize marginal cost while preserving quality, privacy, reliability and security`.

## 8. Security from influence material

Materiały dotyczące subliminal force i mentalismu pokazują mechanizmy kierowania uwagą, oczekiwaniami, sekwencją instrukcji i interpretacją doświadczenia. fileciteturn76file0L19-L45

Materiały o synchronized drinking pokazują połączenie instrukcji werbalnej, gestu, akcentu i powtarzalnego kierowania uwagi. fileciteturn77file15L805-L818

W portfolio są one używane wyłącznie do **defensive threat modeling**:

```text
ATTENTION DIRECTION
+ EXPECTANCY
+ REPETITION
+ PRESSURE
+ LOW TRANSPARENCY
→
INFLUENCE RISK
```

Nie należy implementować tych technik jako covert-control mechanism.

## 9. Black System Apeiron as systems metaphor

Codex Obscura używa metafor takich jak Firewall, Air-Gap, Validator, Buffer, System Wipe, Optimization, Malware, Data Breach, Signal, Deepfake i Recall, a także modelu Page=Daemon, Knight=Runner, Queen=Proxy, King=Admin. fileciteturn76file16L816-L840 fileciteturn76file2L147-L163

Te elementy mogą być traktowane jako warstwa nomenklatury i UX dla projektu bezpieczeństwa, ale nie jako dowód techniczny ani opis rzeczywistych mechanizmów systemowych.

## 10. New portfolio consequences

Źródła wzmacniają następujące invariants:

1. Model is replaceable.
2. Provider is replaceable.
3. Execution substrate is replaceable.
4. Authorization is independent from model choice.
5. Edge/local inference remains untrusted until verified.
6. Research state must be explicit and resumable.
7. Tool access must be capability-scoped.
8. Influence must be measurable as a safety risk, not optimized as a hidden objective.
9. Cost optimization cannot weaken privacy or security.
10. All source-specific performance claims require reproducible evaluation.

## 11. Deep OSINT collector architecture

Dostarczony `DeepOSINT` pokazuje praktyczny baseline kolektorów: web crawling i ekstrakcję kontaktów, generowanie zaawansowanych zapytań, EXIF oraz network reconnaissance. fileciteturn98file0L12-L25 fileciteturn98file0L53-L85 fileciteturn98file0L92-L126 fileciteturn98file0L128-L147

Najważniejsza konsekwencja architektoniczna: kolektor jest adapterem danych, a nie właścicielem polityki. Każdy kolektor powinien mieć wersję, input/output schema, collection mode, wymagane capabilities, target constraints, rate limit, provenance fields i jawne failure modes.

Wzorzec:

```text
COLLECTOR
 ↓
NORMALIZE
 ↓
PROVENANCE
 ↓
EVIDENCE QUALITY GATE
 ↓
EVIDENCE GRAPH
```

Aktywne operacje, takie jak socket-based port scanning, wymagają jawnego scope, autoryzacji, allowlisty operacji, rate limitu i audytu. Zapytania dotyczące paneli administracyjnych, plików konfiguracyjnych lub treści wyciekowych są traktowane jako high-risk discovery patterns i nie są domyślną ścieżką pozyskiwania danych uwierzytelniających. fileciteturn98file0L26-L52 fileciteturn98file0L128-L147

## 12. Constraint-aware scientific reasoning

Drugi materiał wnosi niezależny pattern: odpowiedź techniczna powinna być oceniana względem jawnych warunków stabilności, termodynamiki i geometrii funkcji celu, a nie tylko względem językowej plausibility. W materiale pojawiają się równania MHD i równowaga `∇p = J × B`, krajobraz energii swobodnej z kosztami entropowymi i solwatacją oraz klasyfikacja punktów krytycznych przez wartości własne Hesjanu. fileciteturn98file1L8-L20 fileciteturn98file1L21-L36 fileciteturn98file1L37-L50

W portfolio zostaje to uogólnione do:

```text
CLAIM
 ↓
ASSUMPTIONS
 ↓
CONSTRAINTS
 ↓
SYMBOLIC / NUMERIC CHECK
 ↓
STABILITY / SENSITIVITY
 ↓
EVIDENCE + COUNTEREVIDENCE
 ↓
SIMULATION / FORMAL CHECK
 ↓
CONDITIONAL ACCEPTANCE OR ESCALATION
```

Kluczowa zasada: `unknown` nie jest równoważne `satisfied`.

## 13. Scientific claim provenance

Nowy wzorzec łączy Research Orchestrator z Verified Code Generation i Evidence OSINT:

```text
OBSERVATION
≠ DERIVATION
≠ SIMULATION RESULT
≠ EMPIRICAL RESULT
≠ HYPOTHESIS
≠ PROVEN CLAIM
```

Każda konkluzja naukowo-techniczna powinna przechowywać assumptions, equations, constraints, evidence, counterevidence, verification status i uncertainty. Wysokokonsekwencyjne tezy wymagają zewnętrznej walidacji eksperckiej.

## 14. Updated portfolio invariants

11. A collector never owns authorization policy.
12. Active OSINT actions require explicit scope and authorization.
13. Raw observation must remain distinguishable from inference.
14. A scientific claim with an unresolved required constraint cannot be `verified`.
15. Stability and sensitivity are first-class verification properties.
16. Agreement between multiple solvers is not proof when they share assumptions.
17. Domain-specific criteria must be versioned against authoritative sources.
18. High-consequence scientific/medical/physical side effects remain outside autonomous agent authority.

## 15. Alibaba Cloud — agent/cloud execution fabric

Alibaba Cloud adds a complete implementation layer spanning Model Studio, Qwen and third-party models, MCP, AgentBay, ACK, ECS, Function Compute, OSS, SLS, RAM/STS and Container Registry. Model Studio exposes OpenAI-compatible and native interfaces; AgentBay provides agent-oriented sandbox execution; ACK provides heterogeneous GPU/ASIC/eRDMA scheduling; RAM provides deny-by-default authorization and temporary role credentials; OSS supplies versioned object storage; SLS supplies logs/metrics/traces/events; ACR can block risky container images. citeturn0search1turn0search8turn1search22turn2search13turn1search3turn1search21turn1search2turn2search1turn1search4

### 15.1 Model gateway

`MODEL != PROVIDER != EXECUTION SUBSTRATE` remains invariant. Model Studio is an adapter with explicit model, region, quota, cost and evaluation profiles rather than the authority for policy.

### 15.2 MCP capability boundary

Model Studio supports MCP through the Responses API using SSE MCP servers. citeturn0search0 The correct OmniCore pattern remains:

```text
DISCOVER → TRUST/PROVENANCE → ALLOWLIST → AUTHORIZE → CALL → VALIDATE → AUDIT
```

### 15.3 Disposable agent runtime

AgentBay supports ephemeral sandboxes and MCP-accessible browser, computer, mobile and code environments. citeturn2search5turn2search6 The sandbox is execution isolation, not authorization.

Persistent browser state is treated as high-sensitivity state because AgentBay can retain cookies, cache, local/session storage, preferences and extensions. citeturn2search0

### 15.4 Heterogeneous compute

ACK supports GPUs, ASICs and eRDMA, including GPU sharing/fencing and GPU autoscaling. citeturn2search13turn2search8 This extends Project 37 into a continuous local/edge/cloud compute fabric.

### 15.5 Cloud authorization

RAM uses deny-by-default and explicit-deny-overrides-allow semantics; roles can provide temporary STS credentials. citeturn1search3turn1search12turn1search21 Resource-group scope can isolate projects/environments. citeturn1search6

### 15.6 Evidence/object fabric

OSS provides versioned object storage, lifecycle policies, multiple storage classes and encryption/integrity features. citeturn1search2turn1search8turn1search14 This is useful for Project 30/32 evidence artifacts only when provenance, retention, jurisdiction and access policies are explicit.

### 15.7 Observability

SLS unifies logs, metrics, traces and events and supports alerting and correlated monitoring. citeturn2search1turn2search2turn2search10 The canonical agent event should connect model, capability, policy decision, provenance, artifact, latency, cost and security event through a shared trace ID.

### 15.8 Supply-chain verification

ACR can scan pushed images and enforce blocking policies for high-risk images. citeturn1search4 This strengthens Project 28's `GENERATE → BUILD → SBOM → SCAN → POLICY GATE → SIGN → STAGED DEPLOYMENT` chain.

### 15.9 Confidential execution

ECS documents memory encryption, trusted computing/vTPM and confidential computing with remote attestation on supported instance families. citeturn0search4 This adds an optional higher trust tier but does not replace application-level authorization or provenance.

## 16. Alibaba-derived portfolio invariants

19. Cloud provider is an execution substrate, not the policy authority.
20. Sandbox isolation is not authorization.
21. Persistent browser state is a privileged capability.
22. Temporary cloud credentials should be purpose-bound and short-lived.
23. GPU scheduling must remain scheduler-mediated and tenant-aware.
24. Object storage becomes evidence infrastructure only with provenance and retention controls.
25. Container promotion requires supply-chain verification.
26. Observability must correlate model, capability, policy, artifact and security events.
27. Cloud-native features must not silently bypass the OmniCore policy plane.
28. Local/edge/cloud routing should optimize measurable quality, latency, privacy, energy and cost rather than provider preference.

## Projects affected

- Project 15 — Universal Research Orchestrator
- Project 17 — Adaptive Model Router
- Project 21 — Google AI Sovereign Developer Stack
- Project 26 — OmniCore Trustworthy Kernel & Agentic Safety Lab
- Project 28 — OmniCore AI Foundry / Verified Code Generation
- Project 30 — OmniCore Sugra Evidence/OSINT Control Fabric
- Project 31 — OmniCore Sovereign Agent Operating Fabric MAX
- Project 32 — Deep OSINT Evidence Engine MAX
- Project 33 — Agentic App Builder & Delivery Control Plane MAX
- Project 35 — Context-Aware Intent & Agent Security Engine MAX
- Project 36 — Influence Security & Human Agency Defense Lab MAX
- Project 37 — Sovereign Edge AI Runtime & Zero-Cost Delivery Fabric MAX
- Project 38 — OmniCore Constraint-Aware Scientific Reasoning & Stability Verifier MAX
- Project 39 — OmniCore Alibaba Cloud Agent Runtime & Cloud Fabric MAX
