# 26 — OmniCore Trustworthy Kernel & Agentic Safety Lab MAX

## Status
Architecture-ready defensive research project.

## Objective
Turn the current OmniCore concept into a measurable engineering program for a trustworthy AI-native runtime: deterministic kernel boundaries, typed capabilities, isolated AI execution, verified driver synthesis, multimodal/prompt-injection defenses, and repeatable adversarial evaluation.

This project is deliberately defensive. The supplied security reports describe jailbreak and indirect-injection mechanisms; this artifact converts those findings into threat models, normalization, detection, containment and evaluation requirements rather than bypass tooling.

## Source synthesis

The feasibility report defines an integrated stack of seL4, WebAssembly/WASI, LLM/RAG and 3DGS, with the principal integration risk being GPU access from the microkernel. Its proposed mature path is a seL4 VMM plus a Linux driver domain with IOMMU/SMMU passthrough; shared memory is recommended for large transfers. fileciteturn234file0L45-L79

The same report proposes a security boundary in which the LLM remains isolated and reaches critical actuators only through a narrowly defined, audited IPC channel. fileciteturn234file0L11-L19

The Omnis/LBOS materials define capabilities as typed references, MLIR-based intent compilation, Proof-Carrying Code, a hybrid memory model, SemanticFS, AI Supervisor, CIRA and AI Foundry. fileciteturn229file13L600-L624 fileciteturn234file1L232-L265 fileciteturn234file2L327-L396

The supplied security studies identify distribution gaps across low-resource languages, encodings, structured representations, multimodal inputs, multi-turn context and indirect prompt injection. They also describe defensive directions such as SafeDecoding, multilingual safety data and safety-aware reasoning. fileciteturn234file2L471-L509 fileciteturn235file1L228-L297 fileciteturn235file1L345-L388

## Core architecture

```text
                         OPERATOR
                            |
                    INTENT / REQUEST
                            |
                 +----------v-----------+
                 |  TRUST CONTROL PLANE  |
                 |-----------------------|
                 | policy + authz        |
                 | provenance            |
                 | risk classification   |
                 | input normalization   |
                 | eval routing          |
                 +----+-------------+----+
                      |             |
                +-----v----+   +----v------+
                | AI / LLM |   | Tools/MCP |
                | isolated |   | capability|
                | domain   |   | gateway   |
                +-----+----+   +----+------+
                      |             |
                      +------+------+ 
                             |
                      VERIFIED PLAN
                             |
                 +-----------v-----------+
                 | DETERMINISTIC EXECUTOR |
                 |-------------------------|
                 | typed capabilities      |
                 | quotas / deadlines      |
                 | sandbox / VM            |
                 | audited IPC             |
                 +-----------+-------------+
                             |
               +-------------+-------------+
               |                           |
        +------v------+             +------v------+
        | seL4 trusted|             | Linux GPU /  |
        | base        |             | accelerator  |
        | / RT domain |             | driver domain|
        +-------------+             +-------------+
                             |
                       TELEMETRY / EVAL
                             |
                       EVIDENCE LEDGER
```

## 1. Kernel trust boundary

### 1.1 Keep AI out of the trusted computing base

The project upgrades the original "learned kernel" concept into a safer split:

- deterministic scheduler guardrails remain in the trusted path;
- AI Supervisor produces *recommendations* rather than unconstrained kernel decisions;
- a policy engine validates CPU, memory, deadline and capability constraints;
- unknown or unsafe predictions fall back to deterministic scheduling;
- no model weights, dynamic prompts or external network content enter the highest-trust kernel domain.

The source prototype currently sketches direct AI-driven scheduling and self-healing. fileciteturn230file15L677-L710 The hardened design therefore makes the AI Supervisor subordinate to explicit invariants and a deterministic fallback.

### 1.2 Capability firewall

Every privileged operation becomes a typed capability with:

```text
CapabilityId
SubjectId
Resource
Operation
Scope
Expiry
RateLimit
Provenance
ApprovalState
```

No natural-language output may directly name an actuator operation as executable authority. The model must request a typed capability, and the gateway decides whether that capability exists and is permitted.

### 1.3 Proof and verification gates

AI-generated kernel modules, drivers and compiler rewrites move through:

```text
GENERATE
  -> PARSE
  -> TYPE / EFFECT CHECK
  -> STATIC ANALYSIS
  -> INVARIANT CHECK
  -> SYMBOLIC / SMT CHECK (where applicable)
  -> BUILD
  -> SANDBOX TEST
  -> HARDWARE-IN-LOOP TEST
  -> SIGN
  -> DEPLOY
```

This extends the supplied CIRA concept, where generated drivers are not accepted until invariants and correctness checks pass. fileciteturn234file1L348-L364

## 2. AI Supervisor MAX

The prototype uses historical CPU load and context to predict scheduling priority. fileciteturn235file3L588-L620 The production architecture adds explicit safety envelopes:

```text
prediction = model(state)
proposal   = clamp(prediction, policy_bounds)
if violates_deadline || violates_budget || low_confidence:
    fallback(deterministic_scheduler)
else:
    execute(proposal)
```

Required properties:

- bounded execution time;
- bounded numerical domain in the kernel;
- no FPU dependency in the highest-trust scheduling path;
- rollback to a known-good scheduler;
- trace of every policy decision and override;
- offline evaluation before a new model can become a scheduler advisor.

The supplied automation material explicitly recommends fixed-point arithmetic for kernel scheduling and avoiding floating-point state in Ring 0. fileciteturn234file3L715-L727

## 3. SemanticFS with security semantics

The supplied design replaces path-centric access with vector retrieval over `VectorEntry` objects and HNSW-like indexing. fileciteturn234file1L271-L301

The MAX version adds a security layer so semantic similarity never becomes authorization:

```text
semantic retrieval != permission
```

Every retrieved object therefore carries:

- owner / tenant;
- confidentiality class;
- integrity state;
- source provenance;
- retention policy;
- allowed consumers;
- injection-risk score;
- content hash.

The retrieval engine may rank an object highly while the authorization engine still denies access.

## 4. Prompt-injection firewall

The supplied Gemini studies show why keyword filters alone are insufficient: the attack surface includes multilingual distribution gaps, encodings, structural representations, visual/OCR channels, multi-turn context and indirect instructions inside external content. fileciteturn234file2L471-L509 fileciteturn234file2L575-L629 fileciteturn235file0L11-L49

Therefore OmniCore uses a **canonicalization + provenance + policy** pipeline:

```text
RAW INPUT
  |
  +--> Unicode normalization
  +--> encoding / representation inspection
  +--> OCR / visual-text extraction
  +--> language identification
  +--> structure parsing
  +--> source classification
  |
  v
UNTRUSTED DATA OBJECT
  |
  +--> instruction-likelihood score
  +--> provenance label
  +--> policy classification
  v
MODEL CONTEXT BUILDER
  |
  +--> DATA CHANNEL
  +--> INSTRUCTION CHANNEL
  +--> TOOL AUTHORIZATION CHANNEL
  |
  v
MODEL
```

The key architectural rule is that retrieved or user-supplied content is data by default, not authority.

## 5. Multimodal security

The materials describe visual contextual attacks and OCR/steganographic prompt injection as important attack vectors against multimodal models. fileciteturn235file0L11-L49

OmniCore therefore applies the same trust treatment to:

- text;
- OCR output;
- image captions;
- metadata;
- audio transcripts;
- video-derived events;
- tool-returned web content;
- RAG documents.

A multimodal perception result can inform a plan, but cannot silently mutate policy or gain new capabilities.

## 6. Agent-chain containment

The supplied analysis of indirect prompt injection describes a chain from poisoned logs or documents through personalization/memory into browsing-based exfiltration. fileciteturn230file13L591-L619

MAX architecture inserts a **Capability Broker** between reasoning and every consequential side effect:

```text
LLM PLAN
   |
   v
CAPABILITY BROKER
   |
   +-- identity check
   +-- scope check
   +-- destination allowlist
   +-- data-flow / taint check
   +-- approval requirement
   +-- rate / quota check
   +-- provenance check
   |
   v
TOOL / MCP CALL
```

For network egress, sensitive data classification and destination policy are evaluated independently. A model cannot create a permitted destination merely by putting it in a document, memory record or tool argument.

## 7. Memory poisoning resistance

Long-lived memory is treated as a privileged state store rather than ordinary context. The source security material describes persistent memory poisoning as a mechanism for making malicious instructions survive across sessions. fileciteturn235file0L76-L94

The architecture therefore separates:

```text
EPHEMERAL CONTEXT
LONG-TERM MEMORY
POLICY STATE
CREDENTIAL STATE
AUDIT LOG
```

Only explicit, typed memory-write operations can modify long-term memory. High-impact memory changes require provenance and policy checks; security-relevant claims require confirmation or independent evidence.

## 8. CIRA / AI Foundry hardening

The original AI Foundry concept generates drivers from hardware IDs and retrieved datasheets. fileciteturn230file0L25-L47 The MAX version changes this from "generate and compile" into **generate, verify, attest and quarantine**:

```text
Hardware discovery
      -> Datasheet retrieval
      -> Source provenance check
      -> Driver draft
      -> Contract extraction
      -> Effect / privilege analysis
      -> Formal invariants
      -> Fuzzing + fault injection
      -> Cross-target build
      -> Signed artifact
      -> Staged rollout
      -> Health monitoring
      -> Automatic rollback
```

No generated driver is allowed to self-deploy into the trusted domain merely because it compiles.

## 9. GPU and 3DGS trust partition

The supplied feasibility study identifies GPU integration as the dominant technical risk and recommends the seL4 + Linux guest/driver-domain architecture with passthrough; it also recommends shared memory for large media transfers. fileciteturn234file0L45-L79

The security architecture consequently treats the GPU domain as **lower trust than the seL4 control domain**:

- 3DGS renderer is isolated;
- shaders are treated as untrusted code/data;
- media buffers cross domains through validated shared-memory contracts;
- rendering failures cannot reset or modify safety-critical control state;
- accelerator access is capability-scoped and auditable.

## 10. Evaluation system

A permanent safety benchmark becomes part of the repository:

| Test family | Examples | Gate |
|---|---|---|
| Representation | Unicode variants, encodings, structured text | no policy bypass |
| Language | low-resource multilingual prompts | safety parity target |
| Multimodal | OCR/visual-context injections | no privileged action |
| Stateful | multi-turn escalation | policy stability |
| RAG/Indirect | poisoned docs, logs, webpages | data/instruction separation |
| Memory | poisoned memory writes | durable-state integrity |
| Tool use | exfiltration and destination abuse | broker denial |
| Agent-to-agent | malicious inter-agent payloads | trust propagation blocked |
| Kernel | generated-driver faults | isolation + rollback |
| GPU | malformed shaders/media | domain containment |

Every test stores:

- attack family;
- normalized input;
- source provenance;
- policy version;
- model version;
- tool manifest;
- decision trace;
- outcome;
- regression status.

## 11. SLOs and release gates

The project should not use vague claims such as "secure" or "autonomous". Release criteria become measurable:

```text
P(policy_violation) <= threshold
P(unauthorized_tool_action) <= threshold
P(memory_poison_acceptance) <= threshold
P(cross-domain fault propagation) <= threshold
P(rollback failure) <= threshold
```

Also measure:

- worst-case decision latency;
- recovery time;
- failed-call containment rate;
- provenance completeness;
- false-positive rate;
- safety performance by language and modality;
- capability-broker denial accuracy;
- scheduler fallback frequency.

Thresholds are versioned benchmark policy, not hard-coded claims.

## 12. Implementation roadmap

### Phase A — Trust kernel

- define capability schema;
- implement deterministic capability broker;
- separate AI advisory state from trusted kernel state;
- add event/audit ledger;
- build fallback scheduler.

### Phase B — Secure semantic substrate

- implement `SemanticObject` with provenance and ACL metadata;
- retrieval/authorization split;
- memory write protocol;
- injection-risk classifier;
- corpus poisoning tests.

### Phase C — Agentic build system

- CIRA contract extraction;
- generated-code quarantine;
- static/effect analysis;
- formal invariant hooks;
- fuzz/HIL validation;
- signed artifact promotion.

### Phase D — Multimodal defense

- canonicalization pipeline;
- OCR/visual instruction tagging;
- multilingual safety suite;
- stateful red-team harness;
- RAG indirect-injection benchmark.

### Phase E — Hardware and 3DGS

- seL4 control domain;
- Linux GPU driver domain;
- IOMMU/SMMU configuration;
- validated shared-memory transport;
- isolated renderer;
- fault-injection and recovery tests.

## 13. Definition of done

The project is complete only when:

1. the AI cannot directly cross a privileged capability boundary;
2. untrusted content is explicitly separated from executable authority;
3. semantic retrieval cannot grant permission;
4. long-term memory changes are typed and auditable;
5. generated drivers cannot self-promote without verification;
6. GPU/3DGS faults cannot cross into the safety-critical domain;
7. every security claim is backed by a versioned evaluation;
8. the entire system has deterministic fallbacks and rollback paths.

## Position in the portfolio

This project becomes the **security-and-trust substrate** for projects 03, 04, 06, 09, 12, 13, 18, 19, 21, 23 and 24. It is the missing bridge between the ambitious OmniCore research vision and an engineering discipline suitable for actual implementation.
