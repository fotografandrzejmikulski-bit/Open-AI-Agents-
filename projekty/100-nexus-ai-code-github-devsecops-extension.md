# P100 Extension — GitHub DevSecOps / Supply-Chain Control Plane

## Parent project

**P100 — NeXus AI Code OMEGA-X Agentic Development Environment MAX**

This extension records the GitHub corpus integration without creating a second product identity.

## New control-plane layer

```text
NE XUS OPERATOR
      ↓
PROJECT / REPOSITORY CONTEXT
      ↓
GIT / ISSUES / PROJECTS / ACTIONS / PACKAGES / MCP
      ↓
AGENTIC WORKFLOW / FIREWALL / GATEWAY CAPABILITIES
      ↓
CI + TEST + CODEQL / SAST + DEPENDENCY POLICY
      ↓
ARTIFACT DIGEST / ATTESTATION
      ↓
PROVENANCE / DEPLOYMENT RECORD
      ↓
RUNTIME READBACK
      ↓
AUDIT / PROMOTION / ROLLBACK
```

## Required capabilities

- repository and branch context;
- GitHub Projects/Issues/PR lifecycle integration;
- GitHub Actions workflow evidence;
- Packages/artifact identity;
- CodeQL configuration and result ingestion;
- artifact digest/provenance/attestation records;
- GitHub App short-lived least-privilege authentication;
- release/deployment evidence correlation;
- dependency/supply-chain policy;
- Codespaces/dev-container environment definitions;
- Marketplace-style packaging/discovery metadata;
- optional agentic-workflow firewall/gateway adapters;
- MCP Registry / official GitHub MCP Server compatibility without granting implicit authority;
- typed roadmap states and feedback/triage signals.

## Complete-audit findings

The supplied GitHub organization surface currently exposes repositories and services relevant to the P100 mission, including GitHub Agentic Workflows (`gh-aw`), shared agentic workflow actions, an agentic workflow firewall, an MCP gateway, artifact-attestation policy integration, a Copilot Agent SDK, CodeQL, a redacting logger and the official GitHub MCP Server. These are external reference patterns. They are **not** evidence that P100 already implements equivalent components.

The GitHub Copilot App further demonstrates a current agentic developer workflow in which agents operate across repository work. P100 should therefore preserve an explicit distinction between agent planning, GitHub capability invocation, authorization and postcondition verification.

## CodeQL contract

CodeQL is an evidence-producing security-analysis capability, not a generic security checkbox.

```text
CODE
 ↓
DATABASE
 ↓
QUERY / PACK / MODEL
 ↓
FINDING
 ↓
SARIF / ALERT
 ↓
TRIAGE
 ↓
REMEDIATION
 ↓
RE-ANALYSIS
```

For P100 this should cover supported JavaScript/TypeScript, Rust, Java/Kotlin and other relevant source paths where the configured CodeQL extractor supports them.

## Electron hardening contract

P100's Electron shell must treat remote/untrusted content as hostile and maintain:

- current stable Electron runtime policy;
- context isolation;
- sandboxing;
- restrictive CSP;
- secure HTTPS/WSS content;
- restricted navigation/window creation;
- IPC sender validation;
- minimal preload API surface;
- dependency review;
- no privileged API exposure to arbitrary web content;
- release/package verification through the chosen Electron packaging toolchain.

Electron's current platform documentation also identifies Forge as the batteries-included build/publishing path and Fiddle as an experiment/reproduction path; these are useful references for P100 packaging and reproducibility, not mandatory dependencies.

## npm / supply-chain contract

The npm reference set adds concrete supply-chain controls beyond generic dependency review:

- dependency audit evidence;
- provenance statements;
- OIDC trusted publishing where applicable;
- staged publishing;
- ECDSA registry signature verification where applicable;
- mandatory 2FA policy;
- malware-reporting and incident response path;
- scoped organization/package access;
- granular, least-privilege access tokens.

Prefer trusted publishing for CI/CD package release when supported. Credentials remain outside prompts, source artifacts and UI state.

## Credential contract

Prefer GitHub App installation credentials or other short-lived, narrowly scoped credentials where available. Credentials are not model context and never become part of generated prompts, repository artifacts or UI state.

## Artifact contract

A release is not promoted solely because CI passed.

Required evidence:

`SOURCE SHA + BUILD ENVIRONMENT + TEST EVIDENCE + SECURITY RESULT + DEPENDENCY STATE + ARTIFACT DIGEST + ATTESTATION/PROVENANCE + DEPLOYMENT RECORD + RUNTIME READBACK`.

## Roadmap / feedback contract

GitHub's public roadmap provides typed release phases (`exploring`, `in design`, `preview`, `ga`) and feature-area/deployment labels. P100 may use the same principle for project state without copying GitHub's exact taxonomy.

Community discussions demonstrate an active feedback/incident signal stream. P100 should model feedback as observation requiring triage, not as automatic authority for a code change.

## Status

**ARCHITECTURE ENHANCED — IMPLEMENTATION NOT YET VERIFIED**

The supplied GitHub/Electron/npm documentation establishes design requirements and external reference patterns. It does not establish that P100 has already implemented or executed these gates.
