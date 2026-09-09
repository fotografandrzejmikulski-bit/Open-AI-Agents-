# OSINT Agent Automation — Defensive Architecture

## Source boundary

Derived from `Instrukcja Projektu OSINT_AI z Automatyzacją.pdf`. The source combines OSINT collection, network reconnaissance, profiling, autonomous tool calling and social-engineering tactics. Only the defensive architecture and evidence methodology are retained here.

## Source execution pattern

The source describes an autonomous loop in which an LLM emits a structured tool tag, a Python layer parses it, a tool executes, results are injected back into context, and the model produces a final synthesis. This is reusable as a generic tool-calling architecture.

```text
USER INTENT
 → POLICY / AUTHORIZATION
 → MODEL PLAN
 → TOOL REQUEST
 → CAPABILITY BROKER
 → CONTROLLED COLLECTION
 → AUTHORITATIVE RESULT
 → MODEL SYNTHESIS
 → EVIDENCE / AUDIT
```

## Defensive OSINT modules

Potential modules include public-web collection, document/metadata analysis, entity resolution, relationship graphs, DNS/domain context and authorized asset inventory. Network scanning is restricted to assets for which explicit authorization exists.

## Evidence controls

Every finding should retain source, timestamp, collection method, confidence and entity-resolution status. A model inference is never itself evidence. Negative findings are bounded observations rather than proof of nonexistence.

## Security transformation

The source's automatic selection of attack vectors, spear-phishing generation, covert monitoring and manipulation loops are classified as unsafe operational patterns. They are not implemented as repository capabilities. The safe replacement is a policy-gated analyst assistant that can identify defensive exposures, explain uncertainty and require human approval for consequential actions.

## Mapping

Strong integration with Project 32 investigative evidence methodology, OSINT relationship graphs, cognitive-security lineage and Project 72 runtime assurance.

## Evidence class

`SOURCE_DERIVED → PROPOSED`. Tool behavior, authorization state and discovered facts require independent verification.