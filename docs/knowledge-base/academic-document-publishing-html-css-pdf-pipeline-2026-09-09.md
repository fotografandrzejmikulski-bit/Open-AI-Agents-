# Academic Document Publishing: HTML/CSS → PDF Pipeline — 2026-09-09

## Status
`SOURCE_DERIVED → ENGINEERING_SYNTHESIS → PROPOSED`

This module extracts reusable publication-engineering patterns from the supplied USENIX example paper. It is a technical publishing reference, not a claim that the historical template is the current USENIX submission specification.

## 1. Source architecture

The example demonstrates an HTML document styled with CSS and supplemented by JavaScript for reference handling. The document uses semantic HTML elements such as `section`, `header`, `figure`, `figcaption` and `cite`. fileciteturn103file0L51-L60

## 2. Layout capabilities

The source CSS demonstrates publication-oriented capabilities including:

- multi-column layout;
- footnotes;
- page and column floats;
- multi-level counters.

The example also notes that some proceedings-level elements, such as page numbers and running headers, may be inserted by the publication pipeline rather than authors. fileciteturn103file1L108-L121

## 3. Reference processing

JavaScript in the example handles citations by leaving markers at their source locations and moving reference material to the end of the document. fileciteturn103file0L75-L79

## 4. PDF generation

The example uses Prince as a dedicated HTML/XML-to-PDF formatter because ordinary browsers do not implement all page-formatting features required by scholarly layouts, particularly footnotes and page floats. The example invokes Prince with JavaScript enabled. fileciteturn103file0L80-L94

## 5. Reusable artifact pipeline

```text
STRUCTURED CONTENT
      ↓
SEMANTIC HTML
      ↓
CSS PUBLICATION LAYOUT
      ↓
REFERENCE / CITATION PROCESSING
      ↓
PAGED-MEDIA FORMATTER
      ↓
PDF
      ↓
VISUAL QA + TEXT QA
      ↓
RELEASE ARTIFACT
```

The source also emphasizes that publication quality requires attention to typography and style, not only content. fileciteturn103file5L280-L300

## 6. Integration with the portfolio

Primary mappings:

- **Project 60** — Systems Engineering and Intelligence Foundry;
- **Project 28** — Verified Code Generation / artifact pipeline;
- **Project 44** — AI Content Product Studio;
- professional-artifact generation capabilities already represented in the repository knowledge base.

No new numbered project is required. The contribution is a concrete publishing/rendering pattern that can become one adapter in the existing artifact-generation layer.

## 7. Verification requirements

Any production implementation should independently verify:

- page breaks and float placement;
- footnote integrity;
- citation/reference consistency;
- table overflow;
- font availability and embedding;
- accessibility/text extraction;
- deterministic rendering across formatter versions.

The supplied document is an example template and should not be treated as the authoritative current USENIX authoring standard without checking current official instructions.
