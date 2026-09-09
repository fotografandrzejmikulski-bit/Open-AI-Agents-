# Sovereign Local-First AI Masterplan & Hybrid Edge Runtime — 2026-09-09

## Sources
- `Masterplan 2026_ Komendy dla AI do budowy Suwerenn....pdf`
- `Masterplan 2026- Komendy dla AI do budowy Suwerenn....pdf`

The two supplied Masterplan files are treated as duplicate source lineage.

## Source-derived architecture
The masterplan defines a four-stage path: automated infrastructure, backend logic using Genkit/Ollama, browser/edge AI and mobile on-device AI. fileciteturn182file3L126-L140

The source proposes Infrastructure-as-Code through Project IDX/dev.nix and a local Ollama environment, then a typed Genkit flow using Zod schemas. fileciteturn182file3L142-L158

Its edge layer specifies a browser abstraction with availability checks, streaming and graceful degradation to the backend. The mobile layer proposes Android on-device inference and explicit model loading/error handling. fileciteturn182file13L600-L630

## Generalized runtime
```text
USER INTENT
 ↓
CAPABILITY / DEVICE CHECK
 ↓
LOCAL EDGE MODEL
 ↓ unavailable / insufficient
SOVEREIGN BACKEND
 ↓
VERIFIED RESULT
 ↓
AUDIT / STATE / COST METRICS
```

## Engineering doctrine
- model/provider agnosticism;
- local-first execution;
- graceful degradation;
- explicit capability detection;
- typed interfaces;
- versioned deployment;
- verification before promotion;
- no assumption that a named model/API remains available forever.

## Important source-status note
Model names, browser APIs, package versions, quotas and deployment economics in the supplied document are time-sensitive implementation claims. They must be revalidated before production use.

## Portfolio impact
Strengthens Projects 21, 31, 37, 38, 39, 65 and 72. No new numbered project required because the repository already has sovereign runtime and agentic factory lineages.
