# Chronos: Człowiek Roku — Unreal Engine 5 Architecture

## Source boundary

Derived from `Instrukcja Tworzenia Gry i Kodu (1).pdf` and the supplied Chronos technical material. The source is an implementation-oriented architecture for adapting the narrative into an interactive real-time system.

## Narrative systems

The source identifies three core technical pillars:

- `TimeRift` — dual-timeline state and seamless temporal switching;
- `CCR_Camera` — investigative/documentary camera system;
- `MemoryParticle` — reconstruction of memory as an interactive visual system.

The report emphasizes that code and gameplay mechanics should function as environmental narrative rather than decorative abstractions.

## World architecture

The recommended model uses a Persistent Level containing player character, TimeRift manager, HUD and global post-processing. Temporal worlds such as `Map_2018` and `Map_2026` are treated as streamed sub-levels. `ULevelStreamingDynamic` is used for seamless switching instead of destructive `OpenLevel` transitions.

## TimeRift implementation pattern

The supplied implementation uses `UTimeRift_Manager`, soft world references and asynchronous loading callbacks/latent actions. `TSoftObjectPtr<UWorld>` avoids forcing both temporal worlds into RAM at startup.

## Rendering stack

The source positions UE5 Lumen for dynamic global illumination/reflections, Nanite for dense scanned geometry and Virtual Shadow Maps for high-resolution shadows. World Partition/streaming is used to manage temporal map state. The source explicitly identifies GPU cost, disk/streaming pressure and synchronization as implementation risks.

## Verification architecture

```text
PLAYER INPUT
 → TIME STATE TRANSITION
 → STREAM / LOAD
 → AUTHORITATIVE WORLD STATE
 → CAMERA / VFX UPDATE
 → NARRATIVE STATE
 → POSTCONDITION CHECK
```

All generated C++ should be treated as untrusted until compile-tested, runtime-tested and profiled in the target UE5 version.

## Mapping

Maps to the repository's game/phygital systems, symbolic interfaces, evidence-driven narrative and runtime verification lineages. No new numbered project is required by this source alone.