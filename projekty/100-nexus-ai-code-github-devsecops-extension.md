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
GIT / ISSUES / PROJECTS / ACTIONS / PACKAGES
      ↓
CI + TEST + CODEQL / SAST
      ↓
ARTIFACT DIGEST
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
- artifact digest/provenance records;
- GitHub App short-lived least-privilege authentication;
- release/deployment evidence correlation;
- dependency/supply-chain policy;
- Codespaces/dev-container environment definitions;
- Marketplace-style packaging/discovery metadata.

## CodeQL contract

CodeQL is an evidence-producing security-analysis capability, not a generic security checkbox.

```text
CODE
 ↓
DATABASE
 ↓
QUERY / PACK
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

- context isolation;
- sandboxing;
- restrictive CSP;
- secure HTTPS/WSS content;
- restricted navigation/window creation;
- IPC sender validation;
- minimal preload API surface;
- dependency review;
- no privileged API exposure to arbitrary web content.

## Credential contract

Prefer GitHub App installation credentials or other short-lived, narrowly scoped credentials where available. Credentials are not model context and never become part of generated prompts, repository artifacts or UI state.

## Artifact contract

A release is not promoted solely because CI passed.

Required evidence:

`SOURCE SHA + BUILD ENVIRONMENT + TEST EVIDENCE + SECURITY RESULT + ARTIFACT DIGEST + PROVENANCE + DEPLOYMENT RECORD + RUNTIME READBACK`.

## Status

**ARCHITECTURE ENHANCED — IMPLEMENTATION NOT YET VERIFIED**

The supplied GitHub documentation establishes the design requirements. It does not establish that P100 has already implemented or executed these gates.
