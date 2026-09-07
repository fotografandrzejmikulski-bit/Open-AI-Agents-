# Canonical Project Portfolio — 2026-09-07

This index is the canonical home for projects that are not part of a specific grant/hackathon submission.

## Projects originating from the newly supplied corpus

| ID | Project | Status |
|---|---|---|
| 37 | CogniSync Professional | Reference / hackathon-derived |
| 38 | Sovereign Edge AI | Architecture / benchmark program |
| 39 | Open Creator Layer | MVP architecture |
| 40 | Influence Literacy & Human Agency Lab | Defensive research product |
| 41 | AI Content Product Studio | Product design |

## Canonical separation rule

The dedicated `Agents-for-Humans-Hackathon` repository is the competition submission repository. It must contain only the work necessary to build, demonstrate, evaluate and submit CogniSync Professional.

The broader project portfolio belongs here under `projekty/`.

The accumulated reference material belongs under `docs/knowledge-base/`.

## Shared architecture

```text
                 USER INTENT
                      │
                CONTROL PLANE
       ┌──────────────┼──────────────┐
       │              │              │
   Evidence        Policy          Routing
   / Memory      / Consent      / Reasoning
       │              │              │
       └──────────────┼──────────────┘
                      │
                AGENT RUNTIME
                      │
               CAPABILITY BROKER
                      │
            MCP / Skills / APIs
                      │
                VERIFICATION
                      │
             HUMAN DECISION GATE
                      │
          ACTION / ARTIFACT / AUDIT
```

The reusable insight across the portfolio is that model intelligence alone is not a complete product. Reliability, provenance, authorization, evaluation and controlled capability access form the operational control plane around the model.

## Safety boundary

Projects involving influence, behavior, perception or persuasive systems are defensive by default. Analysis of potentially manipulative techniques may be used to detect or disclose them, but not to build covert psychological-control mechanisms.
