# 31 — Agentic Venture & Business Model Foundry MAX

## Cel projektu

Zbudować warstwę, która zamienia pomysł na produkt AI w **sprawdzalny model biznesu**, a dopiero potem w implementację. Projekt łączy klasyczne modele biznesowe z agentic software factory, application builders, MCP/Skills i kontrolą ryzyka.

Źródłowe ujęcia modelu biznesu rozróżniają strategię od modelu biznesu, ale wskazują na ich silne powiązanie przez tworzenie i przechwytywanie wartości. W literaturze model biznesu bywa opisywany przez wybory strategiczne, tworzenie wartości, przejmowanie wartości oraz sieć wartości. fileciteturn34file7L369-L388

## Model kanoniczny

Projekt implementuje dwa komplementarne widoki:

```text
MAGICZNY TRÓJKĄT
WHO?  → segment klienta
WHAT? → propozycja wartości
HOW?  → łańcuch wartości
WHY?  → ekonomika / rentowność
```

oraz pełny model 9-elementowy:

```text
VALUE PROPOSITION
CUSTOMER SEGMENTS
CHANNELS
CUSTOMER RELATIONSHIPS
KEY RESOURCES
KEY ACTIVITIES
KEY PARTNERS
REVENUE STREAMS
COST STRUCTURE
```

Takie komponenty są explicite przedstawione w ujęciu Osterwaldera i Pigneura, a model Gassmanna, Frankenbergera i Csika sprowadza decyzje do pytań kto/co/jak/dlaczego. fileciteturn34file0L11-L38

## AI Venture Compiler

Natural-language intent jest kompilowany do `BusinessModelSpec`:

```yaml
customer_segment:
value_proposition:
problem:
workflow:
channels:
relationship_model:
key_resources:
key_activities:
key_partners:
revenue_model:
cost_model:
unit_economics:
moat:
risks:
assumptions:
evidence:
experiments:
```

Każde pole ma status:

`OBSERVED | INFERRED | HYPOTHESIS | VALIDATED | REJECTED`

Agent nie może przedstawiać hipotez rynkowych jako faktów.

## Opportunity Mining

Publikacja Mindstream x HubSpot pokazuje szeroki katalog możliwych biznesów AI: chatboty i asystenci dla firm, narzędzia do tworzenia treści, automatyzacja dokumentów, analityka rynku, reputacja, tłumaczenia, narzędzia podcastowe i wiele innych. fileciteturn31file1L45-L105

Foundry nie kopiuje tego katalogu. Tworzy **silnik selekcji okazji** oceniany według:

```text
market_pain
willingness_to_pay
frequency_of_use
distribution_access
gross_margin
integration_friction
retention_potential
data_advantage
security_risk
regulatory_risk
implementation_cost
```

Wynikiem jest ranking hipotez, nie automatyczna decyzja inwestycyjna.

## Monetyzacja

Obsługiwane są modele:

- subscription / SaaS;
- usage-based;
- transactional / take-rate;
- service + software;
- enterprise licensing;
- marketplace;
- affiliate / referral;
- implementation / integration;
- data/insight products, tylko gdy legalność i zgody na wykorzystanie danych są jawnie spełnione.

Każdy model musi policzyć minimum:

`ARPU → gross margin → acquisition cost → retention → payback → capacity cost → support cost`

## Agentic MVP Loop

```text
IDEA
 ↓
CUSTOMER / PROBLEM
 ↓
VALUE PROPOSITION
 ↓
BUSINESS MODEL
 ↓
ECONOMIC SIMULATION
 ↓
RISK / POLICY CHECK
 ↓
CHEAPEST VALIDATING EXPERIMENT
 ↓
MEASURED RESULT
 ↓
PIVOT / PROCEED / KILL
 ↓
IMPLEMENTATION SPEC
```

Najpierw eksperyment, później ciężka implementacja.

## Application-builder integration

Wewnętrzna analiza dostarczonych pakietów AppBuilder/AppStudio wskazuje na istotny wzorzec produktowy: builder może być traktowany nie tylko jako edytor, ale jako **kontrolowana warstwa delivery** z projektami, szablonami, statusami buildów, konfiguracją AI, analityką, subskrypcją, onboardingiem i mechanizmami publikacji.

Foundry rozdziela więc:

```text
BUSINESS MODEL CONTROL PLANE
        ↓
PRODUCT SPEC
        ↓
APP BUILDER / AGENTIC SOFTWARE FACTORY
        ↓
BUILD + TEST + VERIFY
        ↓
PUBLISH / BILL / OBSERVE
```

Builder nie może stać się źródłem prawdy dla ekonomiki biznesu; prawda biznesowa pozostaje w wersjonowanych specyfikacjach i danych backendowych.

## Anti-manipulation boundary

Materiały o ukrytej perswazji są traktowane jako materiał **do rozpoznawania wpływu**, nie jako instrukcja projektowania covert persuasion. Źródło opisuje budowanie porozumienia, synchronizację i wykorzystywanie zainteresowań jako elementy wpływu. fileciteturn30file3L28-L50

Foundry zabrania:

- ukrywania celu perswazji;
- manipulacyjnych dark patterns;
- wykorzystywania danych osobowych do niejawnego profilowania wpływu;
- automatycznego targetowania osób podatnych;
- projektowania interfejsów utrudniających świadomą odmowę.

Dopuszcza transparentną komunikację wartości, personalizację za zgodą, eksperymenty UX z mierzalną hipotezą oraz łatwe opt-out.

## Governance

Każdy pomysł otrzymuje:

`business-model-version + evidence-bundle + assumptions + experiment-log + policy-decision + implementation-decision`

### Integracja

Projekt 31 integruje Projects 07, 13, 16, 20, 22, 24, 25, 29 i 30.

## Definition of Done

- spisana propozycja wartości;
- segmenty i kanały;
- pełny model przychodów i kosztów;
- jawne założenia i hipotezy;
- eksperyment walidacyjny;
- mierniki ekonomiczne;
- threat/policy review;
- implementacja dopiero po spełnieniu progu walidacji.
