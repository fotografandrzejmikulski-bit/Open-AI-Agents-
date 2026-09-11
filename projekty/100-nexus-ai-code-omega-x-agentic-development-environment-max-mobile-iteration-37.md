# P100 Mobile Capability Plane — Iteration 37 Addendum

This addendum extends P100 without duplicating P117.

## New boundary

P100 remains the general NeXus AI developer/control plane. Android capabilities are now routed through a dedicated **Mobile Capability Plane** owned by P117.

## P100 changes

- OCN agents and swarms may request mobile capabilities only through the capability broker.
- Mobile screen, UI-tree, camera, microphone, app-state and contextual observations are provenance-bearing inputs.
- Touch/gesture/app-launch actions require authorization and authoritative readback.
- APK/XAPK/BAPK inspection is exposed as a read-only analysis capability, never as an execution path.
- Mobile context can enter selective-context retrieval and bitemporal memory with freshness metadata.
- DGM-generated mobile automation candidates execute only inside sandboxed test-device boundaries.
- Mobile telemetry is treated as observed system state rather than inferred UI state.

## Canonical flow

`INTENT → MOBILE PLAN → CAPABILITY AUTHORIZATION → SANDBOXED ACTION → READBACK → VERIFY → ARTIFACT LEDGER`

## Relationship to P117

P117 owns device/app execution and package intelligence. P100 owns orchestration, models, OCN, MCP, DGM-H and operator UX.

## Evidence

This is an architecture synthesis from the NeXus source corpus and the uploaded Android binary intake. Exact internals of the uploaded binaries were not observed in this iteration.
