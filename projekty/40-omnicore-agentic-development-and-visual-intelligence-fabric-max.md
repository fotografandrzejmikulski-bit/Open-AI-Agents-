# 40 — OmniCore Agentic Development & Visual Intelligence Fabric MAX

## Cel projektu

Zbudować provider-neutral warstwę wykonawczą łączącą dwa typy agentów, które dotąd często rozwijają się osobno:

1. **repo-scale coding agents** — rozumienie całych repozytoriów, planowanie zmian wieloplikowych, terminal execution, build/test/debug/repair oraz release;
2. **stateful multimodal environment agents** — praca na dynamicznym stanie świata/aplikacji, danych geospatial/live, obrazie ekranu, voice/realtime i deterministycznych akcjach.

Projekt wykorzystuje wzorce zaobserwowane w G0DM0D3 i God's Eye View oraz integruje je z Projects 13, 17, 26, 27, 28, 30, 31, 32, 33, 37 i 39.

---

## Fundamental architecture

```text
                         OMNICORE CONTROL PLANE
                                   │
        ┌──────────────────────────┼──────────────────────────┐
        ↓                          ↓                          ↓
 REPOSITORY GRAPH             WORLD STATE GRAPH        KNOWLEDGE/EVIDENCE
        │                          │                          │
        ↓                          ↓                          ↓
 CODING AGENTS               MULTIMODAL AGENTS          RESEARCH AGENTS
        │                          │                          │
        └──────────────────────┬───┴───┬──────────────────────┘
                               ↓
                     TYPED CAPABILITY BROKER
                               ↓
                  VERIFY → EXECUTE → OBSERVE
                               ↓
                     ARTIFACT / STATE DELTA
                               ↓
                    EVALUATION + PROVENANCE
```

Zasada nadrzędna:

`AGENT BRAIN != ACTION ENGINE != UI`

Żadna z tych warstw nie jest automatycznie trusted computing base.

---

## 1. Repository Graph

Coding agent nie powinien otrzymywać repozytorium wyłącznie jako zbioru plików ani pojedynczych fragmentów wyszukanych semantycznie. Potrzebuje jawnego grafu zależności.

```yaml
RepositoryNode:
  path:
  language:
  symbol:
  module:
  exports:
  imports:
  tests:
  build_targets:
  ownership:
  provenance:
  version:

RepositoryEdge:
  kind: import|call|inherit|config|generated_by|tested_by|deploys_to
  source:
  target:
  confidence:
```

Minimalny indeks powinien łączyć:

`FILES → SYMBOLS → MODULES → DEPENDENCIES → TESTS → BUILD TARGETS → RELEASE ARTIFACTS`.

To rozszerza Project 28 o jawny **repository state model**.

---

## 2. Coding-agent execution loop

```text
USER INTENT
 ↓
REQUIREMENTS / CONTRACT
 ↓
REPOSITORY GRAPH QUERY
 ↓
PLAN
 ↓
READ-ONLY INSPECTION
 ↓
PATCH SET
 ↓
PARSE / TYPE / EFFECT CHECK
 ↓
BUILD
 ↓
TEST
 ↓
FAILURE CLASSIFICATION
 ↓
REPAIR LOOP
 ↓
SECURITY / POLICY GATE
 ↓
SIGNED ARTIFACT
```

Agent nie otrzymuje implicit permission do dowolnego zapisu tylko dlatego, że ma dostęp do workspace.

Każde narzędzie powinno deklarować:

```yaml
CodeCapability:
  id:
  version:
  operation: read|write|rename|delete|execute|build|test|deploy
  paths:
  side_effects:
  required_approval:
  timeout:
  resource_limit:
  rollback_mode:
  audit_id:
```

---

## 3. World State Graph

God's Eye View pokazuje drugi rodzaj problemu: agent steruje żywym środowiskiem, w którym stan zmienia się niezależnie od dialogu.

```yaml
WorldStateSnapshot:
  timestamp:
  viewport:
  entities:
  layers:
  feeds:
  annotations:
  environment:
  selected_entity:
  active_modes:
  provenance:
  uncertainty:
```

Model powinien dostawać **aktualny, przefiltrowany snapshot**, a nie wierzyć bezwarunkowo pamięci rozmowy.

Wariant kanoniczny:

```text
WORLD STATE
 ↓
AUTHORITATIVE SNAPSHOT
 ↓
CONTEXT SELECTION
 ↓
MODEL
 ↓
TYPED ACTION
 ↓
STATE TRANSITION
 ↓
AUTHORITATIVE READBACK
```

---

## 4. Typed Action Runner

Wzorzec zaczerpnięty z deterministycznego action layer GEV: sukces narzędzia nie może oznaczać jedynie „setter został wywołany”. Po wykonaniu należy odczytać rzeczywisty stan i sprawdzić postcondition. fileciteturn124file0L1-L2 fileciteturn125file0L1-L2

```text
PARSE
 ↓
NORMALIZE
 ↓
AUTHORIZE
 ↓
EXECUTE
 ↓
WAIT FOR SETTLEMENT
 ↓
READ AUTHORITATIVE STATE
 ↓
VERIFY POSTCONDITION
 ↓
REPORT FACTUAL RESULT
```

Każda odpowiedź narzędzia powinna rozróżniać:

`requested ≠ accepted ≠ started ≠ settled ≠ verified`.

---

## 5. Turn Ownership Controller

Wieloetapowe agenty muszą rozumieć, że wynik może stać się nieaktualny podczas wykonywania.

GEV utrzymuje aktywną odpowiedź, superseded response IDs, abort controllers i mechanizmy deduplikacji. fileciteturn123file0L1-L2

OmniCore modeluje to jawnie:

```yaml
Turn:
  id:
  parent_session:
  status: active|superseded|cancelled|completed|failed
  authority_epoch:
  started_at:
  expires_at:
  side_effect_budget:
```

Reguła:

`SUPERSEDED TURN MUST NOT AUTHORITATIVELY CONFIRM NEWER STATE.`

In-flight side effects są klasyfikowane jako:

- reversible → rollback/compensate;
- idempotent → safe retry;
- non-idempotent → complete + reconcile;
- irreversible → approval boundary.

---

## 6. Multimodal Evidence Layer

Screenshot, DOM, OCR, files, scene telemetry i network-derived text nie są prawdą samą w sobie. Są observations z provenance.

```yaml
Observation:
  id:
  modality: text|image|audio|video|dom|telemetry|file
  source:
  captured_at:
  transformation_chain:
  content_hash:
  confidence:
  readability:
  corroboration:
  authorization_scope:
```

GEV jawnie ogranicza wizualne odpowiedzi do treści, które są czytelne, i nakazuje unikać halucynowania etykiet. fileciteturn117file0L1-L2

Zasada:

`UNREADABLE ≠ TRUE`

`MODEL CONFIDENCE ≠ SENSOR CONFIDENCE`

---

## 7. Ephemeral Credential Broker

GEV utrzymuje prywatne klucze po stronie serwera i dla Realtime wydaje przeglądarce krótkotrwały token sesyjny zamiast prawdziwego klucza. fileciteturn122file0L1-L2

OmniCore generalizuje:

```text
UI / AGENT
 ↓
PURPOSE-BOUND REQUEST
 ↓
POLICY
 ↓
SHORT-LIVED CREDENTIAL
 ↓
PROVIDER
 ↓
REVOKE / EXPIRE
```

Credential grant zawiera:

```yaml
CredentialGrant:
  subject:
  capability:
  resource:
  purpose:
  scopes:
  issued_at:
  expires_at:
  audience:
  audit_id:
```

---

## 8. Network Capability Firewall

Security model GEV pokazuje konkretny wzorzec ochrony proxy: brak arbitrary-URL fetch, allowlisted upstream hosts, response-size caps, timeouty i sanitized errors. fileciteturn122file0L1-L2

OmniCore wymaga:

```yaml
NetworkCapability:
  destination_allowlist:
  scheme_allowlist:
  port_allowlist:
  dns_validation:
  redirect_policy:
  max_response_bytes:
  timeout_ms:
  rate_limit:
  egress_policy:
  audit_id:
```

`fetch(url)` bez ograniczeń nie jest dopuszczalnym primitive dla agenta uprzywilejowanego.

---

## 9. Multi-model evaluation fabric

G0DM0D3 dostarcza inference-time pattern, w którym wiele modeli może być uruchamianych równolegle, a odpowiedzi są normalizowane, oceniane i porównywane. README oraz PAPER przedstawiają ULTRAPLINIAN jako równoległy multi-model evaluation engine, a AutoTune jako warstwę adaptacji parametrów inferencji. fileciteturn116file0L1-L2 fileciteturn119file0L1-L2

OmniCore integruje to jako opcjonalną ścieżkę:

```text
TASK
 ↓
SOLVER A ─┐
SOLVER B ─┼→ NORMALIZE → SCORE → DISAGREEMENT ANALYSIS
SOLVER C ─┘                           ↓
                                ACCEPT / ESCALATE
```

Nie wolno przyjmować „większość modeli się zgadza” jako dowodu, jeżeli wszystkie korzystają z tych samych danych, promptów i założeń.

---

## 10. Generalized AutoTune

G0DM0D3 używa klasyfikacji kontekstu do wyboru parametrów samplingowych. OmniCore rozszerza ten mechanizm na cały profil wykonania:

```yaml
ExecutionPolicyProfile:
  model_class:
  reasoning_budget:
  sampling:
  retrieval_depth:
  max_tool_calls:
  max_wall_time:
  verification_level:
  privacy_level:
  egress_level:
  cost_ceiling:
  escalation_policy:
```

Profil jest funkcją:

`intent × context × risk × latency_requirement × privacy × cost × capability availability`.

---

## 11. Actual-execution metering

G0DM0D3 `voiceCost.js` rozróżnia żądany tier od modelu faktycznie użytego. Dla nieznanego modelu stosowana jest konserwatywna stawka najdroższego znanego profilu, a spend guard ma soft warning i hard cap. fileciteturn128file0L1-L2

General rule:

`METER ACTUAL EXECUTION, NOT REQUESTED CONFIGURATION.`

Ta zasada dotyczy:

- tokenów;
- czasu GPU;
- egress;
- tool invocations;
- browser sessions;
- serverless calls;
- storage;
- realtime audio.

---

## 12. Agent-facing API Contract

G0DM0D3 udostępnia OpenAI SDK-compatible endpoint, feature gating, rate-limit headers i jawne tier limits. fileciteturn127file0L1-L2

OmniCore wprowadza wspólny kontrakt capability:

```yaml
CapabilityContract:
  id:
  version:
  inputs:
  outputs:
  side_effects:
  authorization:
  quotas:
  latency_slo:
  cost_model:
  failure_modes:
  verification:
  provenance:
```

Agent ma znać nie tylko „jak wywołać”, ale także **co operacja może zmienić**.

---

## 13. UI as projection, not authority

UI, voice i agent chat są projekcjami state'u. Nie stanowią źródła prawdy.

```text
AUTHORITATIVE STATE
 ├─ repository graph
 ├─ world state
 ├─ capability state
 ├─ policy state
 └─ artifact registry
          ↓
       VIEW / UI
```

To zapobiega klasie błędów, w której interfejs pokazuje stan wywnioskowany przez model zamiast stan zweryfikowany przez system.

---

## 14. Architecture for coding + visual agents

```text
                        USER / OPERATOR
                              ↓
                        INTENT COMPILER
                              ↓
                ┌──────── SPEC / POLICY ────────┐
                ↓                               ↓
        REPOSITORY GRAPH                  WORLD STATE GRAPH
                ↓                               ↓
        TASK / CODE AGENT                MULTIMODAL AGENT
                ↓                               ↓
          PLAN / PATCH                    PLAN / ACTION
                └──────────────┬────────────────┘
                               ↓
                     CAPABILITY BROKER
                               ↓
              ┌────────────────┼─────────────────┐
              ↓                ↓                 ↓
           FILE/CLI         WEB/UI          DATA/NETWORK
              ↓                ↓                 ↓
              └──────────── EXECUTION ───────────┘
                               ↓
                     POSTCONDITION CHECK
                               ↓
                 PROVENANCE / ARTIFACT LEDGER
                               ↓
                     EVALS / RELEASE GATE
```

---

## 15. Integration with Projects 13 and 28

Project 13 dostarcza software-factory loop. Project 28 dostarcza formalny verification boundary, effect system, reproducibility i staged rollout.

Project 40 dodaje brakującą warstwę **live operational state**:

`CODE STATE + WORLD STATE + TOOL STATE + POLICY STATE`.

Żaden agent nie może uznać artefaktu za gotowy, jeśli wymagany postcondition nie został sprawdzony.

---

## 16. Integration with Projects 17 and 27

Project 17 wybiera model/substrate na podstawie benchmarków. Project 27 wykonuje compound reasoning i disagreement analysis.

Project 40 dodaje telemetryczne cechy środowiska:

```text
MODEL
+ SOLVER PATH
+ CONTEXT SNAPSHOT
+ TOOL PATH
+ STATE VERSION
+ POLICY VERSION
+ ARTIFACT VERSION
```

Dzięki temu można odtworzyć nie tylko odpowiedź, ale **całą ścieżkę wykonania**.

---

## 17. Integration with Projects 37 and 39

Project 37 definiuje edge-to-cloud continuum. Project 39 dostarcza Alibaba Cloud jako konkretny substrate: Model Studio/Qwen, MCP, AgentBay, ACK, RAM/STS, OSS, SLS, ACR i ECS.

Project 40 jest warstwą ponad nimi:

```text
AGENT CONTRACT
 ↓
ROUTING
 ↓
LOCAL / EDGE / CLOUD
 ↓
SUBSTRATE-SPECIFIC ADAPTER
 ↓
VERIFY / OBSERVE
```

Provider nadal pozostaje substrate, a nie policy authority.

---

## 18. Security model

### Trust domains

1. Model cognition — untrusted.
2. Retrieved knowledge — untrusted until provenance checked.
3. Tool result — untrusted data until validated.
4. UI state — projection.
5. Action engine — deterministic boundary.
6. Capability Broker — authorization boundary.
7. Artifact verifier — promotion boundary.
8. Audit ledger — evidence boundary.

### Required controls

- least privilege;
- typed capabilities;
- short-lived credentials;
- allowlisted network egress;
- postcondition verification;
- turn supersession;
- sandboxing;
- rate/cost budgets;
- provenance;
- signed artifacts;
- rollback/compensation policy;
- immutable audit correlation.

---

## 19. Evaluation matrix

| Domain | Metrics |
|---|---|
| Repository understanding | symbol recall, dependency accuracy, relevant-context precision |
| Code modification | build success, test pass rate, regression rate |
| Debugging | diagnosis accuracy, mean repair iterations, time-to-green |
| Tool safety | unauthorized capability rate, policy bypass rate |
| State correctness | postcondition verification rate, stale-turn mutation rate |
| Multimodal grounding | observation accuracy, unsupported-claim rate |
| Network security | blocked SSRF rate, egress policy violations |
| Cost | cost/task, token/task, GPU-sec, egress/task |
| Reliability | recovery rate, retry success, rollback success |
| Reproducibility | artifact reproducibility, trace completeness |
| Multi-model reasoning | disagreement detection, correlated-error detection |

---

## 20. Core invariants added to OmniCore

39. Repository state must be modeled explicitly for repo-scale agents.
40. Dynamic world state must have an authoritative typed representation.
41. Agent success requires verified postcondition.
42. Requested execution is not equivalent to settled execution.
43. Superseded turns cannot authoritatively mutate or confirm newer state.
44. Agent-facing network access must be capability-scoped and allowlisted.
45. Multimodal observations require provenance and uncertainty.
46. Credentials should be short-lived, purpose-bound and audience-scoped.
47. Meter actual execution identity and usage, not requested configuration.
48. UI is a projection of authoritative state, not the authority itself.
49. Multi-model agreement is evidence, not proof, when solver paths are correlated.
50. Brain, action engine and UI remain separate trust domains.
51. Cloud/edge/local execution must share one policy contract.
52. Every consequential action needs a machine-checkable capability contract.

---

## Definition of Done

- Repository Graph indexer;
- World State Graph;
- typed Code/Browser/Data capabilities;
- deterministic postcondition-aware Action Runner;
- turn ownership/supersession controller;
- multimodal observation/provenance schema;
- ephemeral credential broker;
- network capability firewall;
- actual-execution cost metering;
- optional multi-model race/evaluation;
- Evaluation Ledger;
- integration with Projects 13/17/26/27/28/37/39;
- reproducible benchmarks.

## Status

**Architecture / implementation blueprint.** Wzorce z G0DM0D3 i God's Eye View są traktowane jako implementacyjne evidence, natomiast twierdzenia o „najpotężniejszym” agencie lub przewadze konkretnego produktu wymagają własnych benchmarków.
