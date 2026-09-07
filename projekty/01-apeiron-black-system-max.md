# APEIRON Black System — Maximum Upgrade Specification

**Input:** supplied `Index.html` and concept of the Apeiron card system.  
**Target:** transform the current visual demo into a production-grade interactive application while preserving its obsidian / UV / thermochromic identity.

## Current baseline

The source already contains a React card database, cards with rest/active/UV layers, terminal-style logs, random draws, UV toggling and table clearing. fileciteturn189file1L4-L15 fileciteturn189file1L72-L89 fileciteturn189file1L141-L176

## Maximum upgrade

### 1. Product architecture

```text
Apeiron UI
 ├─ Card renderer
 ├─ Draw/session state
 ├─ Interpretation engine
 ├─ Archive/history
 ├─ Accessibility layer
 └─ Visual system
          |
          v
 Application state machine
          |
   +------+------+
   |             |
 Rules engine   Optional AI
   |             |
   +------+------+
          |
     audit/event log
```

### 2. Replace ad-hoc randomness

The current draw uses `Array.sort(() => 0.5 - Math.random())`. Replace this with a Fisher–Yates shuffle backed by `crypto.getRandomValues()` where cryptographic-quality randomness is desired. Keep a seeded deterministic mode for reproducible tests.

### 3. Model card state explicitly

Create a typed state machine:

`IDLE → DRAWING → REVEALED → INSPECTING → UV_REVEAL → ARCHIVED`

No UI gesture should be able to create an impossible state.

### 4. Expand the card schema

```ts
type ApeironCard = {
  id: string;
  arcana: 'major' | 'void' | 'glitch' | 'memory' | 'system';
  archetype: string;
  title: string;
  descriptions: {
    dormant: string;
    active: string;
    uv: string;
  };
  symbolism: string[];
  tags: string[];
  riskLevel: 'low' | 'medium' | 'high';
  icon: string;
};
```

Use stable IDs instead of positional numeric assumptions.

### 5. Add deterministic interpretation

The application should distinguish **symbol generation** from **interpretation**. Every draw receives a structured event:

```json
{
  "sessionId": "...",
  "drawId": "...",
  "cards": ["..."],
  "mode": "single|debug|spread",
  "uv": false,
  "timestamp": "..."
}
```

An optional LLM layer may interpret this event, but cannot mutate the deck or authoritative session state without passing through typed actions.

### 6. MCP-ready capability surface

Potential read-only tools:

- `apeiron.list_cards`
- `apeiron.get_card`
- `apeiron.get_session`
- `apeiron.get_history`

Potential mutating tools:

- `apeiron.start_session`
- `apeiron.draw_cards`
- `apeiron.reveal_uv`
- `apeiron.archive_session`

Mutating capabilities should remain separate from read-only retrieval.

### 7. Accessibility upgrade

The existing interface is visually dominant. Add keyboard navigation, focus states, reduced-motion mode, semantic buttons, `aria-live` terminal output and a textual description for every card state.

### 8. Observability

Emit structured events instead of relying only on free-form strings:

```ts
type ApeironEvent =
  | { type: 'BOOT'; at: string }
  | { type: 'DRAW'; drawId: string; count: number; at: string }
  | { type: 'UV_ENABLED'; at: string }
  | { type: 'CARD_INSPECTED'; cardId: string; at: string }
  | { type: 'TABLE_CLEARED'; at: string };
```

Keep the terminal as a projection of the event stream.

### 9. Persistence

Persist the session separately from the UI. The source currently clears local state directly with `setDrawnCards([])` and `setIsSystemActive(false)`. fileciteturn189file1L172-L176

Upgrade to a durable session model where clearing the screen does not silently imply irreversible history deletion.

### 10. Visual system

Preserve:
- near-black obsidian surfaces;
- restrained emerald system telemetry;
- purple UV layer;
- thermochromic reveal metaphor;
- monospaced diagnostic typography.

Add a calibrated token system for spacing, elevation, glow intensity, border alpha, motion duration and responsive breakpoints.

### 11. Engineering hardening

- TypeScript strict mode.
- Unit tests for deck integrity and state transitions.
- Property-based tests for shuffle invariants.
- Component tests for visible/UV states.
- E2E test for draw → inspect → UV → clear.
- Snapshot tests for deterministic seeded draws.
- Error boundary for render failures.
- No secrets in client source.

### 12. AI integration boundary

If an AI oracle is added, its output must use a schema such as:

```json
{
  "reading": "string",
  "themes": ["string"],
  "confidence": 0.0,
  "disclaimer": "string"
}
```

The AI may explain a card; it cannot invent an authoritative card ID, modify the deck, or silently persist memory.

### 13. Maximum product direction

APEIRON should evolve from a visual card demo into a **stateful symbolic interaction engine** with three layers:

`Artifact → Ritual → Interpretation`

The card is the artifact, the session/draw sequence is the ritual, and deterministic + optional AI interpretation is the interpretation layer.

This keeps the original artistic concept intact while giving it the architecture required for a serious web application.
