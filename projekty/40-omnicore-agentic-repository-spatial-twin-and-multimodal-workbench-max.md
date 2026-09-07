# 40 — OmniCore Agentic Repository & Spatial Twin Workbench MAX

## Cel projektu

Zbudować wspólną warstwę `Digital Twin + Agentic Workbench`, która unifikuje dwa wcześniej rozdzielone światy:

1. **Repository Twin** — świadoma struktury kodu, zależności, testów, artefaktów, ryzyk i historii wykonania;
2. **Spatial Twin** — świadoma stanu sceny 3D, obiektów, warstw danych, źródeł, trajektorii, adnotacji i wieku danych.

Wzorzec wynika z połączenia architektur `G0DM0D3`, `God's Eye View`, agentic coding environments, generative UI oraz istniejących granic bezpieczeństwa OmniCore.

## Fundamentalna architektura

```text
                    OMNICORE CONTROL PLANE
                             ↓
                 TWIN STATE / CONTEXT GRAPH
                    ↙                 ↘
             REPOSITORY TWIN       SPATIAL TWIN
                    ↓                 ↓
             CONTEXT SNAPSHOT   SCENE SNAPSHOT
                    \                 /
                     ↓               ↓
                 PLANNER / REASONER
                          ↓
                 CAPABILITY BROKER
                          ↓
             TOOLS / MCP / CODE / UI / DATA
                          ↓
                 OBSERVE + VERIFY
                          ↓
                 UPDATE TWIN STATE
                          ↓
                    VERSIONED ARTIFACT
```

## 1. Repository Twin

Repository Twin jest maszynowo odczytywalnym grafem repozytorium.

```yaml
RepositoryTwin:
  repository_id:
  revision:
  files: []
  symbols: []
  dependencies: []
  tests: []
  build_targets: []
  generated_artifacts: []
  security_findings: []
  ownership: []
  open_work: []
  execution_history: []
  provenance:
    commit_sha:
    generated_at:
```

Agent nie powinien czytać całego repozytorium w każdym kroku. Tworzy task-specific snapshot obejmujący tylko wymagany podgraf.

## 2. Spatial Twin

Spatial Twin przechowuje jawny stan świata przedstawianego przez aplikację.

```yaml
SpatialTwin:
  scene_id:
  timestamp:
  camera:
  viewport:
  layers: []
  entities: []
  tracked_entity:
  selected_entity:
  annotations: []
  trajectories: []
  source_epochs: {}
  weather:
  provenance: []
  confidence:
```

Każdy fakt przestrzenny zachowuje `source`, `fetched_at`, `observed_at`, `fresh_until`, `quality` i `uncertainty`.

## 3. Agent Context Snapshot

Twin nie jest bezpośrednio przekazywany modelowi. Kontroler tworzy ograniczony snapshot:

```yaml
ContextSnapshot:
  task_id:
  goal:
  selected_subgraph:
  relevant_entities:
  relevant_files:
  current_state:
  constraints:
  policy:
  evidence_refs:
  freshness:
  token_budget:
```

To łączy istniejące zasady Projects 17, 27, 30, 32 i 35: kontekst jest dynamiczny, zadaniowy, wersjonowany i ograniczony.

## 4. State-aware intent

Intent staje się funkcją nie tylko wiadomości użytkownika, lecz także aktualnego twin state:

`INTENT = f(message, conversation, twin_state, environment, policy)`

Przykład klasycznego błędu:

```text
"zaznacz ten samolot"
```

jest niejednoznaczne bez:

- selected entity;
- tracked entity;
- camera state;
- active layer;
- scene timestamp.

Agent musi rozwiązać referencję względem jawnego stanu, a nie zgadywać.

## 5. Agentic coding loop

```text
TASK
 ↓
DISCOVER REPOSITORY SUBGRAPH
 ↓
PLAN
 ↓
EDIT / COMMAND
 ↓
BUILD / TEST
 ↓
DEBUG
 ↓
VERIFY
 ↓
UPDATE REPOSITORY TWIN
```

Cursor opisuje tryb Agent jako autonomiczną eksplorację kodu, edycję wielu plików, wykonanie poleceń terminala, testowanie i samodzielne poprawki. Claude Code stosuje podobną pętlę `gather context → take action → verify results`. citeturn327784search3turn970672search6

OmniCore nie ufa jednak agentowi programistycznemu. Wynik przechodzi przez Project 28.

## 6. Spatial action loop

```text
VOICE / TEXT / VISION
 ↓
SCENE SNAPSHOT
 ↓
PLAN
 ↓
CAPABILITY CHECK
 ↓
ACTION PREVIEW
 ↓
EXECUTE
 ↓
OBSERVE
 ↓
GEOSPATIAL / SOURCE VALIDATION
 ↓
UPDATE SPATIAL TWIN
```

God's Eye View pokazuje praktycznie ten wzorzec: agent pobiera kontekst bieżącej sceny, operuje na fixed app-control tools i traktuje feed-sourced text jako niezaufany kontekst. fileciteturn117file0L2-L2 fileciteturn118file0L2-L2

## 7. Capability Broker jako wspólny punkt kontroli

Zarówno kodowanie, jak i spatial control wymagają tej samej abstrakcji:

```yaml
CapabilityRequest:
  subject:
  capability:
  operation:
  resource:
  scope:
  purpose:
  expiry:
  risk:
  approval:
  provenance:
```

Przykłady:

```text
repo.write
repo.run_tests
repo.install_dependency
spatial.track_entity
spatial.draw_annotation
spatial.change_camera
spatial.export_snapshot
provider.call
browser.click
```

## 8. Repository sandbox policy

Każdy coding task otrzymuje izolowane środowisko:

```text
MAIN REPO
 ↓
ISOLATED WORKSPACE / BRANCH
 ↓
AGENT
 ↓
TESTS + SECURITY GATES
 ↓
REVIEW
 ↓
MERGE
```

Równoległe agenty mogą pracować nad osobnymi workspaces. Merge jest jedyną ścieżką promocji do wspólnego stanu.

## 9. Spatial sandbox policy

Analogiczna izolacja dla świata 3D:

```text
LIVE SCENE
 ↓
EPHEMERAL ACTION STATE
 ↓
AGENT EXPERIMENT
 ↓
VALIDATION
 ↓
COMMIT ANNOTATION / ARTIFACT
```

Agent może testować widok lub transformację bez automatycznego nadpisania trwałego stanu użytkownika.

## 10. Provenance-aware multimodality

Wszystkie kanały wejściowe są traktowane jednolicie:

```text
TEXT
IMAGE
SCREENSHOT
DOM
AUDIO
VIDEO
CODE
LIVE FEED
        ↓
UNTRUSTED INPUT
        ↓
PROVENANCE / CLASSIFICATION
        ↓
CONTEXT SNAPSHOT
```

Dane przestrzenne nie otrzymują uprzywilejowania dlatego, że są wizualne, a kod nie otrzymuje uprzywilejowania dlatego, że został wygenerowany przez agenta.

## 11. Fail-soft spatial intelligence

God's Eye View rozdziela stany `fresh`, `partial`, `stale`, `degraded` i `unavailable`, stosuje cache oraz źródła zapasowe. fileciteturn121file0L2-L2

OmniCore formalizuje:

```text
UNKNOWN
≠
STALE
≠
DEGRADED
≠
VERIFIED
```

Żaden agent nie może wykonać wysokiego ryzyka action na podstawie stanu `unknown` tylko dlatego, że model jest pewny językowo.

## 12. Source-aware licensing

God's Eye View pokazuje, że kod i dane mogą mieć różne licencje, a dynamiczna atrybucja zależy od aktywowanej warstwy danych. fileciteturn121file0L2-L2 fileciteturn122file0L2-L2

Dlatego każdy Twin artifact posiada:

```yaml
LicenseState:
  source:
  license:
  attribution:
  redistribution:
  commercial_use:
  jurisdiction:
  expiry:
```

Release gate może odrzucić artefakt, jeśli użyte dane/asset nie spełniają polityki dystrybucji.

## 13. Generative UI as Twin renderer

Generative UI nie jest kolejnym źródłem prawdy. Jest rendererem stanu Twin.

```text
AUTHORITATIVE STATE
        ↓
UI MANIFEST
        ↓
GENERATIVE UI
        ↓
HUMAN / AGENT INTERACTION
        ↓
COMMAND
        ↓
CAPABILITY BROKER
```

Vercel v0 pokazuje prompt-to-React/Tailwind/shadcn generowanie komponentów, Framer pozwala agentowi pracować na edytowalnym canvasie, a Webflow AI łączy budowanie, edycję, CMS, code components i optymalizację. citeturn970672search2turn970672search0turn970672search10

Project 33 powinien więc generować UI z Application Manifest, ale nie oddawać UI prawa do samodzielnej zmiany authoritative state.

## 14. G0DM0D3-inspired cognition workbench

G0DM0D3 pokazuje wzorzec wielomodelowego race + scoring + local/provider-neutral execution. fileciteturn116file0L2-L2

W Agentic Twin Workbench każdy większy problem może otrzymać kilka solverów:

```text
DIRECT
DECOMPOSED
ADVERSARIAL
RETRIEVAL-GROUNDED
ALTERNATIVE MODEL
        ↓
COMPARISON
 ↓
DISAGREEMENT CLUSTERS
 ↓
EVIDENCE CHECK
 ↓
FINAL PLAN
```

Wielomodelowy konsensus pozostaje heurystyką, nigdy dowodem.

## 15. Security-sensitive proxy pattern

God's Eye View stosuje allowlisted upstreams, brak arbitrary URL fetch, limity rozmiaru, timeouty, walidację DNS/adresów oraz inne zabezpieczenia SSRF. fileciteturn118file0L2-L2

Każdy Twin connector powinien dziedziczyć ten kontrakt:

```yaml
ConnectorPolicy:
  endpoint_allowlist:
  redirect_policy: deny|restricted
  dns_policy:
  max_response_bytes:
  timeout_ms:
  cache_ttl:
  rate_limit:
  data_classification:
  audit_level:
```

## 16. Provenance ledger

Każda zmiana Twin ma append-only event:

```yaml
TwinEvent:
  event_id:
  twin_id:
  parent_revision:
  actor:
  actor_type: human|agent|system
  capability:
  input_refs: []
  output_refs: []
  policy_decision:
  evidence_refs: []
  source_epochs: {}
  diff:
  verification_status:
  timestamp:
```

Dzięki temu można odtworzyć nie tylko co agent zrobił, ale na jakim stanie repozytorium/świata i na jakich źródłach działał.

## 17. Evaluation matrix

### Repository

- context selection accuracy;
- symbol/dependency graph accuracy;
- patch correctness;
- compile pass rate;
- test pass rate;
- regression rate;
- reproducibility;
- security policy bypass rate.

### Spatial

- entity identification accuracy;
- geospatial transform accuracy;
- source freshness compliance;
- annotation correctness;
- track stability;
- provenance coverage;
- stale-data disclosure rate.

### Combined agent

- intent grounding accuracy;
- capability authorization correctness;
- state integrity;
- rollback success;
- audit completeness;
- human intervention correctness;
- cost/latency/quality frontier.

## 18. Integration with existing projects

```text
P15  Research Orchestrator
 ↓
P17  Adaptive Model Router
 ↓
P26  Trust Kernel
 ↓
P27  Compound Reasoning
 ↓
P28  Verified Code Generation
 ↓
P30  Evidence / OSINT Fabric
 ↓
P31  Agent Operating Fabric
 ↓
P32  Deep OSINT
 ↓
P33  App Builder
 ↓
P35  Intent Security
 ↓
P37  Edge Runtime
 ↓
P39  Alibaba Cloud Fabric
 ↓
P40  Repository + Spatial Twin Workbench
```

## 19. Hard invariants

1. Twin state is context, not authorization.
2. Model output is never authoritative state by itself.
3. Multi-model agreement is not proof.
4. Every action is capability-scoped.
5. Persistent state is privileged.
6. Repository changes require verification before promotion.
7. Spatial facts require source provenance and freshness.
8. Degraded state must remain visible.
9. UI is a renderer/interaction layer, not the source of truth.
10. Licensing and attribution are machine-readable policy inputs.
11. Parallel agent work requires isolated workspaces.
12. All consequential Twin mutations are auditable and reversible.
13. Provider and runtime implementations remain replaceable.
14. Red-team mechanisms remain evaluation-only.
15. High-consequence external actions remain outside unattended authority.

## Definition of Done

- Repository Twin graph builder;
- Spatial Twin state engine;
- task-scoped Context Snapshot compiler;
- unified Capability Broker bindings;
- isolated repository workspaces;
- ephemeral spatial action state;
- provenance ledger;
- source freshness engine;
- license/attribution policy engine;
- multi-model comparison workbench;
- generative UI renderer over authoritative Twin state;
- regression/evaluation suite;
- edge/cloud adapters;
- rollback/resume semantics;
- observability and audit integration.

## Status

**Architecture / implementation blueprint.** Project 40 is intentionally provider-neutral. `G0DM0D3` and `God's Eye View` are treated as architectural evidence and reusable patterns, not as authorities on security, truth or production readiness.
