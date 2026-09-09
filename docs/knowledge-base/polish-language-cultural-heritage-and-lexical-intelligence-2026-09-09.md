# Polish Language, Cultural Heritage & Lexical Intelligence — 2026-09-09

## Source set
- `Linde S - Słownik języka polskiego T 1-6.pdf`
- `kultura_jezyka_polskiego_0910_wejark.doc`

## Source-derived observations
The supplied Linde scan is image-based and its visible title page identifies M. Samuel Bogumił Linde's *Słownik języka polskiego*, Tom I, A–F, in the supplied edition. The scan therefore should be treated as a historical lexical source, not as a modern normative dictionary. The course document *Kultura języka polskiego* is explicitly oriented toward language culture, stylistic varieties of contemporary Polish, press style, lexical and phraseological evolution, word formation, inflection, syntax, valuation in proper names, borrowings and language-media development. fileciteturn180file0L2-L6 fileciteturn180file1L13-L22

## Reusable model
```text
HISTORICAL LEXICON
      ↓
ENTRY / FORM / QUOTATION / SOURCE
      ↓
TEMPORAL + STYLISTIC CONTEXT
      ↓
MODERN USAGE / NORMATIVE REFERENCE
      ↓
SEMANTIC COMPARISON
      ↓
PROVENANCE + CONFIDENCE
      ↓
LANGUAGE-AWARE GENERATION / REVIEW
```

## Engineering implications
1. Separate historical attestation from contemporary norm.
2. Preserve spelling and orthographic form as source data; normalize only into a separate field.
3. Model meaning as time-indexed rather than assuming semantic identity across periods.
4. Keep citations/examples attached to lexical entries.
5. Distinguish descriptive usage from prescriptive correctness.
6. Add stylistic registers and media context where supported by the source.
7. Treat borrowed vocabulary as an object of analysis rather than automatically as an error.
8. For AI generation, expose uncertainty when a historical form has no securely established modern equivalent.

## Candidate data schema
```yaml
LexicalRecord:
  lemma:
  historical_forms: []
  normalized_form:
  meaning:
  period:
  register:
  phraseology: []
  examples: []
  source:
  source_page:
  provenance:
  normative_status: unknown
  semantic_relations: []
```

## Portfolio impact
Strengthens language-aware generation, evidence/provenance, content production, narrative systems and research orchestration. The combination is sufficiently concrete to justify a new dedicated language-intelligence project, rather than treating the material as generic language knowledge.

## Epistemic boundary
The supplied Linde scan is not fully OCR-readable through the document text layer; detailed lexical claims must therefore be made only after page-level visual inspection/OCR. The course material is dated 2009–2010 and should not be treated as a current normative authority without contemporary verification. fileciteturn180file1L38-L50
