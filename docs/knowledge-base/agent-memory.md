# Agent Memory — Sandbox Agents

This document archives the Agent Memory documentation supplied during project research.

## Core model

Sandbox-agent memory is separate from SDK conversational `Session` memory. `Session` stores message history; sandbox memory distills lessons from prior runs into files inside the sandbox workspace. Generated memory artifacts are retained data and must follow the same sensitivity and retention policy as the workspace.

## Enablement

Enable memory by adding `memory()` as a SandboxAgent capability.

Typical dependencies:
- `memory()` requires `shell()` when memory reading/search is enabled.
- Live memory update also requires `filesystem()` so the agent can update `memories/MEMORY.md`.

Useful modes:
- `memory()` — read and generate memories.
- `memory({ generate: false })` — read memory without generating new memory; useful for internal/checker/one-off subagents.
- `memory({ read: null })` — generate memory for later runs without letting the current run be influenced by existing memory.

## Persistence layout

Default workspace layout:

```text
workspace/
├── sessions/
│   └── <rollout-id>.jsonl
└── memories/
    ├── memory_summary.md
    ├── MEMORY.md
    ├── raw_memories.md
    ├── raw_memories/
    └── rollout_summaries/
```

Memory is reusable only when the configured `memories/` directory is preserved, for example by keeping the same live sandbox session or resuming from persisted `sessionState` or a snapshot. A fresh empty sandbox has empty memory.

## Progressive disclosure

At run start the SDK injects a compact `memory_summary.md` into the agent developer prompt. When prior work appears relevant, the agent searches `MEMORY.md` and opens individual rollout summaries only when more detail is required.

Memories may become stale. They are guidance, not authoritative current state. By default memory reads can live-update when stale information is detected; live updates can be disabled when memory should not be modified during the run.

## Memory generation

After a run finishes, the sandbox runtime appends the run segment to a conversation file. Conversation files can contain user input, assistant/tool items, interruptions, and final outputs.

Generation has two phases:

1. **Conversation extraction** — a memory-generating model processes an accumulated conversation file, produces a conversation summary and raw memory extract, omitting system/developer/reasoning content. Very long conversations are truncated to fit the model context, preserving beginning and end.
2. **Layout consolidation** — a consolidation agent reads raw memories for one layout, opens summaries when needed, and produces/consolidates `MEMORY.md` and `memory_summary.md`.

Generation can be configured with `memory({ generate: { ... } })`, including `maxRawMemoriesForConsolidation`, `phaseOneModel`, `phaseTwoModel`, and `extraPrompt`.

`extraPrompt` is intended to emphasize use-case-specific signals such as workflow corrections, verification commands, user preferences, customer/company details, etc.

When raw-memory count exceeds `maxRawMemoriesForConsolidation`, phase 2 keeps memories from the newest conversations and removes older ones. Recency is based on the last conversation update.

## Multi-turn memory conversations

For multi-turn sandbox chats, use the normal SDK `Session` together with the same live sandbox session when the turns should form one memory conversation.

Memory associates a run with a conversation identifier in this order:
1. `conversationId`
2. SDK session id
3. `groupId`
4. generated per-run ID

Using a stable identifier across `run(...)` calls causes those turns to append to one memory conversation file. This is distinct from the sandbox workspace identity.

## Memory isolation

Memory isolation is controlled by `MemoryLayoutConfig`, not by agent name.

Agents using the same memory layout and the same memory conversation ID share one memory conversation and consolidated memory. Agents using different layouts maintain separate rollout files, raw memories, `MEMORY.md`, and `memory_summary.md`, even when they share the same sandbox workspace.

Example pattern:

```js
const engineeringMemory = memory({
  layout: {
    memoriesDir: 'memories/engineering',
    sessionsDir: 'sessions/engineering',
  },
});

const financeMemory = memory({
  layout: {
    memoriesDir: 'memories/finance',
    sessionsDir: 'sessions/finance',
  },
});
```

This prevents unrelated domain knowledge from being consolidated into the wrong agent/domain memory.

## Architectural distinction

Keep the following separate:

- **Conversation state** — SDK `Session` / conversation history.
- **Sandbox state** — live workspace, session state, snapshots.
- **Sandbox memory** — distilled lessons/preferences/patterns persisted as workspace memory artifacts.

Memory is therefore a durable knowledge layer over sandbox runs, not a replacement for conversational history or sandbox persistence.
