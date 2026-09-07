# Projekty — Expanded Design Lab

This directory contains project artifacts upgraded using the project's accumulated knowledge base: OpenAI Agents SDK, MCP, coding-agent patterns, AI application builders, formal verification concepts, safety/alignment research, distributed execution, and the source materials supplied by the project owner.

## Engineering standard

Every project should aim for production-grade architecture rather than prompt-only prototypes. The default target is:

- explicit product and system boundaries;
- deterministic contracts and typed schemas;
- agent/tool/MCP separation;
- durable state and resumability;
- authentication and authorization at the capability boundary;
- sandboxed execution for untrusted work;
- human approval for consequential side effects;
- observability, evaluation and auditability;
- reproducible builds and versioned artifacts;
- graceful degradation and recovery;
- an escape hatch from visual builders to inspectable source or explicit runtime contracts.

## Project lifecycle

`research → architecture → prototype → verification → hardening → evaluation → deployment`

Projects in this folder are treated as living specifications. Improvements should preserve source-derived intent while separating evidence, hypothesis, implementation detail and future research.

## Source discipline

The attached source documents contribute ideas and requirements, but claims about hardware, scientific performance, or future capabilities must not be presented as experimentally established unless independently verified. Conceptual components remain labeled as conceptual until implemented and tested.
