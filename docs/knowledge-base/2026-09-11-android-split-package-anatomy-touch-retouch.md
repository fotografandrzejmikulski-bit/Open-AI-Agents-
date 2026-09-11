# Android Split-Package Anatomy — Touch Retouch 4.23

## Evidence class

**OBSERVED / DIRECTLY PARSED SOURCE** from the user-supplied `manifest.json`.

No claim is made here about proprietary implementation internals that were not decoded.

## Observed package identity

- package: `com.touch.retouch.removeobject.photo`
- application name: `Touch Retouch`
- version code: `58`
- version name: `4.23`
- XAPK version: `2`
- min SDK: `22`
- target SDK: `30`
- declared total bundle size: `6,511,836` bytes
- icon: `icon.png`

## Observed permissions

The supplied manifest declares:

- `android.permission.CAMERA`
- `android.permission.WRITE_EXTERNAL_STORAGE`
- `android.permission.READ_EXTERNAL_STORAGE`
- `android.permission.INTERNET`
- `android.permission.ACCESS_NETWORK_STATE`
- `android.permission.WAKE_LOCK`
- `android.permission.RECEIVE_BOOT_COMPLETED`

These are package declarations only; they do not prove that every permission is actively exercised in every runtime path.

## Observed split topology

The manifest identifies a distinct base APK and 20 declared split configurations.

```text
Touch Retouch XAPK v2
│
├── BASE
│   └── com.touch.retouch.removeobject.photo.apk
│
├── LOCALE / RESOURCE SPLITS
│   ├── ru
│   ├── my
│   ├── zh
│   ├── hi
│   ├── in
│   ├── ar
│   ├── fr
│   ├── es
│   ├── ja
│   ├── vi
│   ├── ko
│   ├── it
│   ├── de
│   ├── th
│   ├── tr
│   ├── pt
│   └── en
│
├── ABI SPLIT
│   └── arm64_v8a
│
└── DENSITY SPLIT
    └── xxxhdpi
```

Source manifest citation: fileciteturn70file0L1-L1

## Architectural deductions allowed by the evidence

1. The application distribution is a **bundle graph**, not a single APK artifact.
2. Locale/resource specialization is separated from the base package.
3. Device-specific delivery includes at least an ARM64 ABI split and an XXXHDPI density split.
4. An APK intelligence system should reconstruct package relationships before analyzing individual artifacts.
5. Package inventory should preserve the distinction between base, locale, ABI and density/configuration nodes.
6. Permission declarations should be retained as package metadata and classified separately from observed runtime behavior.

## P117 implications

P117 now treats split reconstruction as a first-class capability:

```text
INPUT
  ↓
CONTAINER CLASSIFICATION
  ↓
SPLIT GRAPH RECONSTRUCTION
  ↓
BASE / LOCALE / ABI / DENSITY MAP
  ↓
MANIFEST + PERMISSION INVENTORY
  ↓
HASH / SIGNATURE EVIDENCE
  ↓
READ-ONLY PACKAGE LEDGER
```

This is preferable to a naive `APK → unzip → inspect` workflow because the unit of analysis for modern Android distribution can be a coordinated set of artifacts.

## What remains unknown

The supplied manifest does **not** establish:

- classes or DEX implementation;
- native `.so` libraries;
- actual runtime network endpoints;
- cryptographic signing identity;
- internal ML models;
- proprietary object-removal algorithms;
- actual UI implementation;
- runtime behavior of the declared permissions.

Those items require separate, authorized static analysis of the relevant binary artifacts and must not be inferred from filenames alone.
