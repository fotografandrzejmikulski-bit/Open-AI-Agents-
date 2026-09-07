# MCP i platformy Agent AI — druga warstwa wiedzy

> Data analizy: 2026-09-07
> Zakres: źródła wskazane przez użytkownika dotyczące MCP, frameworków agentowych i platform low-code/no-code.
> Metoda: ekstrakcja wzorców architektonicznych i praktyk implementacyjnych z materiałów oficjalnych oraz z oficjalnych repozytoriów tam, gdzie były dostępne. Nie jest to line-by-line crawl każdej strony.

## 1. Model Context Protocol — warstwa bazowa

MCP należy traktować jako **protokół capability integration**, a nie jako framework agentowy. Jego zadaniem jest ustandaryzowanie połączenia hosta AI z zewnętrznymi serwerami udostępniającymi kontekst i operacje.

### Architektura

W praktyce należy utrzymywać trzy granice:

```text
Host AI
  |
  +-- Client MCP
  |
  +-- polityka / consent / lifecycle / permissions
          |
          v
      MCP Server
          |
          +-- Tools
          +-- Resources
          +-- Prompts
```

Host zachowuje odpowiedzialność za politykę, zgodę użytkownika, lifecycle połączeń i integrację z modelem. Serwer MCP powinien udostępniać wąskie, stabilne capabilities.

### Trzy główne prymitywy

| Prymityw | Sterowanie | Zastosowanie |
|---|---|---|
| Tools | model-controlled | wykonanie operacji, wywołanie API, mutacje |
| Resources | application-controlled | dostarczanie danych/kontekstu |
| Prompts | user-controlled | gotowe szablony instrukcji |

To rozdzielenie jest ważnym wzorcem projektowym: **dane, instrukcje i skutki uboczne nie powinny być modelowane jako jedna niejawna powierzchnia**.

### Build / test / registry

Oficjalny ekosystem obejmuje SDK w wielu językach, MCP Inspector do testowania serwerów oraz Registry przechowujące metadane publikowanych serwerów. Registry jest warstwą dystrybucji/metadata, a nie substytutem runtime authorization.

W aktualnym repozytorium MCP widoczne są także prace nad uproszczeniem/bezsesyjnym HTTP oraz dalszym rozwojem mechanizmów auth; oznacza to, że implementacja produkcyjna powinna być projektowana pod aktualną specyfikację, a nie pod historyczne założenia dotyczące transportu.

### Auth

Dla HTTP MCP należy myśleć w kategoriach OAuth 2.1, protected resource metadata, authorization-server metadata i precyzyjnego wskazania resource. OAuth client-credentials jest odrębnym przypadkiem dla integracji machine-to-machine.

**Wniosek:** authorization jest granicą integracji, nie odpowiedzialnością promptu.

## 2. MCP Registry

Registry pokazuje dodatkową warstwę systemową, często pomijaną przy budowie własnych integracji:

```text
Source repository / package
        |
        v
MCP publisher
        |
        v
Registry metadata
        |
        v
Discovery by clients / tooling
```

Warto rozdzielić:
- artefakt serwera;
- jego metadata i wersję;
- publikację/discovery;
- runtime authentication;
- stan użytkownika.

Oficjalne materiały Registry wskazują, że warstwa registry nie jest miejscem przechowywania stanu uwierzytelnienia użytkowników. To dobry wzorzec również dla własnych katalogów integracji.

## 3. OpenAI / Anthropic jako klienci MCP

Materiały dotyczące ChatGPT/MCP oraz Claude Code są ważne nie dlatego, że uczą budowy serwera od zera, ale dlatego, że pokazują różnicę między **protokółem** a **polityką klienta**.

Serwer MCP może być zgodny z protokołem, a mimo to konkretnego klienta obowiązują dodatkowe reguły dotyczące:
- sposobu logowania;
- consent/approval;
- zakresu narzędzi;
- widoczności wyników;
- lifecycle sesji;
- sposobu konfiguracji.

Dlatego test "MCP Inspector działa" nie oznacza jeszcze "integracja z ChatGPT/Claude działa poprawnie".

## 4. Frameworki kodowe — LangGraph, CrewAI, AutoGen

### LangGraph / LangChain

Kluczowa idea LangGraph to **graf wykonawczy**: agent nie musi być pojedynczą funkcją, lecz stanową siecią kroków z rozgałęzieniami, pętlami i możliwością kontrolowania przepływu. W praktyce jest to szczególnie użyteczne wtedy, gdy proces ma jawny stan i potrzebuje deterministycznych punktów przejścia pomiędzy decyzjami modelu.

Wzorzec:

```text
State
  |
  +--> model decision
  |       |
  |       +--> tool
  |       +--> branch
  |       +--> human review
  |
  +<------ next node / cycle
```

**Wniosek architektoniczny:** graf jest dobrym wyborem, gdy przejścia i stan są częścią domeny, a nie tylko przypadkowym skutkiem kolejnych wywołań LLM.

### CrewAI

CrewAI porządkuje system wokół agentów pracujących w zespołach/crew. Każdy agent ma rolę, kontekst i narzędzia, a zadania są delegowane zgodnie z konfiguracją zespołu.

W dokumentacji widać wzorzec:

```text
Agent role + backstory + tools
              |
              v
            Task
              |
              v
             Crew
```

To dobry model do organizowania **specjalizacji semantycznej**, ale nie należy traktować samej liczby agentów jako miary jakości architektury. Agent powinien powstać wtedy, gdy różni się jego odpowiedzialność, narzędzia, instrukcje lub polityka wykonania.

Oficjalne materiały CrewAI pokazują również, że narzędzia są częścią definicji agenta, a więc capability boundary może być projektowane na poziomie specjalisty.

### Microsoft AutoGen

AutoGen rozdziela warstwy. AgentChat jest warstwą wysokiego poziomu dla interaktywnych, zadaniowych aplikacji agentowych, podczas gdy `autogen-core` daje event-driven model wykonawczy o większej kontroli.

To daje użyteczną analogię:

```text
High-level agent conversation
          |
          v
    AgentChat layer
          |
          v
 Event-driven runtime/core
```

AutoGen pokazuje też kilka klas organizacji zespołu agentów: round-robin, selector/group chat i grafy przepływu. `GraphFlow` jest przy tym oznaczony jako eksperymentalny w analizowanym źródle, więc nie należy traktować eksperymentalnego API jako stabilnego kontraktu produkcyjnego bez dodatkowej weryfikacji.

**Wniosek:** AutoGen jest szczególnie interesujący jako model separacji "łatwe API" od "runtime control plane".

## 5. OpenAI Agents SDK jako punkt odniesienia

Na tle tych frameworków OpenAI Agents SDK utrzymuje prostszą jednostkę bazową: Agent + Runner + tools + opcjonalnie handoffs, guardrails, sessions i structured output.

Kluczowa różnica architektoniczna nie polega na tym, że SDK nie może budować złożonych systemów. Polega na tym, że jego podstawowy model zachęca do rozpoczęcia od **jednego skupionego agenta**, a dopiero potem rozdzielania odpowiedzialności.

Reguła porównawcza:

| Problem | Preferowany wzorzec |
|---|---|
| pojedynczy agent z narzędziami | Agents SDK |
| jawny graf stanów i cykle | LangGraph / graph-style runtime |
| role i zespoły specjalistów | CrewAI / AutoGen teams |
| protokół capability integration | MCP |
| deterministyczna automatyzacja | workflow engine |

To są warstwy komplementarne. MCP nie konkuruje z Agents SDK, a framework agentowy nie powinien zastępować warstwy deployment/workflow.

## 6. n8n — workflow jako deterministic control plane

n8n pokazuje bardzo ważny wzorzec hybrydowy: agent może używać narzędzi, ale MCP może również być używane bezpośrednio jako element deterministycznego workflow.

W kodzie n8n widoczna jest osobna powierzchnia `McpClientTool` oraz integracja MCP z warstwą agentów. Oznacza to dwa tryby:

```text
A. Model-driven
Agent -> MCP Tool -> system

B. Workflow-driven
Workflow -> MCP Client -> tool
```

To istotne, ponieważ nie każda integracja z MCP wymaga LLM. Gdy ścieżka jest znana, bezpieczniej i taniej jest wykonać ją deterministycznie.

### Walidacja schema/runtime

Kod n8n zwraca uwagę na zgodność schematu narzędzia z rzeczywistymi parametrami runtime. To wzmacnia ogólną zasadę:

> schema nie jest dokumentacją obok implementacji; schema jest kontraktem wykonawczym.

### MCP registry i OAuth

n8n posiada osobne warstwy klienta MCP oraz integrację z registry/OAuth. Wniosek dla własnych systemów: discovery, credentials i runtime execution powinny być rozdzielone, nawet gdy użytkownik widzi je jako jedną funkcję UI.

## 7. FlowHunt, Botpress i low-code agent builders

Źródła wskazane przez użytkownika pozycjonują FlowHunt i Botpress przede wszystkim jako warstwę szybkiego budowania konwersacyjnych agentów i prototypów.

Najważniejsza wiedza architektoniczna nie brzmi "zbuduj wszystko low-code", lecz:

- low-code przyspiesza składanie workflow i integracji;
- warstwa danych, credentials i deployment nadal wymaga jawnego modelu bezpieczeństwa;
- wraz ze wzrostem złożoności potrzeba rozdzielenia workflow, agent reasoning i backend capabilities.

Botpress należy traktować przede wszystkim jako conversational/product layer, a nie jako zamiennik protokołu MCP czy ogólnego runtime infrastrukturalnego.

## 8. Głębsza synteza: agent ≠ workflow ≠ MCP

Najważniejszy wniosek z całego pakietu materiałów:

```text
                    +------------------+
                    |      AGENT       |
                    | model-directed   |
                    | planning/reason  |
                    +--------+---------+
                             |
                             v
                    +------------------+
                    |   TOOLS / MCP    |
                    | capabilities     |
                    +--------+---------+
                             |
           +-----------------+-----------------+
           |                 |                 |
           v                 v                 v
       API / DB          workflow          sandbox
           |                 |                 |
           +-----------------+-----------------+
                             |
                             v
                    +------------------+
                    | infrastructure   |
                    | / deployment     |
                    +------------------+
```

Workflow jest kontrolowany przez aplikację. Agent jest kontrolowany częściowo przez model. MCP jest protokołem, przez który capabilities stają się interoperacyjne.

Najbardziej dojrzałe systemy będą zatem **hybrydowe**, a nie "w pełni agentowe".

## 9. Specjalizacja agentów — praktyczna reguła

Wspólny wzorzec OpenAI/CrewAI/AutoGen/LangGraph pozwala sformułować mocną heurystykę:

**Dodaj osobnego agenta tylko wtedy, gdy występuje istotna różnica w co najmniej jednej z warstw:**

1. instrukcje/polityka;
2. zestaw narzędzi/MCP;
3. model lub wymagany profil rozumowania;
4. format wyniku;
5. odpowiedzialność za końcową decyzję;
6. wymagania bezpieczeństwa lub approval.

Samo "agent 1 robi X, agent 2 robi Y" nie jest wystarczającym uzasadnieniem.

## 10. MCP Registry + Skills + Agent runtime

Wiedzę z tego pakietu można połączyć z wcześniej zapisanym modelem OpenAI:

```text
Skill
  -> uczy agenta JAK pracować

MCP / Tool
  -> daje agentowi DO CZEGO ma dostęp

Agent runtime
  -> decyduje CO zrobić i w jakiej kolejności

Workflow
  -> gwarantuje JAK przebiega proces, gdy kolejność jest znana

Registry
  -> umożliwia DISCOVERY capability

Sandbox
  -> izoluje GDZIE wykonywany jest nieufny kod

Guardrails/Auth
  -> określa CZY dana operacja jest dozwolona
```

To rozdzielenie należy zachować także w strukturze przyszłego repozytorium agenta.

## 11. Wnioski produkcyjne

### MCP

Projektować serwer jako mały, stabilny contract surface. Read/discovery oddzielać od mutation. Auth wykonywać po stronie serwera. Nie zwracać sekretów w wynikach.

### Framework

Najpierw określić model wykonania: prosty agent, graf, zespół specjalistów czy workflow. Dopiero później wybierać bibliotekę.

### Low-code

Używać do skrócenia drogi od pomysłu do działającego procesu, ale nie mieszać logiki biznesowej, credentials, stanu i reasoning w jednym wizualnym bloku.

### Operacyjnie

Każdy system powinien mieć jawne rozdzielenie:
`development -> preview/staging -> production`.

Dla operacji nieodwracalnych należy dodać approval oraz możliwość retry/resume/rollback.

## 12. Weryfikacja źródeł użytych w tej rundzie

Najmocniejsze aktualne źródła techniczne w tej rundzie:

- `modelcontextprotocol/modelcontextprotocol` — specyfikacja i dokumentacja MCP. Repozytorium było aktualizowane 2026-09-07. fileciteturn133file0L1-L12
- `modelcontextprotocol/registry` — architektura Registry i metadata/versioning. fileciteturn140file0L1-L18 fileciteturn140file1L20-L38
- OpenAI Agents SDK Python — Agent/Runner oraz domyślne użycie Responses API. fileciteturn111file0L1-L10
- CrewAI — role agentów i przypisywanie tools. fileciteturn136file0L1-L14
- Microsoft AutoGen — rozdzielenie AgentChat i event-driven Core. fileciteturn137file0L1-L20 fileciteturn137file1L29-L49
- n8n — MCP Client Tool i integracja MCP z agentami. fileciteturn139file0L1-L21 fileciteturn139file1L23-L51

## 13. Granice pewności

Dla części serwisów wskazanych wyłącznie jako strony produktowe (np. FlowHunt, Botpress oraz część materiałów Anthropic/OpenAI Learn) nie wykonano w tej rundzie kompletnego crawl wszystkich stron, ponieważ dostępny kanał narzędziowy w tej sesji zapewniał bezpośredni, aktualny dostęp przede wszystkim do repozytoriów GitHub. Wnioski dotyczące tych platform są więc traktowane jako warstwa architektoniczna, nie jako pełna dokumentacja funkcjonalna.
