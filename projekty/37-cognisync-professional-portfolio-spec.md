# Project 37 — CogniSync Professional

## Status
Reference implementation / hackathon-derived project record.

## Mission

Build a background-first professional agent that absorbs repetitive coordination work, preserves evidence, evaluates consequences and interrupts the human only when judgment has material value.

## Product loop

`observe → interpret → synthesize → prepare → evaluate consequence → act/wait → audit → learn`

## MVP

- daily project brief;
- blocker detection;
- follow-up drafting;
- decision packets;
- evidence/provenance;
- consequence-aware policy;
- human decision gate;
- audit trail.

## V1

- production MCP connectors;
- durable memory;
- notification channel;
- trace correlation;
- connector-confirmed completion semantics.

## V2

- bounded A2A specialists;
- adaptive model routing;
- evaluation-driven routing and escalation.

## V3

- vertical workflow packs for creative professionals, consultants and small teams.

## Engineering invariants

1. Capability is never authorization.
2. Unknown side effects fail closed.
3. Important conclusions retain provenance.
4. Consequential actions require explicit authorization.
5. External completion is reported only after connector confirmation.
6. Secrets stay outside model context.
7. Evaluation measures both usefulness and restraint.

## Relationship to the hackathon repository

The dedicated hackathon repository contains the competition submission and its executable prototype. This file is the long-lived portfolio record in the main Open-AI-Agents repository; it is not the grant application itself.
