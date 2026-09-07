# Canonical Project Portfolio — 2026-09-08

This index is the canonical home for projects that are not part of a specific grant/hackathon submission.

## Newly reconciled project family

| ID | Project | Status |
|---|---|---|
| 37 | CogniSync Professional MAX | Production-oriented proactive professional agent |
| 38 | Sovereign Edge AI MAX | Canonical sovereign/local-edge execution program |
| 39 | OmniCore Alibaba Cloud Agent Runtime & Cloud Fabric MAX | Cloud execution substrate |
| 40 | OmniCore Agentic Development & Visual Intelligence Fabric MAX | Coding + live multimodal execution |
| 41 | OmniCore Repository Intelligence & Multimodal Action Fabric MAX | Repository/world/evidence intelligence |
| 42 | Open Creator Layer MAX | Engine-on-engine creator platform |
| 43 | Influence Literacy & Human Agency Lab MAX | Defensive influence-security research product |
| 44 | AI Content Product Studio MAX | Content production system |
| 45 | OmniCore Agentic Content & Commerce Factory MAX | Evidence-backed content-to-commerce orchestration |
| 46 | CogniSync Open Creator Influence & Content Nexus MAX | Cross-domain product integration |
| 47 | OmniCore Portfolio Integrity & Project Registry MAX | Canonical portfolio identity and lineage |

## Legacy reconciliation

The repository originally contained two distinct Project 38 artifacts: a sovereign-edge specification and a scientific-stability verifier. The sovereign-edge specification is now the canonical Project 38; the scientific-stability artifact remains preserved as a separate historical/research artifact and is referenced through lineage rather than forced into a conflicting numeric identity.

The original Project 39 Open Creator Layer has been promoted to canonical **Project 42**. The original Project 40 Influence Literacy & Human Agency Lab has been promoted to canonical **Project 43**. The original Project 41 AI Content Product Studio has been promoted to canonical **Project 44**.

The previous OmniCore Projects 39–41 remain valid artifacts from an earlier evolution of the architecture; they are not deleted. Their lineage and integration role are recorded in Project 47.

## Canonical separation rule

The dedicated `Agents-for-Humans-Hackathon` repository is the competition submission repository. The broader engineering portfolio belongs here under `projekty/`, while accumulated source material belongs under `docs/knowledge-base/`.

## Shared architecture

```text
                         USER / OPERATOR
                                │
                       INTENT / REQUIREMENTS
                                │
                     CANONICAL PROJECT REGISTRY
                                │
                         CONTEXT COMPILER
                                │
        ┌───────────────────────┼───────────────────────┐
        ↓                       ↓                       ↓
 REPOSITORY GRAPH          WORLD STATE GRAPH       EVIDENCE GRAPH
        │                       │                       │
        └───────────────────────┼───────────────────────┘
                                ↓
                         AGENT / MODEL ROUTER
                                ↓
                       TYPED CAPABILITY PLAN
                                ↓
                         CAPABILITY BROKER
                                ↓
                     DETERMINISTIC EXECUTION
                                ↓
                  AUTHORITATIVE READBACK
                                ↓
                POSTCONDITION / POLICY VERIFY
                                ↓
                  ARTIFACT + STATE DELTA
                                ↓
                    EVAL / AUDIT / RELEASE
```

## Portfolio engineering invariants

1. Project identity is resolved through canonical registry, not filename alone.
2. Prompt is task specification, never the security boundary.
3. Model choice does not grant authorization.
4. Tools are typed capabilities with explicit side effects.
5. Consequential actions require authoritative postcondition verification.
6. Stale turns cannot overwrite newer state.
7. Repository, world and evidence state are versioned.
8. Multi-model agreement is not proof when assumptions are correlated.
9. Actual execution identity determines metering.
10. Cloud/edge/local routing may optimize cost and latency but cannot lower mandatory security controls.
11. Influence-oriented systems are defensive by default.
12. Legacy project lineage is preserved rather than silently overwritten.
