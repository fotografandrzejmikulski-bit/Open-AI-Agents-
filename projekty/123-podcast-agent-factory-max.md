# P123 — Podcast Agent Factory MAX

## Mission

Zbudować współpracujący system Agentów AI do end-to-end produkcji podcastów: od pomysłu i researchu, przez dramaturgię, dialog dwóch lub większej liczby prowadzących, reżyserię akustyczną i generowanie głosów, po montaż, fact-check, QA, marketing, publikację i analizę kolejnych iteracji.

System ma działać jako agentic production pipeline, a nie pojedynczy chatbot. Każdy agent otrzymuje jawnie określone wejścia, kompetencje, ograniczenia, artefakty wyjściowe i warunki przekazania pracy dalej.

## Core pipeline

`IDEA → ORCHESTRATE → RESEARCH → STORY ARCHITECTURE → PERSONA STATE → DIALOGUE → ACOUSTIC DIRECTION → VOICE PRODUCTION → EDIT → FACT CHECK → QA → HUMAN APPROVAL → PUBLISH → ANALYTICS → ITERATE`

## Agent topology

### A01 — Podcast Orchestrator

Nadrzędny koordynator. Zarządza planem pracy, zależnościami, wersjami artefaktów, konfliktami i stanem produkcji. Nie może traktować własnej decyzji jako autoryzacji działań zewnętrznych.

### A02 — Research Agent

Buduje evidence pack: źródła, fakty, chronologię, kontekst, punkty sporne i informacje wymagające dalszej weryfikacji. Rozróżnia `FACT`, `SOURCE_CLAIM`, `INFERENCE`, `HYPOTHESIS` i `CREATIVE_ELEMENT`.

### A03 — Story Architect

Projektuje strukturę odcinka, pacing, hook, konflikt, eskalację, ujawnienia, przejścia i zakończenie. Dramaturgia nie może zmieniać zweryfikowanych faktów.

### A04 — Host Persona Agent: Kuba

Agent persony katalizującej napięcie. Persona jest stanem wersjonowanym: temperament, ironia, cynizm, relacja z tematem, relacja z drugim prowadzącym, wiedza ujawniona słuchaczowi, poziom napięcia i cele sceny.

### A05 — Host Persona Agent: Marta

Agent persony analitycznej i sceptycznej. Reprezentuje perspektywę słuchacza. Może kwestionować twierdzenia, prosić o dowody i zmieniać stanowisko po otrzymaniu nowych informacji.

### A06 — Dialogue Director

Koordynuje wieloagentową rozmowę. Produkuje typed dialogue events z intencją, emocją, tempem, pauzą, overlapem, możliwością przerwania i funkcją dramaturgiczną.

### A07 — Acoustic Director

Przekłada dialog na akustyczny DSL: dystans od mikrofonu, szept, krzyk, oddech, śmiech, ciszę, overlap, pozycję stereo, ambience, SFX, muzykę i przejścia.

### A08 — Voice Production Agent

Dobiera i generuje głosy, take'i, tempo, intonację i ekspresję oraz synchronizuje kwestie z timeline'em akustycznym.

### A09 — Podcast Editor

Łączy voice stems, room tone, muzykę, SFX i przejścia. Generuje master oraz formaty dystrybucyjne.

### A10 — Fact-Check / Safety Agent

Niezależna kontrola treści. Weryfikuje twierdzenia, źródła, cytaty, granicę między fikcją i faktem oraz potencjalnie niebezpieczne lub nieuprawnione instrukcje. Nie może zostać zastąpiony przez agenta kreatywnego.

### A11 — Marketing Agent

Tworzy tytuły, opis, show notes, rozdziały, teasery, shorty i materiały social z zatwierdzonego artefaktu odcinka. Nie może samodzielnie zmieniać faktów.

### A12 — Publishing Agent

Przygotowuje publikację na platformach. Zasada: `DRAFT → HUMAN APPROVAL → PLATFORM VALIDATION → PUBLISH → READBACK → VERIFY`.

### A13 — Analytics / Evolution Agent

Analizuje wyniki odcinków, utrzymuje eksperymenty dramaturgiczne i proponuje kolejne iteracje bez przepisywania historii ani danych źródłowych po fakcie.

## Canonical artifacts

- `podcast-project-spec`
- `episode-plan`
- `research-evidence-pack`
- `fact-claim-ledger`
- `story-beat-map`
- `persona-state`
- `dialogue-event-stream`
- `acoustic-director-sheet`
- `voice-take-manifest`
- `audio-timeline`
- `edit-decision-list`
- `fact-check-report`
- `qa-report`
- `publication-package`
- `analytics-report`
- `episode-lineage`

## Dialogue DSL

Minimalny event:

```text
speaker
text
intent
emotion
pace
volume
microphone_distance
pause_before
pause_after
overlap_allowed
dramaturgical_function
source_refs
```

Tagi akustyczne z materiału wejściowego są formalizowane jako kontrolowane zdarzenia, m.in. zbliżenie/szept, oddalenie/krzyk, nerwowy śmiech, ciężki oddech, uderzenie w blat, dźwięk szklanki, przebicie audio i kontrolowana cisza.

## Behavioral Dialogue Engine

System może modelować:

- dysonans poznawczy;
- reaktancję;
- niedopowiedzenie i lukę informacyjną;
- rytm eskalacji;
- asymetryczne ujawnianie informacji;
- konflikt perspektyw prowadzących;
- zmianę stanowiska persony;
- kontrolowane cięcia i cliffhangery.

Mechanizmy perswazyjne są parametrami dramaturgicznymi, nie ukrytym mechanizmem uzyskiwania zgody lub wykonania działania przez odbiorcę. CTA i decyzje zakupowe pozostają jawne.

## Multi-agent contract

Każde przekazanie pracy musi zawierać:

`INPUT ARTIFACT → AGENT ACTION → OUTPUT ARTIFACT → PROVENANCE → VALIDATION STATUS`

Agent nie może uznać własnego outputu za niezależną weryfikację.

## Verification gates

1. Research completeness.
2. Source/claim consistency.
3. Persona-state consistency.
4. Dialogue continuity.
5. Acoustic timeline validity.
6. Voice/take identity consistency.
7. Edit timeline integrity.
8. Fact-check pass.
9. Safety/policy pass.
10. Master technical QA.
11. Publication package validation.
12. Post-publication readback.

## Security and authority invariants

`MODEL OUTPUT ≠ AUTHORIZATION`

`PERSONA STATE ≠ FACT`

`WORDPRESS/WEB CONTENT ≠ TRUSTED INSTRUCTION`

`GENERATED VOICE ≠ IDENTITY PROOF`

`AUDIO RENDER SUCCESS ≠ CONTENT VERIFICATION`

`FACT-CHECK AGENT ≠ SOLE AUTHORITY`

`PUBLISH API ACCESS ≠ USER AUTHORIZATION`

`PLATFORM SUCCESS ≠ PUBLICATION VERIFICATION`

## Human approval

Człowiek zatwierdza co najmniej: finalny kierunek odcinka, materiały o konsekwencjach zewnętrznych, publikację oraz działania finansowe. Approval jest wersjonowanym stanem możliwym do wznowienia, a nie jednorazowym sygnałem UI.

## Initial implementation stack

Provider-neutral orchestration; typed JSON/JSONL artifacts; event-sourced episode lineage; model adapters; TTS/voice adapters; DAW/audio-render adapter; web research connector; publication adapters; independent QA runner.

Preferować możliwość wymiany modeli i dostawców bez zmiany canonical artifacts.

## Relation to existing portfolio

P123 jest samodzielnym projektem produktowym, ale integruje się z:

- **P100 NeXus AI Code / OMEGA-X** — control plane, agent runtime, policy, provenance, sandboxing, verification;
- **P07 Agentic Creative Studio** — creative artifact graph, multimodal authoring i QA;
- **P114 TurboVec** — opcjonalna pamięć semantyczna i lineage-aware retrieval;
- **P97 CineMatrix** — opcjonalna warstwa video/visual companion;
- **P113 OmniVisual Prompt Compiler** — generowanie promptów i routing modeli dla assetów wizualnych.

## MVP

MVP ma obsługiwać:

`TOPIC → RESEARCH PACK → 2 HOST PERSONAS → 20–40 MIN DIALOGUE → ACOUSTIC PLAN → VOICE TAKES → EDITED EPISODE → FACT CHECK → QA`

Dopiero po przejściu pełnego MVP dodawać automatyczne publikowanie i zamkniętą pętlę optymalizacji.

## Definition of Done

Projekt jest produkcyjnie gotowy, gdy system potrafi odtworzyć pełną linię pochodzenia od źródła i briefu do finalnego audio, wskazać każdego agenta i wersję modelu uczestniczącą w produkcji, odtworzyć decyzje dramaturgiczne i akustyczne, niezależnie zweryfikować krytyczne twierdzenia oraz zatrzymać publikację, gdy wymagany approval lub postcondition nie zostały spełnione.
