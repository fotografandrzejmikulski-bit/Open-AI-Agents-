# Telephony, SMS, eSIM and Mobile-Identity Architecture — Repository Synthesis

> Evidence class: source-derived repository analysis → engineering synthesis.
>
> Scope: architecture, capability boundaries, security, lifecycle/state modeling, mobile/eSIM execution, observability and agent integration. Verification-bypass and anonymity-evasion behaviors are treated only as defensive threat patterns.

## 1. Executive finding

The reviewed repositories form four distinct capability families:

1. **Virtual telephony / SMS providers** — provisioning, activation lifecycle, status polling, forwarding, provider abstraction and inbox state.
2. **MCP/agent integration** — exposing provider operations as typed tools and translating provider-specific state into agent-consumable results.
3. **eSIM/LPA mobile execution** — local profile management, reader/device adapters, native bridges, QR decoding and cross-platform capability declaration.
4. **Simulation / semantic matching** — deterministic compilation/simulation pipelines and entailment/response-selection models that can strengthen verification, contradiction detection and multi-turn context handling.

The strongest reusable design pattern is not “virtual numbers” itself. It is a **governed identity-and-telecom capability plane** that treats phone numbers, SIM/eSIM profiles, eUICCs, SMS inboxes, provider accounts, QR artifacts and device adapters as separate typed resources with explicit ownership, authorization, lifecycle and postcondition verification.

## 2. Source observations

### 2.1 VirtualPhoneNumber

The repository is essentially a catalog of public/free virtual-number services rather than a maintained software stack. Its primary engineering value is as a **threat-intelligence input**: shared/ephemeral numbers, public inboxes, uncertain ownership and weak provenance create verification-fraud, privacy leakage and identity-correlation risks.

### 2.2 SMSProxy

The project describes a simple architecture in which one virtual number proxies multiple SMS conversations. The useful abstraction is **identity virtualization plus conversation routing**. A modern equivalent needs explicit tenant/session binding, message correlation IDs, retention rules, consent, anti-cross-tenant leakage and auditable routing decisions.

### 2.3 Twilio Virtual Phone

The project provisions virtual telephony through provider credentials and persists application state in PostgreSQL with Redis also required. This is a useful reference for a **stateful provider adapter**: external provider → API boundary → durable state → cache/queue → application/UI. The old Heroku deployment model is historical, not a production recommendation.

### 2.4 Grizzly SMS MCP

This is the most direct agent-integration reference. The MCP server defines Zod-backed request schemas, maps service names to service codes, supports provider/country/price constraints, exposes number acquisition/status/price/country/service operations and supports both stdio and Streamable HTTP transports. The client normalizes provider responses into activation IDs, phone numbers and lifecycle statuses.

Useful abstraction:

`Agent → MCP tool contract → capability broker → provider adapter → activation resource → authoritative status readback`

Security correction for OmniCore: API keys should never be requested or exposed as ordinary conversational data; activation/OTP data should be treated as secrets with short retention, redaction and explicit policy gates. Browser-driven registration flows must not be copied for account-verification bypass or abuse.

### 2.5 TempSMS

This repository scrapes a public SMS site with HTTP requests and HTML parsing to enumerate countries, numbers and recent message rows. Its main reusable lesson is negative: **web scraping is not a trustworthy identity substrate**. Public inboxes need provenance labels, freshness, source reputation and privacy boundaries, and scraped message content must be considered untrusted external data.

### 2.6 OnlineSimBot

The bot combines a messaging UI with a virtual-number provider, filters available numbers, presents per-number state and exposes an inbox. The repository also contains explicit network-filtering bypass behavior; that is retained only as a defensive threat pattern. The architecture lesson is session-scoped ephemeral resource allocation and user-facing lifecycle controls.

### 2.7 ion-intl-tel-input

The phone input model separates:

`dialCode + internationalNumber + isoCode + nationalNumber`

and provides validation, country selection, preferred/allowed country lists and UI events. This should become a canonical `PhoneIdentity` boundary in OmniCore. **Normalization/validation is not proof of ownership or authentication.**

### 2.8 terraform-ibm-landing-zone-vsi

The module demonstrates IaC-driven bootstrap of logging and monitoring agents, OS-aware package selection, cloud-init command composition, tags and collector configuration. It is directly relevant to monitorability-aware infrastructure. A notable security issue in the sampled configuration is `--check_certificate false`; OmniCore must enforce certificate verification by policy and fail closed on invalid trust configuration.

Reusable pattern:

`InfrastructureSpec → OS/image capability detection → bootstrap plan → observability agents → durable logs/metrics → policy/audit`

### 2.9 Virtuoso

Virtuoso wraps Java 21 virtual threads and provides thread/future/executor abstractions plus `map`, `pmap` and futures. The repository explicitly documents that unbounded parallel I/O can hit system limits and recommends bounded chunking for large network workloads.

OmniCore implication: telecom/eSIM capability fan-out should use **bounded concurrency, deadlines, cancellation, backpressure and provider-specific rate limits**, even when the underlying runtime supports cheap virtual threads.

### 2.10 User fork: virtual-phone

The fork of the historical `anark/virtual-phone` project is valuable as an old example of provider-neutral adapters: `twilio` versus `tropo`, environment-driven configuration and callback URLs for incoming calls. It strongly aligns with the existing OmniCore provider-neutral adapter doctrine. It is legacy Rails-era architecture and should be treated as lineage, not as a modern dependency choice.

### 2.11 User fork: eSim (FOSSEE electronics simulation)

This `eSim` is an electronics/EDA simulator, not telecom eSIM. Its architecture provides a very useful compiler/simulation pattern: schematic → validated model → intermediate/netlist representation → executable simulation → RAW output → plotting; mixed-signal flows bridge VHDL/Verilog and Ngspice. Security documentation explicitly identifies crafted project/netlist files and insecure temporary/permission handling as important attack surfaces.

OmniCore reuse:

`intent → typed model → normalized IR → deterministic execution → result artifact → verification`

This pattern should be applied to eSIM profile plans and device operations: never execute a high-impact profile mutation directly from model output; compile it into a typed operation graph and verify authoritative device state afterward.

### 2.12 eSim-Cloud

The cloud project demonstrates a web IDE around circuit design and simulation with React/Angular front ends, Django REST middleware, Celery/Redis, Docker and multiple database options. It is useful as a reference for **visual builder + asynchronous execution + sandboxed backend + artifact export + validation**. This maps well to the existing Agentic App Builder and simulation projects.

### 2.13 Alibaba ESIM response selection

This repository uses the ESIM acronym for a multi-turn response-selection model. It preprocesses context, trains word2vec embeddings and trains/tests an ESIM model on conversational data. Its value for OmniCore is semantic matching and multi-turn context handling, not telecom.

### 2.14 coetaur0/ESIM

This repository is the PyTorch implementation of Enhanced Sequential Inference Model for natural-language inference. It supports SNLI/MultiNLI/BNLI preprocessing, checkpointed training and evaluation. It provides a useful legacy reference for **entailment/contradiction classification and reproducible evaluation pipelines** that can support evidence contradiction analysis.

### 2.15 Silentely/eSIM-Tools

This is one of the highest-value sources. The project is an eSIM-management toolkit with a local-first web architecture, a BFF/Edge proxy boundary, authentication middleware, CSP, local/session state handling, QR generation, resumable flows and explicit security checks. Its project guidance emphasizes code-grounded retrieval, cross-verification, module structure, state management and production diagnostics.

The architecture is especially reusable for OmniCore:

- `BFF/Edge` separates browser UI from protected credentials.
- `withAuth` centralizes authentication/CORS/request validation.
- state manager and recoverable points support resumable workflows.
- security tooling and dependency audits become release gates.
- agent-readable `CLAUDE.md` and `llms.txt` show that repositories themselves can expose structured machine guidance.

Do not treat the repository's claims about local processing, service windows or third-party activation paths as independently verified facts without testing.

### 2.16 NekokoLPA

The project is a cross-platform LPA application. The README describes Android/iOS reader support including Android OMAPI and USB CCID, iOS CryptoTokenKit, and a device-adapter abstraction registered through `src/lpa/adapters/`. The current package definition uses React Native, TypeScript, native module code generation, Redux state, camera/QR support, BLE support and platform-specific build scripts. The repository also describes a newer NekokoLPA 2 line with broader platform/telephony support; that future release claim should be treated as source-derived roadmap information until independently verified.

This is the strongest reference for **mobile eUICC/eSIM control-plane separation**:

`UI/features → LPA domain → device adapter → native bridge → physical/eUICC substrate`

The adapter contract is directly compatible with the OmniCore capability-broker model.

### 2.17 free-esim

The repository presents an eSIM connectivity/trial product with QR activation and a multi-service web infrastructure story. The technical content is lightweight, but it is useful for **product/acquisition threat modeling**: free-trial abuse, device eligibility, entitlement issuance, QR replay, allocation fairness and partner/service trust should be modeled separately from the marketing layer. Claims about coverage, performance and integrations remain source claims until verified.

## 3. Canonical OmniCore resource model

Separate these resources; do not collapse them into “phone” or “eSIM”:

```text
PhoneIdentity
  ├─ dialCode
  ├─ internationalNumber
  ├─ nationalNumber
  ├─ isoCode
  └─ ownership/proof state

TelecomNumberResource
  ├─ provider
  ├─ allocationId
  ├─ lifecycle state
  ├─ validity window
  └─ authorization scope

SmsConversation
  ├─ sessionId
  ├─ numberResourceId
  ├─ message IDs
  ├─ retention policy
  └─ correlation metadata

SmsSecret
  ├─ activationId
  ├─ OTP/code
  ├─ issuedAt
  ├─ expiresAt
  └─ redaction policy

EuiccProfile
  ├─ profile identity
  ├─ subscription/activation metadata
  ├─ lifecycle state
  ├─ target eUICC/device
  └─ provenance

LpaDevice
  ├─ adapterId
  ├─ platform
  ├─ reader type
  ├─ capabilities
  └─ trust state

QrActivationArtifact
  ├─ artifactId
  ├─ payload provenance
  ├─ issuedAt
  ├─ expiry/replay policy
  └─ redaction policy
```

## 4. Capability broker proposal

Example typed capabilities:

```text
phone.identity.normalize
phone.identity.validate-format
telecom.number.search
telecom.number.allocate
telecom.number.release
sms.inbox.read
sms.message.send
sms.activation.status.read
sms.activation.cancel
esim.profile.list
esim.profile.download
esim.profile.enable
esim.profile.disable
esim.profile.delete
esim.qr.generate
esim.qr.decode
lpa.device.enumerate
lpa.device.capabilities
lpa.profile.readback
observability.telecom.health
observability.telecom.audit
```

High-risk capabilities (`send`, `allocate`, `download`, `enable`, `disable`, `delete`, OTP access) require explicit policy evaluation, resource ownership, scope, expiry, rate limits and authoritative postcondition verification.

## 5. State machines

### Number activation

```text
DISCOVERED → RESERVED → ALLOCATED → WAITING_FOR_MESSAGE → CODE_AVAILABLE
      ↘                                  ↘
       EXPIRED                            CANCELLED
CODE_AVAILABLE → VERIFIED → COMPLETED
```

### eSIM profile

```text
DISCOVERED → ELIGIBLE → DOWNLOAD_PENDING → DOWNLOADED
                                      ↓
                                   ENABLED
                                      ↓
                           DISABLED ↔ ENABLED
                                      ↓
                                   DELETED
```

Every transition must have:

- actor/subject identity;
- capability token;
- policy decision;
- resource version;
- timestamp/deadline;
- provider/device response;
- authoritative readback;
- audit record.

## 6. OTP and secret handling

OTP/SMS verification content is a secret, not ordinary conversational context.

Mandatory controls:

- never place OTPs in long-lived agent memory;
- never log raw OTP values;
- redact secrets from traces and error messages;
- use short-lived encrypted storage when persistence is unavoidable;
- bind codes to activation/session/resource IDs;
- enforce expiry and replay prevention;
- prevent cross-session retrieval;
- prevent model-generated text from synthesizing authorization.

## 7. eSIM/LPA security boundary

The LPA layer should be treated as a privileged device capability, not a normal HTTP tool.

```text
MODEL / AGENT
    ↓
INTENT + POLICY
    ↓
CAPABILITY BROKER
    ↓
SIGNED / TYPED LPA OPERATION GRAPH
    ↓
MOBILE NATIVE BRIDGE
    ↓
DEVICE / eUICC / READER
    ↓
AUTHORITATIVE READBACK
```

The model cannot decide that a profile is successfully installed. Only trusted device/provider state can establish that postcondition.

## 8. QR security

A QR code is an activation artifact, not authorization by itself.

Treat every QR payload as untrusted until:

1. syntax and encoding are validated;
2. issuer/provider provenance is known;
3. policy permits the target operation;
4. audience/device binding is checked when applicable;
5. replay/expiry conditions are satisfied;
6. the actual installation result is independently read back.

## 9. Provider abstraction

All external telecom systems should implement a common adapter contract while preserving provider-specific capabilities:

```text
capabilities()
health()
list_regions()
list_services()
quote()
allocate_number()
read_activation_status()
release_number()
read_inbox()
apply_rate_limit()
```

Provider adapters must not smuggle policy decisions into implementation code. The control plane owns authorization; adapters own translation and transport.

## 10. Concurrency and reliability

Use bounded concurrency even when runtime primitives make thousands of tasks cheap. Apply:

- per-provider concurrency ceilings;
- per-user/session budgets;
- deadline propagation;
- cancellation;
- exponential backoff with jitter;
- circuit breakers;
- idempotency keys;
- queue-based retries;
- durable workflow checkpoints.

The Virtuoso evidence is a concrete reminder that unconstrained parallel network I/O can hit operating-system limits; the correct response is bounded fan-out, not merely more threads.

## 11. Monitoring and observability

Borrow the infrastructure-agent pattern from the IBM Terraform module but strengthen it:

```text
Provisioning
  ↓
Telemetry bootstrap
  ↓
Health / metrics / logs / audit
  ↓
Independent observer
  ↓
Control-plane decision
```

Certificate validation must never be disabled as a convenience. Monitoring must be independently useful even when model reasoning traces are unavailable or low quality.

## 12. Monitorability-aware rule

For sensitive telecom/eSIM operations:

```text
CoT available + strong monitorability
    → normal verification tier

CoT weak / empty / unreliable
    → stronger action/state verification
    → tighter capability scope
    → deeper audit
    → higher human-review threshold
```

An empty reasoning trace is not evidence of safety.

## 13. Abuse and threat model

The repositories expose recurring abuse surfaces:

| Surface | Defensive treatment |
|---|---|
| Disposable/public numbers | reputation scoring, ownership checks, provenance, abuse throttles |
| Shared SMS inboxes | tenant isolation, minimum retention, privacy warnings |
| OTP retrieval | secret boundary, replay prevention, no model-memory persistence |
| Automated registration | prohibit bypass; only authorized first-party workflows |
| TOR/filter evasion | detect as bypass signal; do not provide operational evasion path |
| QR activation | provenance, expiry, audience binding, readback |
| eUICC mutations | privileged capability, human approval for destructive operations |
| Scraped message content | untrusted external evidence, sanitation and isolation |
| Provider credentials | secret manager/short-lived credentials, no conversational disclosure |
| Browser automation | sandbox, domain allowlist, explicit authorization |

## 14. Integration with existing portfolio

Primary lineage:

- **Project 31** — Agent OS + Skills + MCP + security.
- **Project 37** — provider-neutral local/edge/cloud runtime.
- **Project 39** — cloud execution fabric and capability substrate separation.
- **Project 41** — repository/world/evidence graphs and typed actions.
- **Project 52** — procedural simulation and safety gates.
- **Project 54** — epistemic/contradiction-aware control.
- **Project 57** — multimodal intelligence + physical/cognitive interface.
- **Project 58** — monitorability-aware oversight.

New synthesis:

`Telephony/eSIM Capability Plane = provider-neutral identity resources + mobile LPA adapters + MCP capability exposure + authoritative lifecycle state + OTP secrecy + monitorability-aware verification`.

## 15. Engineering status

This document is a **source-derived synthesis**, not a claim that every listed repository was exhaustively audited line-by-line. High-value implementation details should be re-verified against source before production adoption. Legacy repositories are lineage references; contemporary architecture should follow the portfolio's existing zero-trust, typed-capability, resumable-workflow and independent-verification doctrine.
