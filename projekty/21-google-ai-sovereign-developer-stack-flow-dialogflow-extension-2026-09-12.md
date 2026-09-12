# P21 Extension — Google Flow / Dialogflow CX / Cloud Node.js Service Fabric

Date: 2026-09-12
Parent: P21 — Google AI Sovereign Developer Stack
Classification: EXISTING PROJECT EXTENSION

## Purpose
Extend the Google AI developer stack with three concrete service surfaces: Google Flow for multimodal creative production, Dialogflow CX Flows for explicit conversational state graphs, and Google Cloud Node.js client libraries for typed cloud-service integration.

## Unified architecture

```text
USER / DEVELOPER
      ↓
CANONICAL INTENT / STATE / ARTIFACT
      ↓
GOOGLE CAPABILITY REGISTRY
      ├── FLOW / VEO
      ├── DIALOGFLOW CX
      └── GOOGLE CLOUD NODE.JS CLIENTS
      ↓
AUTH / POLICY / DATA CLASSIFICATION
      ↓
PROVIDER EXECUTION
      ↓
READBACK / EVALUATION
      ↓
PROVENANCE / AUDIT
```

## Google Cloud Node.js

The official google-cloud-node repository becomes the service-adapter inventory for Node.js-based Google Cloud integration. P21 should record service client, API/version, release level, required APIs, authentication, IAM scope, side effects and verification timestamp.

## Dialogflow CX

Dialogflow CX Flow is modeled as an explicit state/route graph with pages, transition routes, route groups, event handlers, NLU settings and knowledge connectors.

This complements the P21 agentic runtime with a deterministic conversational control surface:

`INTENT → FLOW STATE → ROUTE → ACTION/FULFILLMENT → NEXT STATE`

## Google Flow

Flow adds a multimodal creative surface supporting images, video, characters, references, scenes and project-scoped assets. Its Agent adds conversational planning/generation/editing capabilities.

The provider remains a capability surface, not the canonical project state.

## Governance

- API credentials remain outside source control.
- Provider access is distinct from authorization.
- Generated Flow Tools are candidate software artifacts.
- Educational completion does not grant runtime privileges.
- Model/product availability is live metadata.
- Provider state is not authoritative project state.

## Verification

- service-client/API lifecycle tests;
- IAM and API-enable separation;
- Dialogflow Flow graph/readback tests;
- Flow model-feature compatibility tests;
- generated Tool security/provenance tests;
- cross-provider state/provenance tests;
- data-classification routing tests.

## Status

`ARCHITECTURE-ENHANCED / PROVIDER-VERIFICATION CONTINUES`
