# P117 Extension — GitHub Release Assurance

## Parent project

**P117 — NeXus Mobile Multimodal Agent Runtime MAX**

## Purpose

Extend the mobile capability boundary with a verifiable software-supply-chain and release-assurance layer derived from the complete GitHub corpus audit.

## Canonical lifecycle

```text
ANDROID SOURCE
    ↓
DEV-CONTAINER / REPRODUCIBLE ENVIRONMENT
    ↓
UNIT / INTEGRATION / DEVICE TESTS
    ↓
CODEQL / SAST
    ↓
DEPENDENCY / PACKAGE POLICY
    ↓
APK / AAB BUILD
    ↓
DIGEST + ATTESTATION
    ↓
PROVENANCE
    ↓
DEPLOYMENT RECORD
    ↓
DEVICE INSTALL / EXECUTION
    ↓
AUTHORITATIVE READBACK
    ↓
PROMOTION / ROLLBACK
```

## Security requirements

- APK/AAB outputs are identified by immutable digest.
- Build environment and source commit are recorded with the artifact.
- CodeQL/SAST results are attached to the release evidence chain where supported.
- Package inspection remains read-only for untrusted APK/XAPK/BAPK inputs.
- Deployment success is not inferred from build success.
- Runtime/device state is independently read back after deployment.
- Secrets are held outside source and generated artifacts.
- Mobile CI/CD integrations are treated as capabilities requiring explicit authorization and evidence.
- Marketplace mobile Actions are reference integrations, not automatically trusted execution paths.

## Mobile marketplace finding

The supplied mobile Actions marketplace URL shows a real ecosystem of mobile CI/CD integrations. P117 should therefore model mobile build/deploy integrations as typed capabilities with version, permission, provenance and runtime verification metadata.

## CodeQL applicability

P117's Kotlin/Java source is within CodeQL's documented supported-language scope. CodeQL execution remains a future repository verification step; this extension does not claim that scans have already run.

## Artifact provenance

GitHub Artifact Metadata provides a useful external model for associating an artifact digest with storage and deployment context. P117 should preserve the chain:

`source → build → digest → provenance/attestation → deployment record → device readback`.

## Status

**ARCHITECTURE ENHANCED — IMPLEMENTATION NOT YET VERIFIED**
