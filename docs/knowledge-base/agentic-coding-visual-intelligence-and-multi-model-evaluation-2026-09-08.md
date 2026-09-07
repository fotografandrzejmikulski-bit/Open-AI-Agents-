# Agentic Coding, Visual Intelligence & Multi-Model Evaluation — Knowledge Synthesis

## Scope

Synteza obserwacji z `G0DM0D3`, `God's Eye View` oraz zestawienia współczesnych agentów: środowiska coding-agent, autonomiczne środowiska E2E, UI generation, web builders, game agents, Unity AI, MCP i realtime voice. Źródła repozytoryjne są traktowane jako implementacyjne wzorce i evidence; deklaracje marketingowe nie są automatycznie uznawane za benchmark.

## 1. G0DM0D3 — inference-time evaluation as a first-class subsystem

G0DM0D3 jest modularnym frameworkiem do badania zachowania LLM podczas inferencji. README opisuje pięć głównych mechanizmów: AutoTune, GODMODE/parallel model races, ULTRAPLINIAN multi-model evaluation, Parseltongue input perturbation oraz privacy/telemetry controls. Repozytorium udostępnia również lokalne modele przez Ollama/LM Studio/llama.cpp/vLLM oraz OpenAI-compatible endpoints. fileciteturn116file0L1-L2

PAPER doprecyzowuje architekturę: kontekst jest klasyfikowany przed generacją, parametry samplingowe mogą być adaptowane, wiele modeli może być uruchamianych równolegle, a wyniki są następnie porównywane i normalizowane. Framework został zaprojektowany bez dostępu do wag modelu, jako inference-time evaluation layer. fileciteturn119file0L1-L2

Wniosek dla OmniCore:

```text
MODEL CALL
 ↓
OBSERVE CONFIG
 ↓
OPTIONAL MULTI-MODEL RACE
 ↓
SCORE / CRITIQUE
 ↓
EVIDENCE + METRICS
 ↓
ROUTING / ACCEPTANCE DECISION
```

Najważniejsza lekcja nie dotyczy konkretnych promptów red-teamowych, lecz możliwości zbudowania **wymienialnej warstwy ewaluacyjnej na poziomie inferencji**, działającej ponad różnymi providerami.

## 2. AutoTune — context-aware execution parameters

G0DM0D3 klasyfikuje kontekst rozmowy, a następnie wybiera profil parametrów generacji. PAPER podaje pięć kategorii (`code`, `creative`, `analytical`, `conversational`, `chaotic`) i funkcję ważenia bieżącej wiadomości silniej niż starszych elementów historii. Dostępne są ograniczenia zakresów parametrów oraz blending z profilem bazowym przy niskiej pewności klasyfikacji. fileciteturn119file0L1-L2

OmniCore może uogólnić ten pattern z parametrów samplingowych do **ExecutionPolicyProfile**:

```yaml
ExecutionPolicyProfile:
  reasoning_budget:
  model_family:
  temperature:
  retrieval_depth:
  tool_budget:
  timeout:
  verification_level:
  escalation_policy:
```

To pozwala adaptować nie tylko generację, lecz cały koszt/ryzyko wykonania.

## 3. ULTRAPLINIAN — parallel model race

G0DM0D3 opisuje ULTRAPLINIAN jako równoległy wyścig wielu modeli, ranking odpowiedzi według jawnego composite score i zwracanie zwycięskiego wyniku. README wskazuje obecne pule modeli OpenRouter/Venice/local zależne od konfiguracji, a API udostępnia wirtualne modele typu `ultraplinian/fast`, `standard`, `smart`, `power`, `ultra`. fileciteturn116file0L1-L2 fileciteturn127file0L1-L2

W portfolio należy traktować to jako pattern **parallel candidate generation + explicit selection**, nie jako dowód, że większa liczba modeli zawsze poprawia wynik.

```text
TASK
 ↓
N CANDIDATE SOLVERS
 ↓
NORMALIZED OUTPUTS
 ↓
SCORING / CROSS-CHECK
 ↓
DISAGREEMENT ANALYSIS
 ↓
SELECT / ESCALATE
```

Łączy się bezpośrednio z Project 27 (compound reasoning) i Project 17 (adaptive routing).

## 4. Reproducible safety telemetry

G0DM0D3 rozdziela lokalną historię rozmów, operational telemetry i opcjonalny dataset collection. README podkreśla, że hosted telemetry zawiera metadane operacyjne i nie ma być nośnikiem promptów, odpowiedzi, obrazów ani kluczy; tryby No-Log i Local-only ograniczają ten przepływ. fileciteturn116file0L1-L2

PAPER przedstawia three-tier telemetry architecture oraz dane badawcze zbierane per request. fileciteturn119file0L1-L2

Architektoniczna lekcja:

```text
CONTENT
≠
OPERATIONAL METADATA
≠
OPTIONAL RESEARCH DATA
```

To wzmacnia wcześniejsze wymaganie rozdzielenia provenance, privacy i observability.

## 5. God's Eye View — live geospatial interface as an agent substrate

God's Eye View łączy photorealistic 3D globe z live aircraft, ships, satellites, earthquakes, traffic i public cameras, a także voice agentem korzystającym z realtime AI. README podkreśla, że większość danych działa lokalnie w browserze i że warstwy źródłowe są modularne. fileciteturn117file0L1-L2

Najważniejszym wzorcem nie jest militarna stylistyka HUD, tylko **stateful multimodal environment**:

```text
WORLD STATE
 ├─ entities
 ├─ geography
 ├─ live feeds
 ├─ camera/viewport state
 ├─ user annotations
 └─ visual mode
       ↓
AGENT CONTEXT
       ↓
TOOL ACTION
       ↓
STATE TRANSITION
       ↓
OBSERVE RESULT
       ↓
CONFIRM / CORRECT
```

To jest praktyczny przykład środowiska, w którym agent nie odpowiada tylko tekstem, lecz wykonuje deterministyczne operacje na bogatym stanie aplikacji.

## 6. Voice agent — live context beats giant conversation memory

God's Eye View przekazuje agentowi bieżący kontekst sceny, między innymi współrzędne, nazwy miejsc, aktywne warstwy i skalę widoku, a przy analizie na poziomie ulicznym może dołączyć viewport screenshot. README wskazuje również, że agent ma potwierdzać tylko akcje, które faktycznie się udały. fileciteturn117file0L1-L2

To wzmacnia wzorzec:

`LIVE STATE > STALE CONVERSATION MEMORY`

Wniosek: przy agentach sterujących dynamiczną aplikacją należy okresowo pobierać **authoritative current state**, zamiast polegać wyłącznie na pamięci dialogu.

## 7. Deterministic action runner and tool semantics

Kod `gevActions.js` pokazuje rozbudowany deterministic action layer. Narzędzia posiadają aliasy, normalizację argumentów, jawne stany anulowania, oczekiwanie na settlement zmian oraz weryfikację rzeczywistego stanu po wykonaniu. Przykładowo `set_layer_visibility` nie uznaje żądania za sukces tylko dlatego, że wywołano setter; sprawdzany jest finalny lifecycle state. fileciteturn124file0L1-L2 fileciteturn125file0L1-L2

Canonical OmniCore action pattern:

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
RETURN RESULT
```

To jest silniejsze niż samo `tool_call → ok:true` i powinno zostać utrzymane jako systemowy invariant.

## 8. Cancellation, supersession and race safety

`gevRealtime.js` zawiera jawne mechanizmy dla aktywnej odpowiedzi, superseded response IDs, abort controllers, deduplikację wywołań, graceful disconnect handling i ograniczenia rozmiaru viewport screenshots. fileciteturn123file0L1-L2

Lekcja:

```text
CURRENT TURN
 ↓
TOOL CALL
 ↓
MAY BECOME STALE
 ↓
ABORT / SUPERSEDE / COMPLETE
 ↓
ONLY CURRENT AUTHORITY MAY SPEAK
```

W agentach wieloetapowych **turn ownership** powinien być explicit. Późny wynik starego requestu nie może nadpisać nowszego stanu.

## 9. Ephemeral credentials and server-side secret brokerage

God's Eye View trzyma klucze prywatne po stronie serwera. Dla OpenAI browser pobiera krótkotrwały token sesji Realtime, a prawdziwy `OPENAI_API_KEY` nie trafia do przeglądarki. Podobne wzorce stosowane są dla innych prywatnych provider credentials. fileciteturn122file0L1-L2

Canonical security boundary:

```text
BROWSER / AGENT UI
      ↓
SHORT-LIVED EPHEMERAL CREDENTIAL
      ↓
SERVER-SIDE KEY BROKER
      ↓
PROVIDER
```

To bezpośrednio wzmacnia Projects 26, 31, 37 i 39.

## 10. SSRF and proxy hardening as agent security

Security model God's Eye View explicitly zabrania arbitrary-URL fetching przez proxy, stosuje allowlistę upstream hosts, limity rozmiaru/timeouty, sanityzację błędów oraz inne ograniczenia ruchu. fileciteturn122file0L1-L2

Wniosek: **agent-facing proxy APIs muszą być projektowane jako capability-restricted network functions**, a nie jako wygodne `fetch(url)`.

```yaml
NetworkCapability:
  destination_allowlist:
  protocols:
  ports:
  dns_policy:
  redirect_policy:
  max_response_bytes:
  timeout_ms:
  audit_id:
```

## 11. Local-first architecture with explicit exposure controls

God's Eye View domyślnie binduje serwer do localhost, a LAN exposure jest świadomym opt-in. Repozytorium rozdziela local development, provider-side spend protection i ewentualny zewnętrzny auth proxy. fileciteturn122file0L1-L2

To rozszerza zasadę Project 37:

`LOCAL-FIRST != LOCAL-TRUSTED`

Lokalna usługa nadal potrzebuje rate limits, capability scoping i ochrony sekretów.

## 12. Realtime voice cost governance

God's Eye View posiada osobny moduł kosztowy dla voice sessions. `voiceCost.js` rozdziela registry modeli od spend guard; nieznany model jest wyceniany konserwatywnie według najdroższego znanego profilu, a limity mają soft warning i hard cap. Moduł celowo unika ufania niezweryfikowanemu identyfikatorowi tieru. fileciteturn128file0L1-L2

Najważniejszy pattern:

```text
MODEL REGISTRY
 ↓
ACTUAL MODEL ID
 ↓
RATE RESOLUTION
 ↓
USAGE METERING
 ↓
SOFT WARNING
 ↓
HARD CAP
```

Wspólna zasada dla wszystkich kosztownych agent actions:

**meter actual execution, not requested configuration.**

## 13. Agent-facing APIs need semantic contracts

G0DM0D3 pokazuje OpenAI SDK-compatible REST endpoint z tier-based quotas i jawnie opisanym feature gatingiem. API zwraca rate-limit headers oraz błędy upgrade requirements. fileciteturn127file0L1-L2

Dla OmniCore wzmacnia to model `Capability Contract`:

```yaml
CapabilityContract:
  id:
  version:
  inputs:
  outputs:
  side_effects:
  required_authorization:
  quotas:
  latency_slo:
  cost_model:
  failure_modes:
  audit_schema:
```

Agent powinien otrzymywać nie tylko nazwę narzędzia, ale jawny kontrakt jego skutków i ograniczeń.

## 14. Agentic coding environments — extracted pattern

Zestawienie użytkownika wskazuje wspólną klasę agentów codingowych: Cursor/Windsurf, Claude Code, Devin, Replit Agent, Lovable/Bolt i podobne systemy łączą rozumienie wielu plików, wieloplikowe edycje, terminal execution, testowanie, budowanie i w części przypadków deployment. Dla portfolio nie należy przyjmować deklaracji „najpotężniejszy” jako faktu bez benchmarku.

Wspólny abstraction:

```text
REPOSITORY GRAPH
 ↓
TASK DECOMPOSITION
 ↓
CODE / FILE ACTIONS
 ↓
BUILD + TEST
 ↓
DEBUG / REPAIR LOOP
 ↓
SECURITY / POLICY GATE
 ↓
ARTIFACT / DEPLOY
```

To wzmacnia Project 13 (Software Factory) i Project 28 (Verified Code Generation).

## 15. IDE agent vs backend agent

God's Eye View pokazuje, że bogaty agent może być sterowany przez realtime voice, ale właściwe operacje są wykonywane przez deterministic action runner. G0DM0D3 pokazuje analogiczną separację między UI a modularnym silnikiem oceny. fileciteturn123file0L1-L2 fileciteturn119file0L1-L2

Wniosek:

`AGENT BRAIN != ACTION ENGINE != UI`

Trzy warstwy powinny być testowalne osobno.

## 16. Multimodal state should be typed, not prompt-packed

W GEV dane sceny obejmują entities, coordinates, active layers, viewport, screenshots, feed state i annotations. Agent dostaje wybrane pola jako kontekst, natomiast wykonanie odbywa się przez typed tools. fileciteturn117file0L1-L2

Wniosek dla wszystkich agentów:

```text
RAW WORLD STATE
 ↓
TYPED STATE SNAPSHOT
 ↓
CONTEXT SELECTION
 ↓
MODEL
 ↓
TYPED ACTION
```

Nie należy serializować całego stanu świata do nieustrukturyzowanego promptu, gdy może on być pobierany przez authoritative state API.

## 17. Visual intelligence and honest grounding

GEV instruuje voice agent, aby korzystał z viewport screenshot tylko w granicach tego, co jest czytelne, oraz unikał halucynowania etykiet. fileciteturn117file0L1-L2

To daje general rule dla Vision agents:

`UNREADABLE ≠ UNKNOWN SOURCE ≠ TRUE`

Każda obserwacja wizualna powinna mieć provenance i confidence, a model nie powinien zamieniać braku czytelności w pewne twierdzenie.

## 18. Project 40 — natural integration target

Źródła wskazują spójny nowy kierunek dla portfolio: **OmniCore Agentic Development & Visual Intelligence Fabric**.

```text
                    OMNICORE CONTROL PLANE
                              │
          ┌───────────────────┼───────────────────┐
          ↓                   ↓                   ↓
   REPOSITORY GRAPH      WORLD STATE GRAPH    KNOWLEDGE/EVIDENCE
          │                   │                   │
          ↓                   ↓                   ↓
   CODING AGENTS         MULTIMODAL AGENTS    RESEARCH AGENTS
          │                   │                   │
          └───────────────┬───┴───────┬───────────┘
                          ↓
                  TYPED CAPABILITY BROKER
                          ↓
             VERIFY → EXECUTE → OBSERVE
                          ↓
                  ARTIFACT / STATE DELTA
                          ↓
                       EVALS
```

### Core additions

1. Repository Graph — symbol/file/module/dependency map for repo-scale agents.
2. World State Graph — authoritative state model for dynamic environments such as GEV-like applications.
3. Typed Action Runner — postcondition-aware tool execution.
4. Turn Ownership Controller — cancellation and supersession safety.
5. Ephemeral Credential Broker — short-lived provider sessions.
6. Cost Governor — actual-model and actual-usage accounting.
7. Network Capability Firewall — allowlisted network destinations and bounded proxies.
8. Multimodal Evidence Layer — screenshot/DOM/data observations with provenance.
9. Parallel Solver Race — optional N-model candidate generation and selection.
10. Evaluation Ledger — immutable benchmark records linking task, model, tool path, artifact and outcome.

### Definition of Done

- repo-scale graph indexing;
- deterministic read/write/test/build tool contracts;
- postcondition verification;
- turn supersession and abort handling;
- ephemeral credentials;
- spend guard;
- multimodal state snapshots;
- typed visual evidence;
- parallel model race;
- security and provenance telemetry;
- reproducible task benchmarks.

## 19. Portfolio invariants added

29. Agent brain, action engine and UI are separate trust domains.
30. Tool success requires verified postcondition, not merely successful invocation.
31. Stale turns cannot authoritatively mutate or confirm newer state.
32. Actual execution identity, not requested tier, determines metering.
33. Agent-facing network functions are allowlisted capabilities, not arbitrary fetchers.
34. Dynamic world state should be authoritative and typed rather than copied wholesale into prompts.
35. Multimodal observations require provenance and calibrated uncertainty.
36. Parallel model agreement is evidence only when solver paths are meaningfully independent.
37. Operational telemetry, content and optional research datasets remain separate data classes.
38. Local-first deployment still requires explicit exposure, rate-limit and secret controls.
