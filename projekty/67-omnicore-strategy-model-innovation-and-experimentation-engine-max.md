# Project 67 — OmniCore Strategy, Business-Model Innovation & Experimentation Engine MAX

## Cel

Zbudować oryginalny, evidence-driven silnik, który rozdziela model biznesu, strategię i operacje, a następnie pozwala je wspólnie projektować, porównywać, eksperymentować, wdrażać i ponownie kalibrować na podstawie rzeczywistych wyników.

## Geneza

Projekt wynika z syntezy dostarczonego korpusu dotyczącego Business Model Canvas, relacji strategia–model biznesu, mikrofundamentów, kompetencji organizacyjnych, przewagi konkurencyjnej, prostych reguł strategicznych, eksperymentowania, strategii małych firm oraz zmian modeli biznesowych pod wpływem turbulencji rynkowych. Źródła wskazują m.in. na rozdzielenie modelu biznesu, strategii i operacji oraz na znaczenie tworzenia, dostarczania i przechwytywania wartości. fileciteturn130file0L30-L40 fileciteturn130file4L11-L15

## Oryginalna koncepcja

### Business Strategy Operating System (BSOS)

BSOS traktuje strategię i model biznesu jak wersjonowane, wykonywalne artefakty zamiast statycznych dokumentów.

```text
MARKET / CUSTOMER / TECHNOLOGY / RESOURCE SIGNALS
                    ↓
             EVIDENCE GRAPH
                    ↓
          BUSINESS MODEL STATE
                    ↓
           STRATEGY STATE
                    ↓
       CAPABILITY / RESOURCE FIT
                    ↓
        SCENARIO / OPTION SET
                    ↓
        EXPERIMENT COMPILER
                    ↓
         BOUNDED EXECUTION
                    ↓
          OUTCOME READBACK
                    ↓
       DRIFT / GAP ANALYSIS
                    ↓
       MODEL / STRATEGY UPDATE
                    ↺
```

## Rozdzielenie obiektów

### `BusinessModelSpec`

Opisuje:
- customer segments;
- value proposition;
- channels;
- relationships;
- key activities;
- key resources;
- key partners;
- cost structure;
- revenue/value-capture mechanisms;
- assumptions and evidence state.

### `StrategySpec`

Opisuje:
- strategic objectives;
- competitive position;
- chosen domain;
- strategic constraints;
- priorities;
- capability development;
- strategic trade-offs;
- decision rules;
- horizon and review cadence.

### `OperatingModelSpec`

Opisuje:
- workflows;
- roles;
- systems;
- controls;
- service levels;
- operational metrics;
- dependencies;
- execution ownership.

Źródła podkreślają, że model biznesu ma charakter bardziej reprezentacyjny, natomiast strategia opisuje dynamiczne zachowania i wybory organizacji; dlatego projekt przechowuje je jako osobne, ale połączone artefakty. fileciteturn132file6L216-L236

## Microfoundation Graph

Każdy strategiczny wybór musi być mapowalny do zdolności organizacji:

`STRATEGIC CHOICE → REQUIRED CAPABILITY → ASSET / SKILL / PROCESS → OWNER → MEASURE → OUTCOME`

To rozwija wnioski dotyczące kluczowych kompetencji jako strategicznych aktywów oraz problemu ich wyceny i wykorzystania. fileciteturn124file3L7-L24

## Experiment Compiler

System nie "przewiduje sukcesu". Kompiluje hipotezę do testowalnego eksperymentu:

```text
HYPOTHESIS
  ↓
ASSUMPTIONS
  ↓
EXPECTED SIGNAL
  ↓
CONTROL / BASELINE
  ↓
INTERVENTION
  ↓
METRIC
  ↓
STOPPING RULE
  ↓
OUTCOME
  ↓
EVIDENCE UPDATE
```

Wynik eksperymentu nie nadpisuje modelu automatycznie; aktualizuje stan dowodowy i uruchamia regułę rewizji.

## Strategic Rule Engine

Silnik wspiera proste, mierzalne reguły zamiast nieprzejrzystych narracji. Korpus Obłoja wskazuje na jasne wyzwania, kontrolę kosztów, bezwzględne eksperymentowanie, koncentrację na właściwych odbiorcach, wykorzystanie potencjału ludzi i uczenie się z poważnych porażek. fileciteturn132file5L172-L190

W OmniCore są to parametryzowane reguły:

- `challenge_level`
- `cost_guardrail`
- `experiment_rate`
- `segment_priority`
- `capability_allocation`
- `failure_learning_weight`

Reguły nie mogą jednak omijać polityk bezpieczeństwa ani human-review.

## Business Model Morphing

Projekt umożliwia zmianę wybranych komponentów modelu jako kontrolowaną transformację:

`T1..Tn → candidate variant → impact analysis → experiment → outcome`

Inspiracją jest materiał PARP pokazujący zmianę klientów, kanałów, relacji, zasobów, działań i partnerów podczas przechodzenia do modelu online. fileciteturn132file11L325-L343

## Circular Value Graph

Model biznesowy może zawierać:
- material flow;
- reuse/refurbish/remanufacture;
- partner symbiosis;
- waste-to-input transitions;
- lifecycle economics;
- reverse logistics;
- resource constraints.

Circularity jest więc reprezentowana jako przepływ wartości i zasobów, a nie wyłącznie wskaźnik ESG.

## Dynamic strategic lifecycle

BSOS wspiera trzy tryby działania zgodne z dostarczonym materiałem:

1. `GROWTH_RULES` — proste reguły i szybka nauka;
2. `OPTIMIZATION` — doskonalenie modelu i przewagi;
3. `RENEWAL` — okresowa renowacja modelu i innowacja.

Przejście między trybami wymaga sygnałów z danych i jawnego kryterium, np. stagnacji wzrostu, wzrostu kosztów, spadku retention, pogorszenia unit economics albo zmiany otoczenia.

## Decision matrix

Każdy wariant modelu oceniany jest wielokryterialnie:

| Kryterium | Pytanie |
|---|---|
| Value | Czy tworzy mierzalną wartość? |
| Capture | Czy firma potrafi zatrzymać część wartości? |
| Capability fit | Czy organizacja potrafi go wykonać? |
| Strategic fit | Czy wspiera wybraną pozycję? |
| Adaptability | Jak reaguje na zmianę założeń? |
| Economics | Czy unit economics są wykonalne? |
| Evidence | Ile założeń pozostaje niezweryfikowanych? |
| Risk | Jakie są główne downside scenarios? |
| Circularity | Czy zasoby i przepływy można zamknąć lub wydłużyć? |

## State and evidence model

Każde założenie ma stan:

`OBSERVED | ASSUMED | INFERRED | TESTING | VALIDATED | REJECTED | STALE`

Każda zmiana modelu tworzy `ModelRevision` z:
- parent revision;
- changed components;
- rationale;
- evidence delta;
- expected impact;
- experiment linkage;
- approval state.

## Integracja z istniejącym OmniCore

Project 67 wykorzystuje:
- Project 25 — portfolio control plane;
- Project 27 — bounded reasoning and self-consistency;
- Project 29/30 — evidence/MCP plane;
- Project 34 — venture/business-model foundry;
- Project 48 — grand-challenge/evidence synthesis;
- Project 49 — cognitive sovereignty and active inference;
- Project 56 — commercialization/outcome economics;
- Project 62/63/64 — data, causality, decision intelligence and predictive BI;
- Project 66 — adaptive business-model and circular-value foundation.

Nie zastępuje wcześniejszych projektów. Jest nad nimi warstwą wykonawczą dla **strategii + modelu biznesowego + eksperymentu + wyniku**.

## Hard invariants

- `business_model != strategy`
- `strategy != operations`
- `hypothesis != evidence`
- `forecast != realized outcome`
- `capability != competitive advantage`
- `experiment result != causal proof` bez odpowiedniego projektu badawczego
- `model score != authorization`
- `AI recommendation != strategic approval`
- `dashboard != validation`
- `circular claim != measured resource outcome`

## Safety

Silnik nie może optymalizować manipulacji, uzależnienia, wykorzystania podatności ani ukrytego sterowania zachowaniem. Segmentacja i personalizacja są dozwolone dla dopasowania produktu, ale wymagają przejrzystości, proporcjonalności i możliwości odmowy. Materiały strategiczne dotyczące presji, motywacji lub wpływu są interpretowane jako dane do oceny ryzyka Human Agency.

## Release gates

`G0 source/evidence integrity → G1 model completeness → G2 capability fit → G3 economics → G4 risk/scenario → G5 experiment design → G6 bounded execution → G7 outcome readback → G8 revision approval → G9 staged rollout → G10 post-release drift monitoring`

## Expected outcome

Project 67 daje OmniCore zdolność do utrzymywania **żywego modelu biznesowego**, który można obserwować, testować i zmieniać na podstawie rzeczywistych wyników, zamiast ponownie generować statyczny plan biznesowy po każdej zmianie rynku.