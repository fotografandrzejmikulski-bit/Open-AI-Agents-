# P30 Extension — Source Admissibility / Citation Discovery Prior

## Parent
P30 — OmniCore Sugra Evidence, OSINT & Control Fabric MAX

## Trigger
AI answer-source infographic showing citation-frequency percentages across multiple domains.

## Finding
The chart is useful as a **source-discovery prior** but cannot be converted into a universal source-quality score. Its stated study population/methodology is not independently established by the image.

## Evidence scoring contract

```text
DISCOVERY FREQUENCY
      +
AUTHORITY
      +
CLAIM RELEVANCE
      +
FRESHNESS
      +
INDEPENDENCE
      +
PRIMARY-SOURCE STATUS
      +
LICENSING
      +
CORROBORATION
      ↓
EVIDENCE ADMISSIBILITY
```

A frequently cited site can be weak evidence for a particular technical/legal claim. A low-frequency primary source can be decisive.

## Retrieval behavior

1. Use frequency as a search/discovery hint only.
2. Resolve the actual source behind the claim.
3. Prefer primary/authoritative evidence where appropriate.
4. Record retrieval time and freshness.
5. Evaluate independence before counting corroboration.
6. Preserve source/license metadata.
7. Separate source evidence from model inference.

## Invariant

`CITATION FREQUENCY ≠ TRUTH SCORE`

## Status
`ARCHITECTURE ENHANCED — SOURCE-DERIVED PRIOR ONLY`
