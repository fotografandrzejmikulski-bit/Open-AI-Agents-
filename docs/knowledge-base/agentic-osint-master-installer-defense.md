# Agentic OSINT / Master Installer — Defensive Architecture

## Source basis

Derived from the supplied report *Autonomiczne Ekosystemy Cyber-Wywiadowcze: Inżynieria Master Installer, Automatyzacja Wdrożenia i Kognitywna Synteza Danych*.

The source describes a layered Fusion Intelligence architecture spanning acquisition, normalization, cognitive synthesis, persistence and presentation, with technologies including APIs, local LLMs and graph/3D interfaces. fileciteturn328file2L957-L986

## Defensive adaptation

Operational offensive scanning, persistence and covert behavior described in source material are not adopted as unrestricted capabilities. OmniCore converts the useful architecture into an **authorized intelligence and evidence pipeline**.

```text
SCOPE / AUTHORIZATION
        |
        v
SENSOR / ACQUISITION
        |
        v
NORMALIZATION + SANITIZATION
        |
        v
EVIDENCE GRAPH
        |
        v
COGNITIVE SYNTHESIS
        |
        v
PROVENANCE / FRESHNESS / CONFIDENCE
        |
        v
HUMAN / POLICY REVIEW
        |
        v
REPORT / VERIFIED ACTION
```

## Layer model

### Sensor

Acquire only data permitted by explicit scope. The source identifies registries, scanners and APIs as acquisition sources. fileciteturn328file2L987-L1010

### Processing

Sanitize, normalize, deduplicate and structure incoming data before reasoning over it.

### Cognitive

Local or remote models may correlate evidence and generate hypotheses, but hypotheses remain separate from verified facts.

### Persistence

The source discusses auto-restart and persistent operation. OmniCore retains durable orchestration and resumability but rejects hidden persistence: services must be observable, revocable and explicitly configured.

### Presentation

Graph and 3D interfaces are projections of state, not authoritative state themselves.

## Master Installer

The installer pattern is retained as a deployment bootstrapper for legitimate infrastructure. A production implementation should be:

- idempotent;
- least-privilege;
- explicit about requested privileges;
- reversible;
- signed or integrity-checked;
- auditable;
- offline-capable where sovereignty requires it;
- unable to silently expand its own scope.

## Provenance-first OSINT

Every external observation should carry:

`source -> timestamp -> collection method -> authorization context -> transformation -> evidence status`

Conflicting sources remain separate until resolved by additional evidence.

## Core invariants

1. Passive collection is preferred.
2. Active scanning requires explicit scope and authorization.
3. Network rate limits are enforced outside the model.
4. Persistence is observable and revocable.
5. Installer privilege is explicit and least-privilege.
6. External intelligence is evidence, not authority.
7. Model synthesis cannot silently convert a hypothesis into fact.
8. Graph/3D presentation cannot mutate authoritative state without a typed capability path.
