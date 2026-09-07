# 37 — CogniSync Professional — Hackathon Submission Project Record

## Purpose

This record preserves the independent project specification for CogniSync Professional after separation from the dedicated hackathon submission repository.

## Product thesis

A background-first professional agent should perform repetitive information work continuously, preserve evidence, evaluate consequence, and interrupt the human only when a decision has material value.

`observe → interpret → prepare → evaluate consequence → act or wait → surface → audit`

## Core architecture

```text
Signals
  ↓
MCP / Integration Adapters
  ↓
Supervisor / Strands
  ├── session context
  ├── durable memory
  ├── evidence / provenance
  ├── bounded specialist workers
  └── consequence policy
          ↓
      verification
          ↓
   human decision gate
      ↙       ↘
 safe work   authorized effect
      ↘       ↙
        audit
```

## Engineering invariants

- Capability is not authorization.
- Unknown operations fail closed.
- Important conclusions retain provenance.
- External completion is only reported after connector confirmation.
- Secrets remain at integration boundaries.
- Local demo behavior must be reproducible without cloud credentials.

## Prototype scope

The hackathon repository implements a deterministic local core, action-policy gate, audit trail, background heartbeat, tests, CLI and a Strands/Bedrock integration surface.

## Production path

1. AgentCore Runtime
2. AgentCore Memory
3. AgentCore Gateway / MCP
4. bounded A2A workers
5. continuous evaluation and telemetry

## Evaluation

Measure useful work, human interventions, evidence coverage, escalation precision, unauthorized effects, recovery success, latency and cost per completed workflow.

## Source relationship

This project record is intentionally separate from the hackathon grant application. It belongs to the general project portfolio and can evolve independently of the competition submission.
