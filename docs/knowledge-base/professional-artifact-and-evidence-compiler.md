# Professional Artifact & Evidence Compiler

## Source basis

The supplied resume-prompt corpus presents repeatable workflows for creating, tailoring and reviewing resumes and related application materials. It recommends role-specific customization, impact-oriented achievements, relevant keywords, professional summaries and interview preparation. fileciteturn221file2L101-L119 fileciteturn221file4L187-L200

The same source explicitly cautions that generated writing can be generic and that facts produced by the model may be incorrect; it recommends using the material for brainstorming and first drafts rather than treating generated output as the final product without review. fileciteturn221file1L70-L85

## Compiler model

```text
USER FACTS
   ↓
EVIDENCE INVENTORY
   ↓
ROLE / TARGET REQUIREMENTS
   ↓
CLAIM-TO-EVIDENCE MATCHING
   ↓
ARTIFACT PLAN
   ↓
DRAFT GENERATION
   ↓
FACT / METRIC / CONSISTENCY CHECK
   ↓
STYLE + ATS / FORMAT REVIEW
   ↓
HUMAN APPROVAL
   ↓
VERSIONED FINAL ARTIFACT
```

## Hard constraints

- Never invent employment history, credentials, employers, dates, metrics, certifications or achievements.
- Preserve uncertainty instead of converting missing evidence into confident prose.
- Separate user-provided facts from verified external facts.
- Make derived metrics reproducible where the user supplied sufficient inputs.
- Keep target-role requirements separate from claims about the candidate.
- Track revisions and retain the evidence basis for consequential claims.
- Treat optimization for keywords as a formatting/relevance objective, never as permission to distort facts.

## Reusable structured object

```json
{
  "artifactType": "resume|cover_letter|profile|proposal",
  "target": {
    "role": "...",
    "organization": "...",
    "requirements": []
  },
  "claims": [
    {
      "text": "...",
      "evidenceRefs": [],
      "status": "verified|user_supplied|inferred|unknown"
    }
  ],
  "constraints": {
    "maxLength": null,
    "requiredKeywords": [],
    "forbiddenClaims": []
  },
  "review": {
    "factCheck": "pending",
    "metricCheck": "pending",
    "humanApproval": "required"
  }
}
```

## Integration with OmniCore

Professional documents should use the same provenance model as research, software and telecom artifacts:

```text
knowledge → evidence → claim → transformation → artifact
```

A generated sentence is therefore an **output artifact**, not an evidence source. The underlying fact remains the authority.

## Useful evaluation dimensions

| Dimension | Test |
|---|---|
| Factual fidelity | Every consequential claim maps to evidence |
| Role alignment | Relevant requirements are represented without distortion |
| Quantification | Metrics are sourced or reproducible |
| Specificity | Generic boilerplate is minimized |
| Consistency | Dates, titles and quantities agree across sections |
| Readability | Human reviewer can verify the claims quickly |
| Format robustness | Important information survives machine parsing |
| Revision safety | Changes do not silently introduce unsupported claims |

## Security boundary

Prompt instructions, stylistic preferences and role-play personas cannot authorize fabrication. The artifact compiler must fail closed when a requested statement has no acceptable evidence basis.
