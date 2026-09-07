# 32 — Deep OSINT Agent & Zero-Trust Evidence Engine MAX

## Cel projektu

Zbudować defensywnego agenta OSINT, który przechodzi od prostego skryptu enumeracyjnego do **rekurencyjnego, dowodowego systemu analitycznego** z wyraźną granicą między zbieraniem danych, wnioskowaniem i działaniem.

Materiały Deep OSINT opisują przejście od pasywnego zbierania do rekurencyjnego procesu, w którym każdy punkt danych staje się potencjalnym `pivot point`; podkreślają również konieczność zdefiniowania celu, zakresu oraz ram prawnych i etycznych przed zbieraniem danych. fileciteturn31file0L10-L35

## Canonical investigation loop

```text
TARGET / QUESTION
      ↓
SCOPE + AUTHORIZATION + LEGAL BOUNDARY
      ↓
PASSIVE COLLECTION
      ↓
NORMALIZATION
      ↓
EVIDENCE GRAPH
      ↓
PIVOT SELECTION
      ↓
NEW COLLECTION
      ↓
CORRELATION / ANALYSIS
      ↓
CONFIDENCE + COUNTEREVIDENCE
      ↓
REPORT / ALERT
```

## Autonomous Command Loop — bez niekontrolowanej autonomii

Materiały NEXUS-GHOST przedstawiają ACL jako pętlę: dyrektywa użytkownika → analiza → decyzja o narzędziu → wykonanie backendowe → zwrot wyniku do kontekstu → ponowna synteza. fileciteturn32file8L451-L473

W Project 32 ACL zostaje zastąpiona przez typed state machine:

```text
RECEIVED
→ SCOPED
→ AUTHORIZED
→ PLAN
→ COLLECT
→ VALIDATE
→ CORRELATE
→ ESCALATE
→ REPORT
```

Każde przejście ma warunki wejścia i wyjścia.

## Evidence object

Każde znalezisko jest normalizowane do:

```yaml
Evidence:
  id:
  observed_at:
  source:
  source_type:
  target:
  claim:
  raw_reference:
  extracted_data:
  provenance:
  freshness:
  reliability:
  confidence:
  collection_mode: passive|active
  authorization_scope:
  counterevidence:
  transformations:
```

`Evidence != Claim != Hypothesis != Recommendation`.

## Passive-first policy

Domyślnie agent zaczyna od pasywnego rozpoznania. Materiały wskazują DNS historyczny, archiwa, WHOIS i publiczne repozytoria jako typowe źródła takiego rozpoznania. fileciteturn31file0L29-L35

Aktywne testy są dozwolone wyłącznie po spełnieniu:

```text
explicit_scope
+ target_ownership_or_authorization
+ operation_allowlist
+ rate_limit
+ audit_logging
```

Brak autoryzacji oznacza przejście do trybu pasywnego albo odmowę.

## Tool fabric

Materiały dotyczące agenta OSINT pokazują klasyczne moduły: skanowanie portów, banner grabbing, wyszukiwanie profili, ekstrakcję metadanych i geolokalizację. fileciteturn32file4L230-L260

Project 32 opakowuje je jako capability-scoped tools:

```text
capability_id
subject_id
target_scope
operation
expiry
rate_limit
provenance
approval_state
```

Narzędzie nie dziedziczy automatycznie uprawnień od agenta.

## Weaknesses of the baseline script

Dostarczony prosty `OSINTAgent` rozdziela skan IP, analizę domeny i enumerację nazwy użytkownika, zapisując wyniki do JSON. fileciteturn30file6L9-L15

Jednocześnie jego wyników nie wolno traktować jako dowodów wysokiej jakości, ponieważ:

- analiza IP zależy od zewnętrznego API;
- `HEAD` i status HTTP nie zawsze dają jednoznaczne rozstrzygnięcie;
- enumeracja użytkowników oparta na 200/404 jest uproszczona;
- raport nie ma modelu provenance, reliability ani counterevidence;
- zakres uprawnień celu nie jest częścią kontraktu narzędzia.

Project 32 usuwa te ograniczenia przez evidence schema, typed connectors i warstwę policy enforcement.

## Deep OSINT recursion governor

Agent wybiera kolejny pivot na podstawie:

`information_gain × relevance × confidence_gap × freshness / cost`

Zatrzymanie następuje, gdy:

- pytanie zostało odpowiednio pokryte;
- marginal information gain spadł poniżej progu;
- pozostałe pivots wymagają nieautoryzowanego działania;
- przekroczono budżet czasu / zapytań;
- pojawiła się sprzeczność wymagająca człowieka.

## MCP + Agent Skills architecture

Remote MCP jest osobną domeną zaufania. OpenAI dokumentuje, że serwer MCP może dostarczyć modelowi zewnętrzne narzędzia, ale zaufanie do serwera jest krytyczne, ponieważ złośliwy serwer może eksfiltrować dane znajdujące się w kontekście modelu. fileciteturn25file0L12-L21

Dlatego Project 32 stosuje:

```text
MODEL
 ↓
TOOL DISCOVERY
 ↓
ALLOWED-CAPABILITY FILTER
 ↓
AUTHORIZATION
 ↓
MCP CALL
 ↓
OUTPUT VALIDATION
 ↓
PROVENANCE NORMALIZATION
 ↓
EVIDENCE GRAPH
```

Dla dużych katalogów narzędzi używa filtrowania i deferred loading, aby ograniczyć koszt i powierzchnię ekspozycji. fileciteturn25file0L491-L514

## UI / evidence workstation

MCP Apps są używane w modelu data-first/render-second. Najpierw narzędzie zwraca `structuredContent`, następnie osobne narzędzie renderuje finalny widok. fileciteturn25file1L1160-L1193

Proponowany interfejs:

```text
LEFT: target / scope / permissions
CENTER: evidence graph
RIGHT: claim inspector
BOTTOM: provenance / timeline / raw source
```

Stan biznesowy pozostaje na serwerze; stan UI jest efemeryczny; stan trwały jest przechowywany w kontrolowanym backendzie. fileciteturn25file1L1375-L1415

## Adversarial evaluation

Test suite obejmuje:

- fałszywe korelacje;
- spoofed profiles;
- poisoned public data;
- prompt injection w stronach i dokumentach;
- sprzeczne źródła;
- stale data;
- unicode/homoglyph obfuscation;
- wymuszenie aktywnego skanowania poza zakresem.

Celem jest sprawdzenie, czy agent potrafi powiedzieć **„brak wystarczających dowodów”** zamiast generować pozorną pewność.

## Integracja

Project 32 integruje Projects 06, 12, 15, 19, 25, 26, 27, 29 i 30.

## Definition of Done

- typed investigation graph;
- provenance dla każdego twierdzenia;
- passive-first execution;
- authorization-aware active tools;
- evidence/reasoning separation;
- resumable investigations;
- adversarial evaluation;
- audytowalny raport końcowy.
