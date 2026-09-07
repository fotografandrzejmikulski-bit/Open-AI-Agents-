# Agentic Coding, Visual Intelligence & Prompt-Control — Knowledge Synthesis — 2026-09-08

## Scope
Synteza nowych materiałów: Microsoft AI Agents for Beginners, G0DM0D3, God's Eye View, Ghost Protocol v2, NEXUS-EYE Ultimate, materiały Google AI for Developers, raport o unikalnych promptach oraz wcześniejsze architektury OmniCore/OSINT.

## 1. Agent = context + policy + capabilities + state + verification

Najważniejsza wspólna lekcja wszystkich źródeł: agent nie jest pojedynczym promptem. Jest pętlą wykonawczą, w której model interpretuje stan, wybiera capability, uruchamia deterministyczne działanie, odczytuje wynik i dopiero wtedy aktualizuje stan.

```text
INTENT
 ↓
CONTEXT COMPILATION
 ↓
REASONING / PLAN
 ↓
CAPABILITY SELECTION
 ↓
AUTHORIZATION
 ↓
DETERMINISTIC EXECUTION
 ↓
AUTHORITATIVE READBACK
 ↓
VERIFY POSTCONDITION
 ↓
STATE DELTA / ARTIFACT
```

Ghost Protocol pokazuje prosty wariant ACL: LLM generuje sygnał akcji, backend wykonuje narzędzie, wynik wraca do kontekstu i model dokonuje syntezy. fileciteturn134file0L10-L32

## 2. Repo-scale coding agents

Wzorzec repo-scale coding agenta wymaga jednoczesnego dostępu do:

- drzewa repozytorium i zależności;
- dokumentacji i issue/PR context;
- terminala/build/test runnera;
- obserwacji błędów;
- deterministycznych operacji na plikach;
- checkpointów i możliwości wznowienia.

Nie wystarcza pojedyncze `generate_code()`. Agent musi umieć przejść przez pętlę:

```text
DISCOVER REPO
 → FORM HYPOTHESIS
 → PATCH
 → BUILD
 → TEST
 → READ FAILURE
 → REPAIR
 → RE-TEST
 → VERIFY
 → COMMIT
```

## 3. Action runner > free-form tool execution

God's Eye View dostarcza mocnego wzorca deterministycznego action runnera dla agenta multimodalnego. Narzędzia posiadają jawne nazwy, aliasy parametrów, walidację stanu i obsługę anulowania; wynik zawiera rzeczywisty stan po operacji. Szczególnie ważna jest zasada, że agent nie powinien potwierdzać akcji wyłącznie na podstawie własnej narracji — wynik narzędzia musi zostać odczytany z authoritative state. fileciteturn123file0L1-L2 fileciteturn125file0L1-L2

Nowy invariant:

`ACTION SUCCESS = EXECUTION + VERIFIED POSTCONDITION`

## 4. Supersession, cancellation and stale-turn defense

God's Eye View posiada explicit response identity, supersession memory, abort controllers i grace periods dla chwilowych rozłączeń. Narzędzia, które zostaną uruchomione, mogą dokończyć się, ale stary turn nie może nadpisać autorytatywnego stanu nowszego turnu. fileciteturn123file0L1-L2

OmniCore powinien rozszerzyć model stanu o:

```yaml
Turn:
  turn_id:
  session_id:
  parent_state_version:
  status: pending|executing|superseded|cancelled|committed
  capabilities:
  postconditions:
  state_delta:
```

Każdy commit stanu wymaga zgodności z aktualnym `state_version` lub jawnego merge policy.

## 5. Multimodal state is evidence, not truth

God's Eye View łączy dane telemetryczne, scene context, DOM, screenshoty, warstwy mapy i dane publiczne. Screenshot służy jako best-effort context i nie może blokować podstawowej ścieżki odpowiedzi. Agent ma wykonywać działania wyłącznie przez ograniczony zestaw app-control tools. fileciteturn121file0L8-L17 fileciteturn122file0L2-L2

W OmniCore oznacza to:

```text
OBSERVATION
 ↓
PROVENANCE + TIMESTAMP + SOURCE
 ↓
UNCERTAINTY
 ↓
INTERPRETATION
 ↓
ACTION PROPOSAL
```

Percepcja nie nadaje sama sobie uprawnień.

## 6. Ephemeral credential architecture

God's Eye View trzyma sekret OpenAI na serwerze i wydaje przeglądarce krótkotrwały token sesyjny. Podobny wzorzec obowiązuje dla innych sekretów backendowych. fileciteturn122file0L2-L2

Portfolio invariant:

`LONG-LIVED SECRET → SERVER-SIDE BROKER → SHORT-LIVED EPHEMERAL SESSION CREDENTIAL`

## 7. Network proxy as capability firewall

God's Eye View ogranicza proxy do zarejestrowanych upstreamów, stosuje timeouty, response-size caps, sanitized errors, blokadę arbitralnych URL oraz ochronę SSRF; LAN exposure jest jawnie opt-in i kosztowne endpointy mają procesowe limity. fileciteturn122file0L2-L2

OmniCore Capability Broker powinien przejąć ten pattern dla wszystkich connectorów:

```text
MODEL REQUEST
 ↓
CAPABILITY RESOLUTION
 ↓
DESTINATION ALLOWLIST
 ↓
NETWORK POLICY
 ↓
RATE / COST LIMIT
 ↓
EXECUTE
 ↓
SANITIZE RESULT
 ↓
AUDIT
```

## 8. Multi-model racing and comparative evaluation

G0DM0D3 wprowadza dwa istotne patterns: równoległe uruchamianie wielu modeli oraz systematyczne ocenianie wyników wspólnym scoringiem. README opisuje GODMODE CLASSIC jako race kilku modeli oraz ULTRAPLINIAN jako wielomodelową ewaluację z tierami i composite score. fileciteturn116file0L1-L2

PAPER dodatkowo opisuje AutoTune, Parseltongue, STM, ULTRAPLINIAN i feedback loop jako osobne, konfigurowalne moduły. fileciteturn119file0L1-L2

Generalized OmniCore pattern:

```text
QUERY
 ↓
MODEL/TACTIC VARIANTS
 ↓
PARALLEL EXECUTION
 ↓
NORMALIZATION
 ↓
SCORING
 ↓
DISAGREEMENT ANALYSIS
 ↓
WINNER / ENSEMBLE / ESCALATION
```

Nie należy traktować `winner` jako dowodu poprawności. Zgodność solverów wymaga analizy zależności wspólnych założeń.

## 9. Adaptive parameter control

G0DM0D3 AutoTune pokazuje pattern dynamicznego doboru parametrów inferencji zależnie od kontekstu, z blended defaults i ograniczeniami zakresów; feedback loop wykorzystuje uczenie EMA. fileciteturn119file0L1-L2

OmniCore powinien modelować parametry jako część wersjonowanego `ExecutionProfile`, np.:

```yaml
ExecutionProfile:
  task_class:
  model:
  reasoning_budget:
  sampling_profile:
  latency_target:
  cost_ceiling:
  safety_profile:
  eval_profile:
```

Profile nie powinny móc obniżać wymaganych security gates.

## 10. Prompt engineering as compilation, not magic

Raport o unikalnych promptach przedstawia prompt jako kompozycję precyzji strukturalnej, architektury kognitywnej i iteracyjnej ewaluacji. fileciteturn133file0L9-L31

Praktyczny pattern:

```text
ROLE / CONTEXT
 ↓
TASK / DATA
 ↓
CONSTRAINTS
 ↓
MENTAL MODEL / METHOD
 ↓
OUTPUT CONTRACT
 ↓
COUNTERARGUMENT / BLIND-SPOT CHECK
 ↓
EVALUATION
 ↓
REVISION
```

Materiał wskazuje też strukturę typu „górna kromka / mięso / dolna kromka”, w której krytyczne ograniczenia są powtórzone na końcu. fileciteturn134file6L339-L344

Warto przenieść to do Project 24 jako kompilowalny Prompt DSL.

## 11. Persona library + mental models

Raport promptowy wskazuje biblioteki person i modeli mentalnych: architekt systemów, księgowy śledczy, tutor sokratejski, red-team specialist, negocjator kryzysowy oraz techniki takie jak inwersja. fileciteturn134file6L345-L380

Bezpieczne zastosowanie dla OmniCore: persona jest `reasoning profile`, a nie źródłem dodatkowych uprawnień.

```yaml
ReasoningPersona:
  role:
  cognitive_bias_target:
  preferred_methods:
  required_checks:
  forbidden_assumptions:
```

## 12. Scientific stability as generic agent principle

Raport o fuzji, medycynie i optymalizacji pokazuje wspólny schemat: system należy analizować przez krajobraz celu, ograniczenia, stabilność i mechanizmy wyjścia z pułapek. Wspólny wzorzec obejmuje MHD, dynamiczne symulacje molekularne, Hessian i stochastyczne metody optymalizacji. fileciteturn134file4L251-L270

Tabela raportu zestawia problem niestabilności, krajobraz oraz mechanizm ucieczki/stabilizacji. fileciteturn134file5L281-L318

Generalized agent principle:

```text
STATE
 ↓
CONSTRAINTS
 ↓
OBJECTIVE LANDSCAPE
 ↓
STABILITY CHECK
 ↓
SENSITIVITY / PERTURBATION
 ↓
ESCAPE LOCAL TRAP
 ↓
VERIFY
```

To wzmacnia Project 38 — Constraint-Aware Scientific Reasoning & Stability Verifier.

## 13. OSINT fusion and graph intelligence

NEXUS-EYE oraz PAULA OS wskazują na łączenie wielu źródeł danych w graf węzłów i krawędzi. NEXUS-EYE posiada węzły opisujące IP, lokalizację, organizację, ASN, technologie, CMS, metadata i email; relacje są zapisywane jako edges. fileciteturn133file8L21-L29 fileciteturn133file8L61-L75

PAULA OS definiuje Fusion Intelligence: KRS, CRT, port scanning, EXIF i Socials są agregowane, normalizowane i oceniane przez LLM, z widokiem grafowym 2D i strategicznym 3D. fileciteturn134file2L139-L151

Bezpieczny standard OmniCore:

`RAW OBSERVATION → SOURCE → NODE → EDGE → EVIDENCE QUALITY → INFERENCE`

Graf nie jest dowodem sam w sobie; krawędź musi mieć provenance i confidence.

## 14. Ghost Protocol lessons, hardened

Ghost Protocol pokazuje użyteczny, ale niesurowy wzorzec: LLM emituje sygnał `<<SCAN:TARGET>>`, backend wykonuje skan i zwraca wynik do kontekstu. fileciteturn134file1L61-L104

Problem architektoniczny: parser tekstowy nie jest wystarczającym capability protocol. Wzmocnienie:

```text
FREE-FORM MODEL OUTPUT
        ↓
STRUCTURED ACTION SCHEMA
        ↓
TARGET VALIDATION
        ↓
AUTHORIZATION / SCOPE
        ↓
RATE LIMIT / BUDGET
        ↓
SANDBOX / SAFE EXECUTOR
        ↓
OBSERVE
        ↓
VERIFY
```

Aktywny network reconnaissance pozostaje dozwolony tylko w jawnie autoryzowanym scope; implementacja defensywna nie udostępnia nieograniczonego skanowania celów zewnętrznych.

## 15. G0DM0D3 privacy and metering as model governance

G0DM0D3 rozdziela lokalną historię, metadane telemetryczne, opcjonalny dataset i provider-side logs; standalone UI nie zawiera w telemetry świadomie promptów, odpowiedzi, obrazów ani kluczy. fileciteturn116file0L1-L2

Dodatkowo voiceCost.js pokazuje dojrzały pattern: tier żądany przez klienta nie jest źródłem prawdy dla rozliczenia; metering opiera się na modelu faktycznie uruchomionym, a nieznany model jest liczony konserwatywnie. fileciteturn136file0L2-L2

OmniCore invariant:

`ACTUAL EXECUTION IDENTITY > REQUESTED LABEL`

To należy stosować do modeli, narzędzi, regionów, runtime tierów i kosztu.

## 16. Repository Intelligence Fabric — new synthesis

Połączenie G0DM0D3 + God's Eye View + Ghost/NEXUS-EYE prowadzi do nowej warstwy **Repository Intelligence Fabric (RIF)**:

```text
REPO GRAPH
  ├─ files
  ├─ symbols
  ├─ imports
  ├─ tests
  ├─ CI
  ├─ issues/PRs
  └─ runtime telemetry

WORLD / OBSERVATION GRAPH
  ├─ APIs
  ├─ devices
  ├─ browser state
  ├─ external data
  └─ evidence

             ↓
      CONTEXT COMPILER
             ↓
       AGENT REASONER
             ↓
     TYPED ACTION PLAN
             ↓
     CAPABILITY BROKER
             ↓
     EXECUTOR / SANDBOX
             ↓
     AUTHORITATIVE READBACK
             ↓
     GRAPH DELTA + ARTIFACT
```

RIF staje się warstwą wspólną dla repozytorium, świata zewnętrznego i artefaktów.

## 17. New invariants

1. Prompt is a program specification, not a security boundary.
2. Persona changes reasoning style, never authorization.
3. Tool execution must be typed and schema-validated.
4. Action success requires verified postcondition.
5. Stale turns cannot overwrite newer state.
6. Multimodal perception is evidence with provenance and uncertainty.
7. Actual runtime/model identity determines metering.
8. Multi-model agreement is not proof when assumptions are correlated.
9. Network proxies must be allowlisted and SSRF-resistant.
10. Secrets should remain server-side; clients receive bounded ephemeral credentials.
11. State graphs must distinguish observation, inference, action and committed state.
12. Repository-scale coding requires inspect → modify → test → repair → verify, not single-shot generation.
13. Scientific/engineering conclusions require explicit constraints and stability checks.
14. Graph edges require provenance; visualization is not validation.
15. Safety gates cannot be lowered by dynamic prompt, persona or model selection.

## 18. Projects affected

- Project 13 — Agentic Software Factory
- Project 15 — Universal Research Orchestrator
- Project 16 — Prompt Laboratory & Evaluation Engine
- Project 17 — Adaptive Model Router
- Project 19 — Omniscience Research Orchestrator MAX
- Project 24 — Agentic Prompt Compiler & DSL
- Project 26 — OmniCore Trustworthy Kernel & Agentic Safety Lab
- Project 27 — OmniCore Compound Reasoning & Self-Consistency Engine
- Project 28 — OmniCore AI Foundry / Verified Code Generation
- Project 30 — OmniCore Sugra Evidence/OSINT Control Fabric
- Project 31 — OmniCore Sovereign Agent Operating Fabric MAX
- Project 32 — Deep OSINT Evidence Engine MAX
- Project 33 — Agentic App Builder & Delivery Control Plane MAX
- Project 35 — Context-Aware Intent & Agent Security Engine MAX
- Project 37 — Sovereign Edge AI Runtime & Zero-Cost Delivery Fabric MAX
- Project 38 — Sovereign Edge AI + Constraint-Aware Scientific Reasoning / stability work
- Project 39 — OmniCore Alibaba Cloud Agent Runtime & Cloud Fabric MAX
- Project 40 — OmniCore Agentic Development & Visual Intelligence Fabric MAX

## Strategic conclusion

Nowa warstwa nie polega na stworzeniu „większego agenta”. Polega na połączeniu **repozytoryjnej inteligencji, multimodalnego stanu świata, typed capabilities, multi-model evaluation, deterministycznego execution, postcondition verification, cost governance i evidence graphs** w jeden spójny control fabric.
