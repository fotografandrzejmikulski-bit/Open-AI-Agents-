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

## Source-derived baseline: Deep OSINT Framework

Dostarczony framework implementuje klasę `DeepOSINT` z modułami generowania zapytań wyszukiwawczych, crawl/extraction, analizy EXIF, skanowania portów oraz raportowania HTML. Źródło pokazuje m.in. ekstrakcję e-maili, telefonów i linków społecznościowych z HTML, analizę `model`, `make`, `datetime_original`, GPS i software w EXIF oraz sprawdzanie typowych portów 21/22/25/53/80/443/3306/8080. fileciteturn98file0L12-L25 fileciteturn98file0L53-L85 fileciteturn98file0L92-L126 fileciteturn98file0L128-L147

Framework zawiera również generowanie wyszukiwań dotyczących publicznych dokumentów, paneli logowania, otwartych katalogów, plików konfiguracyjnych, wyników społecznościowych i treści z serwisów paste. W systemie produkcyjnym takie zapytania są klasyfikowane jako **high-risk discovery patterns** i mogą być wykonywane wyłącznie w dozwolonym zakresie oraz z zachowaniem polityki prywatności i autoryzacji; nie stanowią domyślnej ścieżki eksfiltracji ani pozyskiwania danych uwierzytelniających. fileciteturn98file0L26-L52

Wniosek: źródłowy skrypt jest dobrym **adapterem kolektorów**, ale nie jest jeszcze bezpiecznym agentem dowodowym. Project 32 zachowuje jego klasy modułów, lecz nakłada na nie capability boundary, provenance, authorization i evidence validation.

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

## Collector contract

Każdy kolektor z frameworku zostaje przekształcony do kontraktu:

```yaml
Collector:
  id:
  version:
  input_schema:
  output_schema:
  collection_mode: passive|active
  required_capabilities: []
  target_constraints: []
  rate_limit:
  timeout:
  provenance_fields: []
  evidence_quality:
  failure_modes: []
```

Minimalny wynik kolektora musi zawierać `observed_at`, `source`, `target`, `raw_reference` i identyfikator kolektora. Kolektor nie może samodzielnie zmienić zakresu dochodzenia.

## Weaknesses of the baseline script

Dostarczony framework korzysta bezpośrednio z `requests.Session`, regexów, BeautifulSoup, EXIF oraz socketów; zapisuje stan do `report_data`, a raport końcowy renderuje jako HTML. fileciteturn98file0L12-L25 fileciteturn98file0L53-L85 fileciteturn98file0L148-L173

To nie wystarcza do systemu produkcyjnego, ponieważ:

- wynik scrapowania nie jest dowodem wysokiej jakości bez provenance i snapshotu źródła;
- regex dla telefonów i e-maili może generować false positives/negatives;
- link HTTP, status `200/404` albo pojedynczy rekord nie potwierdza tożsamości podmiotu;
- EXIF może być usunięty lub zmodyfikowany, więc GPS jest obserwacją metadanych, nie automatycznie prawdą o miejscu wykonania zdjęcia;
- aktywny socket scan jest działaniem sieciowym i wymaga autoryzacji oraz kontroli zakresu;
- generowanie zapytań do paneli administracyjnych, konfiguracji lub treści wyciekowych zwiększa ryzyko pozyskania danych nieuprawnionych;
- raport HTML nie posiada kryptograficznego łańcucha pochodzenia ani modelu counterevidence;
- brak wersjonowanego stanu dochodzenia utrudnia wznowienie i audyt.

Project 32 usuwa te ograniczenia przez evidence schema, typed connectors, snapshot/provenance layer i policy enforcement.

## Deep OSINT recursion governor

Agent wybiera kolejny pivot na podstawie:

`information_gain × relevance × confidence_gap × freshness / cost`

Zatrzymanie następuje, gdy:

- pytanie zostało odpowiednio pokryte;
- marginal information gain spadł poniżej progu;
- pozostałe pivots wymagają nieautoryzowanego działania;
- przekroczono budżet czasu / zapytań;
- pojawiła się sprzeczność wymagająca człowieka.

## Evidence quality gate

Przed awansem znaleziska do claimu system wykonuje:

```text
RAW OBSERVATION
      ↓
PARSING / NORMALIZATION
      ↓
SOURCE + TIME + TARGET VALIDATION
      ↓
DUPLICATE / CONFLICT CHECK
      ↓
COUNTEREVIDENCE SEARCH
      ↓
RELIABILITY + FRESHNESS SCORE
      ↓
CLAIM ELIGIBILITY
```

Reguła nadrzędna: brak dowodu nie jest dowodem braku, a brak spójności nie jest automatycznie dowodem oszustwa.

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
- wymuszenie aktywnego skanowania poza zakresem;
- fałszywe lub zmanipulowane EXIF;
- źródła zmieniające treść po pobraniu;
- kolektory próbujące rozszerzyć `target_scope`;
- kolektory zwracające dane bez wymaganych provenance fields.

Celem jest sprawdzenie, czy agent potrafi powiedzieć **„brak wystarczających dowodów”** zamiast generować pozorną pewność.

## Resumability

Każda faza dochodzenia zapisuje checkpoint:

```yaml
InvestigationCheckpoint:
  investigation_id:
  state:
  scope_version:
  evidence_graph_version:
  completed_collectors: []
  pending_pivots: []
  blocked_actions: []
  unresolved_conflicts: []
  budget:
  last_updated:
```

Wznowienie nie może automatycznie odziedziczyć wygasłych uprawnień. Capability grants są ponownie walidowane przy wykonaniu.

## Integracja

Project 32 integruje Projects 06, 12, 15, 19, 25, 26, 27, 29 i 30.

## Definition of Done

- typed investigation graph;
- provenance dla każdego twierdzenia;
- passive-first execution;
- authorization-aware active tools;
- evidence/reasoning separation;
- collector contracts;
- evidence quality gates;
- resumable investigations;
- adversarial evaluation;
- audytowalny raport końcowy.
