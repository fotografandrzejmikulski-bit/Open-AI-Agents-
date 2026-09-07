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

## Projects affected

- Project 15 — Universal Research Orchestrator
- Project 17 — Adaptive Model Router
- Project 21 — Google AI Sovereign Developer Stack
- Project 26 — OmniCore Trustworthy Kernel & Agentic Safety Lab
- Project 31 — OmniCore Sovereign Agent Operating Fabric MAX
- Project 33 — Agentic App Builder & Delivery Control Plane MAX
- Project 35 — Context-Aware Intent & Agent Security Engine MAX
- Project 36 — Influence Security & Human Agency Defense Lab MAX
- Project 37 — Sovereign Edge AI Runtime & Zero-Cost Delivery Fabric MAX
