# P117 Extension — GitHub Release Assurance

## Parent project

**P117 — NeXus Mobile Multimodal Agent Runtime MAX**

## Purpose

Extend the mobile capability boundary with a verifiable software-supply-chain and release-assurance layer derived from the GitHub corpus.

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
APK / AAB BUILD
    ↓
DIGEST
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

## CodeQL applicability

P117's Kotlin/Java source is within CodeQL's documented supported-language scope. CodeQL execution remains a future repository verification step; this extension does not claim that scans have already run.

## Status

**ARCHITECTURE ENHANCED — IMPLEMENTATION NOT YET VERIFIED**
