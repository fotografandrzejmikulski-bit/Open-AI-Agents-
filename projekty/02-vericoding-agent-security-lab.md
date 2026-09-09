# 02 — VERICODING AGENT SECURITY LAB

## Status
**Engineering Specification Baseline**

## Mission
A defensive engineering laboratory and assurance pipeline for AI-generated software and agent runtimes. The system converts security, architecture and verification policies into deterministic gates before code, tools or deployments receive privileged authority.

## Security model
Generated artifacts and model outputs are **untrusted candidates**. Authority is granted only after deterministic analysis, policy evaluation, testing and—where configured—formal proof or explicit human approval.

```text
Intent
  ↓
Typed ChangeSpec
  ↓
Parse / Normalize
  ↓
Static Architecture + Taint + Effect Analysis
  ↓
Security Policy Evaluation
  ↓
Adversarial Regression
  ↓
Proof / Contract Gate
  ↓
Approval Gate (risk dependent)
  ↓
Sandbox Execution
  ↓
Evidence Bundle
  ↓
Promotion
```

## Trust boundaries

1. **Model boundary** — generated text/code is untrusted.
2. **Repository boundary** — repository content may contain hostile instructions or malformed data.
3. **Tool boundary** — every tool is a separately authorized capability.
4. **Execution boundary** — generated code runs in an isolated environment.
5. **Promotion boundary** — production deployment requires an independently evaluated verdict.
6. **Evidence boundary** — reports refer only to artifacts actually observed by the pipeline.

## Canonical entities

```ts
type Risk = 'LOW' | 'MEDIUM' | 'HIGH' | 'CRITICAL';
type Verdict = 'ALLOW' | 'DENY' | 'REVIEW';
type Effect =
  | 'PURE'
  | 'IO_FILE'
  | 'IO_DB'
  | 'IO_NETWORK'
  | 'CREDENTIAL'
  | 'DEPLOYMENT';

type ChangeSpec = {
  changeId: string;
  repository: string;
  baseRevision: string;
  candidateRevision: string;
  requestedCapabilities: string[];
  affectedModules: string[];
  environment: 'sandbox' | 'preview' | 'staging' | 'production';
  risk: Risk;
};
```

## Policy engine

Policies must be explicit, versioned and deterministic where possible.

### Architecture rules

- dependency direction is machine-checkable;
- forbidden imports fail the gate;
- side effects require declared effect scopes;
- module and service boundaries are represented in an inspectable graph;
- complexity budgets can reject changes exceeding configured limits;
- public interfaces require schema compatibility checks.

### Taint rules

At minimum track:

- untrusted user text;
- repository content;
- model output;
- tool output;
- credentials/secrets;
- SQL fragments;
- shell/process arguments;
- HTML/markup.

Taint propagation must be conservative; sanitizers and validators are explicit policy operations rather than string-name conventions.

## Agent security gateway

Every capability has a manifest:

```json
{
  "tool": "example.write_file",
  "risk": "HIGH",
  "effects": ["IO_FILE"],
  "network": false,
  "requires_human_approval": true,
  "allowed_environments": ["sandbox", "preview"]
}
```

Authorization evaluates actor, session, requested capability, target environment, policy version and current risk state. A model may request a capability but cannot grant one to itself.

## Stateful security evaluation

Security decisions consider relevant history:

```text
conversation state
+ tool-call history
+ current request
+ resource sensitivity
+ policy state
+ prior risk signals
→ current verdict
```

The system therefore tests multi-step attack chains rather than only isolated prompts. Detection logic should remain explainable through reason codes and trace references.

## Adversarial laboratory

The laboratory contains controlled fixtures for:

- prompt injection;
- indirect prompt injection from repository/web content;
- multi-turn escalation;
- tool misuse;
- privilege boundary confusion;
- data exfiltration attempts;
- malicious file/project content;
- adversarial-input robustness;
- unsafe serialization/deserialization paths;
- authorization bypass regression.

Research-only adversarial methods are represented as non-operational fixtures and evaluation parameters. No test fixture may require compromising an external system.

## Formal verification boundary

For selected high-impact operations, generate proof obligations from policy contracts. A proof result is represented separately from a generic test pass:

```text
PROOF_NOT_REQUIRED
PROOF_PENDING
PROOF_VERIFIED
PROOF_FAILED
```

Failure to establish a required proof cannot be converted into `ALLOW` through a model-generated explanation.

## Sandbox contract

The execution environment must provide:

- ephemeral filesystem;
- isolated process/container boundary;
- restricted network egress;
- synthetic credentials/canaries;
- resource and wall-clock quotas;
- deterministic run metadata;
- complete stdout/stderr capture;
- artifact hash recording;
- cancellation and cleanup guarantees.

Production credentials are prohibited in adversarial and generated-code test environments.

## API contracts

### `analyze_project`
Returns normalized architecture graph, policy findings, effects, taint propagation, proof obligations and evidence references.

### `evaluate_change`
Returns a deterministic verdict, reason codes, impacted resources, required approvals, policy version and proof state.

### `run_adversarial_suite`
Returns immutable test-run metadata, per-case verdicts, trace references and regression deltas.

### `authorize_execution`
Returns `ALLOW | DENY | REVIEW` with policy reason codes. It does not execute the requested capability.

## Evidence bundle

Every consequential verdict should be reconstructable from:

```text
changeId
policyVersion
inputArtifactHashes
scannerVersion
suiteVersion
testRunIds
proofReferences
authorizationDecision
operator/actor
createdAt
```

No success claim is valid without a corresponding evidence reference.

## Test strategy

### Unit
Policy predicates, taint propagation, capability matching, effect analysis, schema validation and reason-code generation.

### Property-based
- authorization is deny-by-default for unknown capabilities;
- tainted values never bypass required sanitizer contracts;
- policy evaluation is deterministic for identical inputs;
- unsupported environment/capability combinations never become allowed.

### Integration
Repository scan → policy engine → adversarial suite → evidence bundle.

### Regression
Every vulnerability or bypass discovered in the lab becomes a reproducible fixture with severity and expected verdict.

### E2E
Generated change → analysis → denied/approved gate → isolated execution → evidence capture.

## Observability

Track:

- verdict distribution;
- policy violations by rule;
- false-positive/false-negative review outcomes;
- adversarial suite failure rate;
- authorization latency;
- sandbox failure/cleanup rate;
- proof verification latency;
- bypass attempts and blocked capability requests.

Tracing must correlate repository revision, change ID, test suite version and execution trace.

## Deployment model

```text
local → CI → preview → staging → production
```

The same policy contracts apply across environments, with increasingly restrictive capability policies toward production. Policy changes are versioned and auditable.

## Failure handling

`detect → classify → localize → reproduce → explain → block/fix → regression test → re-evaluate`.

A scanner or verifier failure is itself a security-relevant state; the pipeline must not silently downgrade `UNKNOWN` to `ALLOW`.

## Definition of Done

The project is **Implementation Ready** when policy schemas, AST/IR normalization, capability manifests, taint/effect rules, adversarial fixtures, sandbox contract, evidence model and executable test specifications are implemented. Production readiness additionally requires validated CI integration, measured false-positive/false-negative behavior, operational runbooks and security review evidence.

## Non-goals

This project is not an offensive exploitation framework and is not a replacement for repository-native secure coding practices. Its purpose is to make generated and agentic changes verifiable before privileged execution.
