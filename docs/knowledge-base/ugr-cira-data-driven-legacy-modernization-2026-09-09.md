# UGR + CIRA Data-Driven Legacy Modernization — 2026-09-09

## Source
`Migracja kodu z UGR i CIRA (1).pdf`

## Source-derived architecture
The document treats source code as structured data and proposes a Universal Graph Registry combining control-flow, data-flow and dependency representations. The CIRA agent is then organized as an Observe–Orient–Decide–Act loop over that graph. fileciteturn189file0L15-L42

The proposed IDE architecture separates a server-side CIRA reasoning layer from lightweight IDE clients, with local graph caching, asynchronous heavy queries, JSON configuration and authenticated access. fileciteturn189file8L337-L364

Migration actions operate through AST-level transformation rather than textual find/replace, followed by continuous graph consistency verification. fileciteturn182file7L297-L306

## Reusable pipeline
```text
REPOSITORY
 ↓
PARSE / INDEX
 ↓
CODE PROPERTY GRAPH
 ↓
IMPACT ANALYSIS
 ↓
MIGRATION PLAYBOOK
 ↓
AST TRANSFORMATION
 ↓
DIFF + HUMAN REVIEW
 ↓
COMPILE / TEST
 ↓
GRAPH RE-INDEX
 ↓
POSTCONDITION
```

## Scalability controls
The source proposes graph partitioning, incremental parsing and compressed path representations for very large codebases. It also emphasizes human approval and automated tests because LLM-generated migrations can contain subtle logical errors. fileciteturn189file2L110-L128

## Portfolio impact
This is primarily an evolution of Projects 23, 28, 40, 41, 61 and 65, not a new numbered project.
