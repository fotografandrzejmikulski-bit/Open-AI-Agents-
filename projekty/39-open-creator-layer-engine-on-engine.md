# Project 39 — Open Creator Layer

## Thesis

Create a Buildbox-class creator workflow as an editor extension / abstraction layer over established engines rather than building a new renderer and physics engine.

## Source-derived concept

The supplied Buildbox study proposes an Engine-on-Engine architecture with drag-and-drop authoring, Mind Map navigation, visual scripting, Smart Assets, production automation and modular monetization over Unity/Unreal. fileciteturn66file1L50-L69

## Product model

```text
Natural-language intent
      ↓
Project graph
      ↓
Typed visual nodes
      ↓
Engine adapter
      ↓
Generated native artifacts
      ↓
Validation / compile / test
      ↓
Preview
      ↓
Export
```

## Core modules

- graph-first project navigation;
- typed ports and schema validation;
- Blackboard/global variables;
- event-driven runtime compilation;
- Smart Asset import;
- prefab/template generation;
- build configuration;
- AI-assisted graph authoring;
- escape hatch to native C#/C++/Blueprints.

## Source engineering details

The corpus proposes typed ports, serialized variables and event-driven execution rather than per-frame polling, plus automated asset import and atlas generation. fileciteturn66file11L480-L513

## Success criteria

- first playable prototype from a blank project in minutes;
- graph compiles deterministically;
- no proprietary runtime required beyond the target engine;
- generated artifacts remain editable in native tools;
- asset setup time is materially reduced;
- AI changes are reviewable and reversible.
