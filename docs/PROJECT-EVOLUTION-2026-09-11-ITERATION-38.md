# Project Evolution — Iteration 38

## Trigger
New Android package-analysis artifacts supplied after Iteration 37, including `manifest.json` and individual split APK files.

## Evidence processed
The directly readable `manifest.json` identifies Touch Retouch 4.23 (`com.touch.retouch.removeobject.photo`) as an XAPK v2 bundle with a base APK and 20 declared split configurations spanning locale/resource, ARM64 ABI and XXXHDPI density variants. It also records SDK levels, package versioning, declared permissions and bundle size. fileciteturn70file0L1-L1

The individual APK artifacts remain untrusted binary inputs. Their internal DEX/resource/native implementation is not asserted without direct decoding.

## Knowledge evolution
Created:

- `docs/knowledge-base/2026-09-11-android-split-package-anatomy-touch-retouch.md`

New canonical concept: **Android Split Package Graph**.

The repository knowledge model now distinguishes:

- base application artifact;
- locale/resource splits;
- ABI splits;
- density/device splits;
- package metadata and permissions;
- runtime behavior, which requires separate evidence.

## Project evolution

### P117 — NeXus Mobile Multimodal Agent Runtime MAX

Upgraded from generic APK/XAPK/BAPK inspection to an explicit split-graph reconstruction requirement.

New requirements:

- deterministic base/split classification;
- locale/resource/ABI/density topology;
- package graph ledger;
- permission declarations separated from runtime observations;
- static inspection remains read-only and non-executing;
- hash/signature evidence remains a separate verification stage.

### P116 — WDA Photo Agent MAX

No unsupported implementation claims were added from the manifest. The package evidence strengthens the future mobile integration boundary, but does not prove proprietary retouch internals.

### P100 — NeXus AI Code

No direct code change required in this micro-iteration. P100 remains the orchestration/control plane and consumes P117 package intelligence through the capability broker.

## Security doctrine

- Uploaded packages are untrusted.
- Package inspection must not execute application code.
- Filenames are not treated as proof of functionality.
- Manifest permissions are metadata, not proof of runtime behavior.
- No license bypass, credential extraction or authentication bypass is introduced.

## Verification state

### Observed
- manifest package identity;
- XAPK v2 classification;
- base APK declaration;
- 20 split configurations;
- locale/resource split identifiers;
- ARM64 ABI split;
- XXXHDPI density split;
- declared permissions;
- SDK/version metadata.

### Pending
- DEX/native/resource inventory of individual binary splits;
- signature/hash extraction;
- component graph extraction;
- runtime behavior verification;
- Android device E2E.

## Root README

Still pending full historical-content reconstruction before safe synchronization.
