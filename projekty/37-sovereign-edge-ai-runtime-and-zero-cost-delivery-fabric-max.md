# 37 — Sovereign Edge AI Runtime & Zero-Cost Delivery Fabric MAX

## Status
Architecture-ready systems project. Source-derived claims are treated as hypotheses until validated on target hardware, browser versions and production workloads.

## Cel projektu
Zbudować warstwę wykonawczą dla agentów, która preferuje lokalną inferencję, edge compute i przenośną orkiestrację, tak aby koszt, prywatność, latency i zależność od pojedynczego dostawcy nie były stałymi ograniczeniami systemu.

Materiały źródłowe proponują stos: Project IDX/Nix → Firebase Genkit → Ollama → Chrome Built-in AI/window.ai → Android AICore/MediaPipe oraz rozdzielenie logiki biznesowej od dostawcy modelu. fileciteturn77file11L622-L636 fileciteturn77file2L148-L153

## Fundamentalna zasada

```text
AGENT CONTROL PLANE
        ↓
MODEL-AGNOSTIC EXECUTION CONTRACT
        ↓
┌─────────────────────────────────────────────┐
│ LOCAL SERVER │ DESKTOP EDGE │ MOBILE EDGE │
│    Ollama    │ Browser AI   │ AICore/MP   │
└─────────────────────────────────────────────┘
        ↓
VERIFICATION / POLICY / TELEMETRY
```

Model jest wymiennym wykonawcą. Nie może stać się źródłem prawdy dla autoryzacji, bezpieczeństwa ani stanu biznesowego.

## Runtime tiers

### Tier 0 — deterministic
Walidacja schematów, reguły, cache, parsowanie, lokalne funkcje bez modelu.

### Tier 1 — local server
Ollama lub inny lokalny runtime dla zadań niewymagających chmury.

### Tier 2 — browser edge
Warstwa abstrakcji nad lokalnym API przeglądarkowym. Materiał źródłowy wskazuje na wrapper obsługujący capability detection, lifecycle sesji, błędy i graceful degradation. fileciteturn77file4L233-L280

### Tier 3 — mobile edge
Android AICore dla współdzielonej inferencji urządzeniowej oraz MediaPipe LLM Inference dla modeli wymagających większej kontroli wersji. fileciteturn77file9L547-L568

### Tier 4 — cloud escalation
Cloud model tylko wtedy, gdy policy engine uzna, że lokalne zasoby nie spełniają wymagań jakościowych, modalności, czasu lub narzędzi.

## Provider-neutral contract

Każdy backend implementuje wspólny kontrakt:

```text
capabilities()
create_session()
generate()
stream()
structured_output()
tool_call()
usage()
cancel()
health()
```

Genkit jest używany jako warstwa orkiestracji/abstrakcji, a nie jako źródło bezpieczeństwa. Materiał pokazuje, że zmiana modelu może być ograniczona do konfiguracji przy zachowaniu logiki flow. fileciteturn77file2L129-L153

## Edge wrapper

```text
Capability Probe
      ↓
Availability State
  ├── readily
  ├── after-download
  └── unavailable
      ↓
Session Manager
      ↓
Streaming Adapter
      ↓
Schema Validator
      ↓
Policy / Safety Gate
```

Wrapper musi obsługiwać zmianę API, brak modelu, cold start, pobieranie modelu, anulowanie, timeout i fallback. Nie wolno zakładać, że konkretne API przeglądarkowe pozostanie stabilne.

## Zero-cost doctrine — corrected

Hasło „zero kosztów” z materiału źródłowego nie jest gwarancją ekonomiczną. Projekt definiuje je jako:

`minimize marginal inference cost while preserving security, reliability and quality`

Należy mierzyć:

- cost / successful task;
- energy / task;
- latency p50/p95;
- local-vs-cloud execution ratio;
- cloud escalation rate;
- model download/storage overhead;
- failure/recovery rate.

Twierdzenia o konkretnych limitach darmowych, wydajności lub przyszłej dominacji rynkowej wymagają osobnej walidacji i nie są częścią kontraktu architektury.

## Hybrid routing

Project 37 rozszerza Project 17:

```text
TASK
 ↓
CAPABILITY REQUIREMENTS
 ↓
PRIVACY / CONSEQUENCE / LATENCY POLICY
 ↓
LOCAL-FIRST ROUTER
 ├── deterministic
 ├── local model
 ├── browser edge
 ├── mobile edge
 └── cloud specialist
 ↓
VERIFY
 ↓
ESCALATE ONLY IF REQUIRED
```

Źródła porównawcze wskazują na różne profile Claude i Gemini: Claude jest przedstawiany jako silniejszy w długim, spójnym tekście, kodzie i ostrożności, natomiast Gemini jako silniejszy w multimodalności, integracjach Google i szybkości. Są to dane z dostarczonego porównania, nie niezależny benchmark. fileciteturn77file8L487-L524

## Research/runtime integration

Project 37 wspiera architekturę Deep Research z Project 15:

```text
PLANNER
 ↓
FAST / LOW-COST WORKERS
 ↓
PARALLEL COLLECTION
 ↓
EVIDENCE NORMALIZATION
 ↓
STRONGER REASONING / VERIFIER
 ↓
FINAL REPORT
```

Materiały badawcze wskazują na state graphs, równoległe workery, agregację i reflection loop jako podstawę zaawansowanego agenta badawczego. fileciteturn74file10L465-L494

## Reproducible developer environment

Nix/Dev Container/lockfile powinny definiować:

- runtime versions;
- dependencies;
- model adapters;
- test fixtures;
- environment variables schema;
- build commands;
- reproducible CI.

Źródło przedstawia Project IDX + Nix jako sposób na ograniczenie różnic między środowiskiem developerskim i produkcyjnym. fileciteturn77file11L637-L649

## CI/CD

```text
COMMIT
 ↓
LOCKFILE / SBOM
 ↓
UNIT + CONTRACT TESTS
 ↓
MODEL / SCHEMA EVALS
 ↓
SECURITY TESTS
 ↓
EDGE BUILD
 ↓
SIGNED ARTIFACT
 ↓
STAGED RELEASE
 ↓
OBSERVE
```

Dostarczony materiał pokazuje również automatyzację build/deploy przez GitHub Actions oraz Firebase Hosting/Functions. Traktujemy to jako wzorzec pipeline'u, nie jako obowiązkowy backend. fileciteturn77file0L10-L31

## Security boundary

Edge execution jest **untrusted execution domain** dopóki wynik nie przejdzie walidacji.

Obowiązuje dziedziczenie z Projects 26, 30, 31, 35 i 36:

- model nie autoryzuje capabilities;
- lokalna inferencja nie omija policy engine;
- structured output jest walidowany;
- dane lokalne nie są automatycznie eksportowane do chmury;
- cloud escalation wymaga jawnej polityki transferu danych;
- cache modeli nie może zawierać sekretów;
- UI/browser state nie jest źródłem prawdy;
- wszystkie consequential actions przechodzą przez Capability Broker.

## Graceful degradation

Awaria edge AI nie może powodować awarii całej aplikacji:

```text
EDGE AVAILABLE
   ↓
USE EDGE

EDGE UNAVAILABLE
   ↓
LOCAL SERVER

LOCAL SERVER FAIL
   ↓
SAFE DETERMINISTIC FALLBACK

CLOUD ESCALATION
   ↓
ONLY IF POLICY ALLOWS
```

## Evaluation matrix

Każdy model/runtime jest oceniany na identycznych zadaniach:

| Wymiar | Metryka |
|---|---|
| Quality | task success / judge score |
| Reliability | schema validity / retry rate |
| Latency | TTFT / p50 / p95 |
| Privacy | data egress |
| Cost | marginal cost/task |
| Energy | estimated Wh/task |
| Recovery | successful fallback rate |
| Security | policy violation rate |
| Portability | adapter compatibility |

## Definition of Done

- provider-neutral runtime contract;
- local-first execution policy;
- browser/mobile capability wrappers;
- deterministic fallback;
- cloud escalation gate;
- reproducible build environment;
- signed artifacts;
- telemetry and evaluation suite;
- explicit data-egress policy;
- integration with Projects 15, 17, 26, 28, 30, 31, 33, 35 and 36.

## Strategic result

Project 37 nie zakłada, że jeden model jest „najlepszy”. Buduje **substrate**, w którym najlepszy wykonawca może zmieniać się wraz z zadaniem, urządzeniem, ceną, prywatnością i aktualnym stanem technologii — bez przebudowy całego agenta.
