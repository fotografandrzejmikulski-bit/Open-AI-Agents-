# P116 — Mobile Visual Production Extension

## Iteration 37

The new Android visual-editing corpus strengthens P116's mobile UX and operation model without changing its domain boundary.

## New capabilities to target

- smart object/people detection;
- brush-driven and automatic masks;
- tracked removal for video workflows;
- background removal/replacement;
- blemish/skin cleanup;
- cutout → paste → clone operations;
- AI enhancement / expansion;
- deterministic before/after comparison;
- reversible edit graph;
- EXIF/provenance preservation policy;
- confidence and quality-gate reporting.

These are feature-pattern inputs from the supplied corpus plus current public product documentation, not claims about the internal implementation of the uploaded APKs.

## Revised operation graph

```text
CAPTURE / IMPORT
      ↓
SUBJECT + OBJECT ANALYSIS
      ↓
MASK / TRACK / IDENTITY LOCK
      ↓
EDIT GRAPH
      ↓
GENERATE / FILL / REMOVE / ENHANCE
      ↓
QUALITY + PROVENANCE GATE
      ↓
EXPORT / SHARE / VERSION
```

## Integration boundary

P117 owns Android device/app interaction. P116 owns image semantics, identity preservation, retouch planning, generative operations and quality verification.

## Security

No watermark-removal or object-removal feature is treated as permission to process third-party content without authorization. User-controlled media remains data, not executable instruction. Provider calls remain server-side and require readback.
