# 33 — Agentic App Builder & Delivery Control Plane MAX

## Cel projektu

Zbudować aplikacyjny „assembly line” łączący natural-language intent, generowanie aplikacji, AI-assisted editing, szablony, build/test, signing, publikację, analitykę i billing — ale pod kontrolą jednej warstwy governance.

Dostarczone materiały OpenAI opisują trzy istotne warstwy: Skills jako wersjonowane pakiety instrukcji i plików, MCP jako warstwę zewnętrznych capabilities oraz MCP Apps jako opcjonalny UI. Skills są traktowane jako potencjalnie uprzywilejowany kod/instrukcje i wymagają przeglądu bezpieczeństwa. fileciteturn28file0L14-L24 fileciteturn28file0L540-L563

## Product architecture

```text
NATURAL-LANGUAGE INTENT
          ↓
REQUIREMENTS / SPEC
          ↓
APP MANIFEST
          ↓
AGENTIC PLANNER
          ↓
GENERATOR / TEMPLATE / SKILL
          ↓
BUILD
          ↓
TEST / SECURITY / POLICY
          ↓
SIGN
          ↓
STAGED RELEASE
          ↓
ANALYTICS / FEEDBACK
          ↓
VERSIONED REVISION
```

## Application Manifest

Każdy projekt otrzymuje jedną jawnie wersjonowaną reprezentację:

```yaml
app_id:
name:
version:
platforms:
ui_contract:
data_contract:
capabilities:
skills:
connectors:
secrets_policy:
build_profile:
signing_profile:
release_channel:
rollback_version:
telemetry_policy:
commercial_plan:
```

Manifest jest źródłem prawdy dla delivery; UI builder jest jego klientem.

## Builder UX doctrine

Wewnętrzna inspekcja dostarczonych pakietów AppBuilder/AppStudio została wykorzystana jako materiał do odtworzenia wzorców UX dla buildera: osobny lifecycle projektu, konfiguracja, build status, templates, AI playground, analityka, subskrypcja, onboarding, publikacja i signing/key management.

Nie kopiujemy implementacji binarnej. Wyciągamy z niej wzorzec architektoniczny:

```text
EDIT
CONFIGURE
PREVIEW
BUILD
VERIFY
SIGN
PUBLISH
OBSERVE
```

Każdy etap jest osobnym stanem i może zostać wznowiony.

## AI Playground

Tryb eksperymentalny jest izolowany od produkcji:

`DRAFT → GENERATED → REVIEW → TEST → PROMOTE`

AI-generated code nie jest automatycznie kodem produkcyjnym tylko dlatego, że build przeszedł.

## Skills as executable product capabilities

OpenAI Skills są wersjonowane; `default_version` wskazuje wersję domyślną, a referencja może wskazywać określony numer wersji. fileciteturn28file0L462-L489

Control Plane wymusza:

- skill provenance;
- version pinning dla release builds;
- developer-only skill installation;
- review skryptów i instrukcji;
- brak arbitralnego doboru Skills przez końcowego użytkownika;
- explicit approval dla działań wysokiego wpływu.

## MCP capability boundary

Remote MCP i connectors są źródłami capabilities, nie autorytetem. OpenAI opisuje listowanie narzędzi, filtrowanie `allowed_tools` i osobne mechanizmy approval. fileciteturn25file0L453-L489 fileciteturn25file0L491-L514

W projekcie:

```text
DISCOVER
 ↓
FILTER
 ↓
AUTHORIZE
 ↓
CALL
 ↓
VALIDATE OUTPUT
 ↓
AUDIT
```

## MCP Apps UI

UI jest opcjonalne i nie może być warunkiem poprawności workflow. OpenAI zaleca oddzielenie narzędzi danych od narzędzi renderujących, aby model mógł najpierw przetworzyć dane, a dopiero później wybrać prezentację. fileciteturn25file1L1026-L1054 fileciteturn25file1L1160-L1184

Wersja Control Plane stosuje:

```text
DATA TOOLS
  ↓ structuredContent
MODEL DECISION
  ↓
RENDER TOOL
  ↓
MCP APP
```

## State architecture

Rozdzielone są:

- authoritative business data;
- ephemeral UI state;
- durable cross-session state.

Dokumentacja MCP Apps zaleca utrzymywanie danych biznesowych po stronie serwera oraz przechowywanie trwałego stanu w kontrolowanym backendzie. fileciteturn25file1L1375-L1415 fileciteturn25file1L1493-L1509

## CSP and supply-chain security

Każdy widget posiada minimalny allowlist dla `connectDomains`, `resourceDomains` i — tylko gdy niezbędne — `frameDomains`. Dokumentacja wskazuje także, że polityka jest sprawdzana podczas review. fileciteturn25file1L1684-L1697

Control Plane dodaje:

- dependency lock;
- SBOM;
- provenance builda;
- hash artefaktów;
- signed release metadata;
- rollback;
- staged rollout;
- automatic quarantine po regresji.

## Monetization integration

Builder jest sprzężony z Project 31, ale billing pozostaje oddzielony od generatora kodu. Plan komercyjny decyduje o limitach i funkcjach, nie o bezpieczeństwie.

Dla workflow z płatnością obowiązuje zasada: serwer jest źródłem prawdy dla ceny i statusu zamówienia, a operacje płatnicze muszą być idempotentne. fileciteturn25file1L1745-L1766

## Release gates

```text
G0 — SPEC VALID
G1 — CAPABILITIES AUTHORIZED
G2 — BUILD REPRODUCIBLE
G3 — TESTS PASS
G4 — SECURITY REVIEW PASS
G5 — SIGNING PASS
G6 — HUMAN / POLICY APPROVAL
G7 — STAGED DEPLOYMENT
G8 — OBSERVED STABILITY
```

Brak przejścia przez gate blokuje promocję.

## Integracja

Project 33 integruje Projects 07, 13, 16, 20, 24, 25, 26, 28 i 31.

## Definition of Done

- inspectable app manifest;
- versioned Skills;
- governed MCP capabilities;
- resumable build lifecycle;
- reproducible release artifacts;
- signing and rollback;
- MCP Apps data/render separation;
- CSP allowlists;
- telemetry/evals;
- commercial limits isolated from security policy.
