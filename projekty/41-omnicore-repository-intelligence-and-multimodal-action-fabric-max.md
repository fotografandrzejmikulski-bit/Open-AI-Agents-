# 41 — OmniCore Repository Intelligence & Multimodal Action Fabric MAX

## Thesis

Zbudować wspólną warstwę wykonawczą dla agentów programistycznych, badawczych i multimodalnych: **Repository Intelligence Fabric (RIF)**. System ma rozumieć repozytorium jako graf, stan świata jako osobny graf, a następnie kompilować oba do minimalnego, zweryfikowanego kontekstu i planu działania.

Projekt łączy wzorce z G0DM0D3, God's Eye View, Ghost Protocol, NEXUS-EYE oraz istniejących projektów OmniCore. Źródła pokazują odpowiednio: multi-model racing i adaptive execution, deterministyczny action runner z authoritative readback, ACL/OODA, grafowe łączenie obserwacji oraz fusion intelligence. fileciteturn116file0L1-L2 fileciteturn123file0L1-L2 fileciteturn134file0L10-L32 fileciteturn133file8L61-L75

## Fundamental architecture

```text
                         USER / OPERATOR
                                ↓
                       INTENT / REQUIREMENTS
                                ↓
                    ┌───────────┴───────────┐
                    │    CONTEXT COMPILER   │
                    └───────────┬───────────┘
                                ↓
          ┌─────────────────────┼─────────────────────┐
          │                     │                     │
     REPOSITORY GRAPH      WORLD STATE GRAPH      EVIDENCE GRAPH
          │                     │                     │
          └─────────────────────┼─────────────────────┘
                                ↓
                         AGENT REASONER
                                ↓
                       TYPED ACTION PLAN
                                ↓
                       CAPABILITY BROKER
                                ↓
                DETERMINISTIC EXECUTOR / SANDBOX
                                ↓
                  AUTHORITATIVE READBACK
                                ↓
                 POSTCONDITION VERIFICATION
                                ↓
             GRAPH DELTA + ARTIFACT + TELEMETRY
                                ↓
                    EVAL / RELEASE / ROLLBACK
```

## 1. Repository Graph

RIF materializuje repozytorium jako graf:

```yaml
RepositoryNode:
  id:
  kind: file|directory|symbol|test|workflow|issue|pr|artifact
  path:
  language:
  version:
  provenance:

RepositoryEdge:
  from:
  to:
  kind: imports|calls|tests|generates|documents|depends_on|fails_with
  confidence:
  provenance:
```

Graf nie jest budowany wyłącznie z nazw plików. Źródłem prawdy mogą być AST, package manifests, lockfiles, compiler output, test reports, CI logs i runtime telemetry.

## 2. Context Compiler

Zamiast wysyłać całe repozytorium do modelu, system kompiluje minimalny kontekst:

```text
INTENT
 ↓
AFFECTED SYMBOLS
 ↓
DEPENDENCY NEIGHBORHOOD
 ↓
RELEVANT TESTS
 ↓
BUILD / CI STATE
 ↓
RECENT FAILURES
 ↓
SECURITY / POLICY CONSTRAINTS
 ↓
MINIMAL CONTEXT PACK
```

Pozwala to ograniczyć token cost i jednocześnie zwiększyć deterministyczność wyboru materiału.

## 3. Coding-agent lifecycle

Canonical loop:

```text
DISCOVER
 ↓
HYPOTHESIS
 ↓
PLAN
 ↓
PATCH
 ↓
BUILD
 ↓
TEST
 ↓
OBSERVE FAILURE
 ↓
REPAIR
 ↓
RE-TEST
 ↓
VERIFY
 ↓
COMMIT
```

Agent nie uznaje kodu za ukończony tylko dlatego, że generacja zakończyła się bez błędu modelu.

## 4. Deterministic Action Runner

Wzorzec God's Eye View pokazuje wartość ograniczonego action runnera: jawne action names, normalizacja parametrów, kontrola aktywnego turnu, cancellation i odczyt rzeczywistego stanu po operacji. fileciteturn124file0L1-L2 fileciteturn125file0L1-L2

RIF przyjmuje:

```yaml
Action:
  id:
  capability:
  arguments_schema:
  preconditions:
  postconditions:
  side_effect_class:
  timeout:
  cost_limit:
  authorization:
```

Wywołanie jest skuteczne tylko gdy `postconditions == verified`.

## 5. Supersession and stale-turn protection

Każdy turn ma własną tożsamość i bazową wersję stanu:

```yaml
Turn:
  turn_id:
  parent_state_version:
  status:
  requested_actions:
  completed_actions:
  state_delta:
  superseded_by:
```

Commit do trwałego stanu jest blokowany, gdy baza jest nieaktualna i nie istnieje jawna strategia merge.

To zabezpiecza przed sytuacją, w której starszy agent nadpisuje efekt nowszej instrukcji.

## 6. Multimodal World Graph

RIF nie jest tylko coding agentem. Obsługuje również stan z kamery, screenshotu, przeglądarki, mapy, telemetry data, audio/video i innych źródeł.

```yaml
Observation:
  source:
  timestamp:
  modality:
  payload_ref:
  confidence:
  uncertainty:
  provenance:
  freshness:
```

Screenshot/OCR/DOM są obserwacjami, nie autorytetami polityki. Źródła God's Eye View wskazują, że viewport-image jest kontekstem best-effort, a app-control pozostaje ograniczone do stałego zestawu narzędzi. fileciteturn121file0L8-L17

## 7. Evidence graph

Wzorzec NEXUS-EYE/PAULA OS jest generalizowany do grafu dowodowego, w którym każdy node/edge ma źródło i confidence. NEXUS-EYE zapisuje węzły i połączenia między nimi, a PAULA OS scala wiele źródeł w Fusion Intelligence. fileciteturn133file8L21-L29 fileciteturn134file2L139-L151

Canonical relation:

`OBSERVATION → EVIDENCE → INFERENCE`

nigdy:

`VISUALIZATION → TRUTH`.

## 8. Multi-model comparative reasoning

G0DM0D3 wprowadza równoległe wyścigi modeli i scoring odpowiedzi. fileciteturn116file0L1-L2

RIF implementuje:

```text
TASK
 ↓
MODEL ROUTER
 ├─ specialist A
 ├─ specialist B
 ├─ local model
 └─ verifier model
 ↓
NORMALIZE
 ↓
SCORE
 ↓
DISAGREEMENT CLUSTERING
 ↓
VERIFY / ESCALATE
```

Scoring nie daje prawa do side-effect. Jest jednym sygnałem w procesie wyboru.

## 9. Adaptive execution profiles

G0DM0D3 pokazuje AutoTune jako adaptację parametrów inferencji względem kontekstu oraz feedback loop jako mechanizm EMA. fileciteturn119file0L1-L2

RIF rozszerza to do:

```yaml
ExecutionProfile:
  task_class:
  reasoning_budget:
  model_set:
  sampling_policy:
  latency_target:
  cost_ceiling:
  context_budget:
  verification_level:
  safety_level:
```

Profil może zwiększyć rygor ewaluacji, ale nie może obniżyć obligatoryjnych policy gates.

## 10. Prompt Compiler integration

Nowe materiały o unikalnych promptach wzmacniają Project 24: prompt traktujemy jako specyfikację programu z rolą, kontekstem, ograniczeniami, metodą, kontraktem wyjścia i iteracyjną ewaluacją. fileciteturn133file0L17-L31

RIF compiler pipeline:

```text
NATURAL LANGUAGE
 ↓
INTENT MODEL
 ↓
TASK CLASS
 ↓
REASONING PROFILE
 ↓
CONSTRAINTS
 ↓
OUTPUT / ACTION CONTRACT
 ↓
EVAL PLAN
```

Persona i mental model wpływają na sposób rozumowania, ale nigdy na authorization.

## 11. Scientific stability / perturbation gate

Wzorce stabilności z raportu fizyka–medycyna–optymalizacja są uogólniane do systemów agentowych: przed zaakceptowaniem rozwiązania sprawdzane są constraints, sensitivity i stability. fileciteturn134file4L251-L270

```text
SOLUTION
 ↓
CONSTRAINT CHECK
 ↓
SENSITIVITY / PERTURBATION
 ↓
STABILITY
 ↓
COUNTEREXAMPLE SEARCH
 ↓
ACCEPT / ESCALATE
```

`UNKNOWN` nie jest traktowane jako `PASS`.

## 12. Cost governance based on actual execution identity

God's Eye View i G0DM0D3 pokazują dojrzałe metering patterns. Szczególnie voiceCost.js wiąże rozliczenie z modelem faktycznie wykonującym sesję, a nie z aliasem wybranym przez klienta. fileciteturn136file0L2-L2

RIF invariant:

```text
REQUESTED MODEL LABEL
        ≠
ACTUAL MODEL ID
        ↓
ACTUAL COST / USAGE
```

To samo dotyczy runtime, regionu, capability i wersji Skill.

## 13. Secure network/tool boundary

God's Eye View ogranicza sekretne klucze do serwera i stosuje allowlisted proxy, SSRF protections, timeouty, response-size limits i rate limits. fileciteturn122file0L2-L2

RIF wszystkie zewnętrzne działania prowadzi przez Capability Broker:

```text
MODEL
 ↓
CAPABILITY REQUEST
 ↓
SCOPE / AUTHORIZATION
 ↓
DESTINATION ALLOWLIST
 ↓
BUDGET / RATE LIMIT
 ↓
EXECUTOR
 ↓
SANITIZE
 ↓
VERIFY
 ↓
AUDIT
```

## 14. Ghost ACL hardening

Ghost Protocol używa specjalnego markera tekstowego do zamawiania skanu, po czym backend interpretuje marker i wykonuje narzędzie. fileciteturn134file1L71-L104

RIF zachowuje ideę backendowego intent execution, ale zastępuje parser tekstowy typed tool schema i policy enforcement.

Dla aktywnego network reconnaissance obowiązuje explicit scope, authorization, rate limiting i audyt. System nie uznaje modelowego żądania za samowystarczającą zgodę na działanie wobec zewnętrznego celu.

## 15. Persistence and checkpointing

Każdy większy task zapisuje:

```yaml
Checkpoint:
  run_id:
  repository_version:
  world_state_version:
  evidence_refs:
  context_hash:
  plan_hash:
  completed_steps:
  pending_steps:
  verification_state:
  artifacts:
```

Po awarii agent może wznowić pracę bez udawania, że poprzedni krok został wykonany.

## 16. Error taxonomy

RIF rozróżnia:

- model error;
- context error;
- tool selection error;
- authorization denial;
- execution failure;
- stale-state conflict;
- postcondition failure;
- provenance failure;
- evaluator disagreement;
- budget exhaustion;
- provider/runtime outage.

Każdy typ błędu ma osobną strategię recovery.

## 17. Security and trust boundary

```text
AI MODEL
  ↓ untrusted plan
CAPABILITY BROKER
  ↓ authorized action
DETERMINISTIC EXECUTOR
  ↓ observable effect
VERIFIER
  ↓ committed state
```

AI nie należy do trusted computing base. Model może proponować, ale nie może sam sobie nadać uprawnień, potwierdzić side-effect bez readback ani obniżyć policy.

## 18. Evaluation suite

### Coding
- repo navigation accuracy;
- patch correctness;
- build success;
- test repair rate;
- regression rate;
- security-gate bypass rate.

### Multimodal
- scene grounding accuracy;
- false-label rate;
- state readback accuracy;
- stale-action suppression;
- tool postcondition accuracy.

### Multi-model
- winner stability;
- correlated-error rate;
- cost/successful task;
- escalation precision;
- disagreement recovery.

### Security
- unauthorized action rate;
- SSRF block rate;
- secret exposure rate;
- stale-turn overwrite rate;
- provenance coverage.

## 19. Integration map

Project 13 → coding factory
Project 15/19 → research orchestration
Project 17 → adaptive model routing
Project 24 → prompt compiler / DSL
Project 26 → trust kernel / capability broker
Project 27 → compound reasoning
Project 28 → verified code generation
Project 30/32 → evidence / OSINT
Project 31 → agent operating fabric
Project 33 → application delivery
Project 35 → contextual intent security
Project 37 → edge/cloud runtime
Project 38 → scientific stability verification
Project 39 → Alibaba Cloud execution fabric
Project 40 → agentic development + visual intelligence

## 20. Definition of Done

- repository graph builder;
- context compiler;
- typed action schema;
- capability broker integration;
- deterministic executor;
- authoritative readback;
- postcondition verifier;
- stale-turn protection;
- multimodal observation schema;
- evidence graph integration;
- multi-model race/evaluator;
- adaptive execution profiles;
- actual-identity metering;
- checkpoint/resume;
- security and provenance audit;
- CI/test integration;
- release and rollback gates.

## Strategic result

Project 41 nie tworzy kolejnego „coding agenta”. Tworzy **warstwę inteligencji wykonawczej**, w której repozytorium, świat zewnętrzny, wiedza i artefakty mają jawny stan; modele mogą być wymieniane; capabilities są autoryzowane niezależnie; a każda konsekwencjalna akcja kończy się authoritative readback i weryfikacją.
