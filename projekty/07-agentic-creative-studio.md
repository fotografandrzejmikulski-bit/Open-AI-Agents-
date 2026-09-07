# 07 — AGENTIC CREATIVE STUDIO

## Purpose
A multimodal creative-development environment that turns natural-language intent into inspectable, testable application and content artifacts.

The supplied Claude comparison highlights strong long-form writing, code refactoring/debugging and complex reasoning, while Gemini is described as strong in Google ecosystem integration, realtime search and multimodal processing. fileciteturn195file0L7-L22 The capabilities inventory covers web/mobile applications, APIs, databases, debugging, research, document analysis, data work and technical writing. fileciteturn195file1L56-L100

## Product model

```text
Natural Language Intent
        ↓
Requirements Extractor
        ↓
Project Specification
        ↓
Planner / Agent Runtime
        ↓
Artifact Graph
 ┌──────┼─────────┐
 UI   Backend    Data
  │      │         │
 Tests  Tools    Knowledge
        ↓
Verification Gate
        ↓
Preview / Export / Deploy
```

## Core capabilities

### Application generation
- React/TypeScript web applications
- API services
- database schemas/migrations
- authentication
- background jobs
- dashboards
- PWA/mobile-oriented frontends

### Creative generation
- copy and long-form content
- visual specifications
- campaign assets
- product narratives
- documentation
- pitch and grant artifacts

### Research
- web-connected source collection
- PDF/document extraction
- source comparison
- evidence ledger
- claim confidence

## Multi-agent topology

Use specialists only where their tool/policy surface differs materially:

```text
Manager
├── Product Architect
├── UI Engineer
├── Backend Engineer
├── Data Engineer
├── Security Engineer
├── Test Engineer
└── Research Analyst
```

Agents return structured artifacts; the manager owns the final project state.

## Artifact contract

Each generated artifact contains:

```json
{
  "artifactId": "...",
  "type": "application|document|design|test|research",
  "version": "...",
  "sourceRefs": [],
  "dependencies": [],
  "validation": {
    "status": "pass|fail|partial",
    "checks": []
  }
}
```

## Builder integration

The design deliberately supports two modes:

**Visual mode:** product owners compose screens, data and workflows.

**Code mode:** engineers inspect and modify ordinary source files and explicit runtime contracts.

The builder is never the only source of truth.

## Evaluation

Every generated application should receive:
- static checks
- unit/integration tests
- accessibility tests
- security checks
- schema validation
- runtime smoke tests
- agent behavior evals when agents are included

## Research provenance

Every externally derived claim is attached to a source reference. Generated synthesis must distinguish:
- source fact
- inference
- assumption
- recommendation
- unresolved uncertainty

## Safety

The platform blocks hidden instructions, credential exfiltration, unauthorized deployment and unreviewed destructive operations. It should refuse workflows that attempt to use covert persuasion or manipulative behavioral targeting.

## MVP

1. project specification generator
2. typed artifact graph
3. planner/manager agent
4. 3 specialist agents
5. code artifact generator
6. document artifact generator
7. test/eval runner
8. evidence ledger
9. preview UI
10. export to Git repository

## End state

The result is not "AI-generated code" but a continuously verified project workspace in which requirements, implementation, tests, sources and deployment artifacts remain synchronized.