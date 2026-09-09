# Case-Record Evidence, Chronology & Claim Separation — 2026-09-09

## Status
`SOURCE_DERIVED → EVIDENCE-METHODOLOGY → PROPOSED`

Two supplied one-page case notes contain allegations concerning police interventions, threats, a property dispute, court proceedings, protective orders, witness accounts and alleged inconsistencies between records. This module does **not** publish the identities, allegations or conclusions as facts. It extracts only the evidence-handling methodology.

## 1. Atomic chronology

The source material is strongly date- and reference-driven. A defensible system should transform narrative notes into atomic events:

```yaml
CaseEvent:
  date:
  case_reference:
  actor:
  action:
  claimed_fact:
  source_document:
  direct_observation: true|false
  third_party_report: true|false
  official_record: true|false
  allegation: true|false
  corroboration:
  contradiction:
  status: observed|documented|reported|alleged|disputed
```

## 2. Separate procedural fact from interpretation

Statements such as “a hearing occurred”, “a document contains a given statement”, or “a restriction was recorded on a given date” can be checked against primary records. Statements about motive, conspiracy, deliberate deception or influence require separate evidence and must not be inferred merely from chronology.

## 3. Contradiction matrix

Where a source describes materially different versions of an event, preserve each version:

```text
CLAIM A
  ↕ source / date / provenance
CLAIM B
  ↕ source / date / provenance
       ↓
CONFLICT RECORD
       ↓
PRIMARY-DOCUMENT CHECK
       ↓
STATUS: unresolved | reconciled | disproven | supported
```

Do not resolve conflicts by selecting the narrative that sounds most plausible.

## 4. Evidence references

Case numbers, document identifiers, police notes, court records and recordings should be stored as references to source artifacts. The existence of a reference proves only that a reference exists; its contents and legal significance require inspection of the underlying document.

## 5. Privacy and publication boundary

The supplied material contains sensitive personal and legal allegations. It is not reproduced into the public knowledge base. Only generalized evidence-engineering principles are retained.

## 6. Integration

This addendum strengthens Project 32 and the existing OSINT evidence architecture with a dedicated case-record transformation pattern. It does not establish the truth or falsity of any allegation in the supplied documents.
