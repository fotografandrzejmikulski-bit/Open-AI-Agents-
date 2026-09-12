# P100 Extension — Iteration 60 — Mobile AI, Local Models, Builders and Supply Chain

## Scope

This extension adds evidence from the 2026-09-12 corpus to the existing Nexus AI Code / GitHub DevSecOps control plane.

## 1. Local model provider class

Ollama is represented as a local inference provider/runtime exposing CLI, REST API, SDKs, model import/Modelfile workflows and integrations with coding agents and assistants.

Provider record additions:

```yaml
locality: local|remote|hybrid
model_runtime: string
api_surface: [cli,rest,sdk]
data_residency: local|provider_defined|unknown
hardware_requirements: object
agent_integrations: []
observed_at: timestamp
```

The user's `fotografaandrzej333/ollama` repository is a fork of `ollama/ollama` and must be tracked as derived source, not upstream authority.

## 2. OpenRouter / gateway class

OpenRouter is treated as a model gateway/provider candidate. Applications can route across providers while retaining a capability-first abstraction.

`GATEWAY ≠ AUTHORIZATION`

Routing still requires capability matching, policy and verification.

## 3. Builder governance

Plasmic, GrapesJS, Builder and open-source low-code systems strengthen the builder registry with:

- license;
- open-source vs open-core status;
- self-hosting;
- data control;
- paid-feature boundaries;
- SSO/RBAC availability;
- extensibility;
- maintenance burden;
- production readiness.

`PUBLIC REPOSITORY ≠ FULLY OPEN PRODUCT`

## 4. GitHub artifact lineage

GitHub's current artifact metadata API provides a digest-oriented bridge between artifacts, deployment records and provenance attestations.

Required lineage:

```text
SOURCE REVISION
↓
BUILD RUN
↓
ARTIFACT DIGEST
↓
ATTESTATION / PROVENANCE
↓
DEPLOYMENT RECORD
↓
RUNTIME OBSERVATION
```

## 5. npm supply-chain integration

npm trusted publishing provides OIDC-based workflow authentication and automatic provenance for supported public-package publishing flows. The control-plane model should prefer short-lived workflow identity over long-lived publish tokens where supported.

`PUBLISH CREDENTIAL ≠ PERMANENT SECRET`

`PROVENANCE ≠ MALWARE-FREE GUARANTEE`

## 6. Electron baseline

Electron's current security checklist reinforces:

- secure content only;
- context isolation;
- process sandboxing;
- CSP;
- restricted navigation/window creation;
- validated IPC senders;
- safe external-link handling;
- current Electron versions;
- limited Electron API exposure to untrusted content.

These become release-gate checks for Electron-based desktop artifacts.

## 7. CodeQL

CodeQL remains the semantic security layer capable of querying code as structured data and identifying vulnerability variants across supported languages/frameworks.

It is a security signal, not a complete proof of absence of vulnerabilities.

## 8. Agentic-abuse threat model

SentinelOne's Predator AI research demonstrates the pattern of an LLM interface sitting above multiple attack-oriented utilities. The control-plane threat model should therefore classify:

`LLM + TOOL AGGREGATION + CLOUD TARGETING`

as an agentic-abuse pattern requiring authorization boundaries, telemetry and abuse controls.

## Definition of integration

P100 now treats local models, model gateways, application builders and software-supply-chain evidence as parts of one governed capability graph rather than unrelated tooling lists.
