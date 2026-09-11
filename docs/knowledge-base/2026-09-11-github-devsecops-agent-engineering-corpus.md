# GitHub DevSecOps & Agent Engineering Corpus — 2026-09-11

## Corpus status

`38/38 SOURCES AUDITED → EXTERNAL-VERIFIED REFERENCE KNOWLEDGE → PORTFOLIO IMPACT`

The supplied GitHub/GitHub-adjacent URL corpus was audited link-by-link. Each URL is classified below as engineering input, portfolio/governance input, discovery context, or no material engineering delta. Failed dynamic pages are recorded as such rather than silently inferred.

## High-value findings added by the complete audit

1. GitHub's current organization surface exposes an integrated control plane spanning repositories, Projects, Packages, Actions, Codespaces, code security, MCP Registry and agentic workflows. The live repository index also surfaces `gh-aw`, `gh-aw-actions`, `gh-aw-firewall`, `gh-aw-mcpg`, `artifact-attestations-opa-provider`, `copilot-sdk`, `redacting-logger`, CodeQL and the official GitHub MCP Server. These are reference patterns, not proof that equivalent components exist locally.
2. GitHub's official organization page identifies `github-mcp-server` as its official MCP Server. This strengthens the existing P100/P72 distinction between MCP capability exposure and authorization rather than creating a new project.
3. The GitHub Community repository index explicitly contains onboarding checklists for Code Security, Secret Protection and GitHub Advanced Security, reinforcing a checklist/evidence-gate layer around security enablement.
4. Marketplace is not only a discovery catalog: current listings demonstrate integrations for CI/CD, code review, visual testing, backups, quality/security and mobile delivery. The architectural lesson is capability packaging + permissioning + evidence, not indiscriminate installation.
5. GitHub's public roadmap uses explicit release phases (`exploring`, `in design`, `preview`, `ga`) plus feature-area/SKU/deployment labels. This is useful as a typed lifecycle model for project roadmap evidence.
6. GitHub's public organization profile demonstrates a bounded presentation layer: profile README, pinned repositories and organization metadata. This is relevant to repository presentation, not core runtime engineering.
7. GitHub Community discussions are a live feedback/incident signal surface; the current page includes Actions failures, Packages issues and programming help. This supports a feedback→triage→change→verification loop.
8. The NASA Ingenuity case study provides concrete evidence that dependency graphs extend far beyond direct dependencies: the project depended on thousands of open-source contributors and layered dependencies. This strengthens dependency provenance and SBOM-style thinking.
9. Electron's current site exposes Forge, Fiddle, security documentation and current stable runtime information. P100 should treat Electron version, packaging toolchain and security checklist as release inputs, not merely UI implementation details.
10. npm's current documentation explicitly covers audit reports, provenance statements, OIDC trusted publishing, staged publishing, ECDSA registry signatures, 2FA and malware reporting. This materially strengthens P100's package-supply-chain controls.
11. npm's current access-token documentation adds an important credential rule: token scope is bounded by user permission, organization access does not itself grant package publishing, and CI/CD publishing should prefer trusted publishing where possible.
12. GitHub Careers was audited as organizational/process context, not product-engineering evidence. It reinforces ownership, shipping-to-learn, architecture briefs, CI/CD, operational excellence and cross-functional product engineering as process patterns, but it does not justify a portfolio project.
13. GitHub Learn / Well-Architected pages were reachable only through partial/dynamic rendering in this audit. Search indexing confirms a Well-Architected library and checklist structure, but the complete page content was not reliably retrievable; therefore no detailed framework claims are promoted to verified knowledge.

## Link-by-link audit

| # | Supplied URL / source | Classification | Portfolio effect |
|---:|---|---|---|
| 1 | `github.com/github/docs` | GitHub Docs open-source repo/contribution model | P100 documentation-as-interface; governance evidence |
| 2 | `github.com/orgs/github/repositories` | Live organization repository inventory | P100 discovery; agentic/DevSecOps reference patterns |
| 3 | `github.com/orgs/github/projects?query=is:open` | Live project/planning surface | P100 roadmap/project-control adapter |
| 4 | `github.com/orgs/github/packages` | Live package/artifact surface | P100 artifact/package control plane |
| 5 | `docs.github.com/.../artifact-metadata` | Artifact metadata/provenance API | P100/P117/P119 release identity |
| 6 | `learn.github.com/well-architected/` | Well-Architected landing/dynamic source | P100 governance model; detailed claims bounded |
| 7 | `learn.github.com/` | GitHub Learn platform | P100 knowledge/learning discovery; no new runtime |
| 8 | `docs.npmjs.com/` | npm registry/CLI/security docs | P100 dependency and publishing governance |
| 9 | `electronjs.org/` | Electron platform + Forge/Fiddle/security | P100 desktop runtime and packaging hardening |
| 10 | `codeql.github.com/docs/` | CodeQL reference docs | P100/P117/P119 SAST evidence gates |
| 11 | `github.com/open-source/sponsors` | Sponsor/distribution/community surface | governance/distribution only |
| 12 | `github.com/github` | GitHub organization profile | P100 ecosystem reference; official MCP Server identified |
| 13 | `github.com/opensource.guide` | Open Source Guides repo | repository governance/documentation practice |
| 14 | `github.com/readme/featured/nasa-ingenuity-helicopter` | open-source dependency case study | dependency/provenance/SBOM reasoning |
| 15 | `github.com/orgs/github/repositories?q=template:true archived:false` | repository discovery filter | P100 template/environment discovery |
| 16 | `github.com/orgs/github/repositories?q=archived:true` | archive inventory filter | lifecycle/retirement metadata; no new project |
| 17 | `github.com/orgs/github/repositories?q=fork:true archived:false` | fork inventory filter | lineage/source-origin metadata |
| 18 | `github.com/orgs/github/repositories?q=mirror:false fork:false archived:false` | source-of-truth inventory filter | repository lineage policy |
| 19 | `github.com/orgs/github/repositories?q=visibility:public archived:false` | public repository filter | visibility/classification policy |
| 20 | `github.com/github/roadmap` | typed public roadmap | P100 roadmap state machine |
| 21 | `github.careers/careers-home` | organizational/process source | engineering-process principles only |
| 22 | `docs.github.com/.../customizing-your-organizations-profile` | organization presentation docs | repository presentation/profile layer |
| 23 | `docs.github.com/.../github-terms-of-service` | contractual/legal source | operational/legal boundary; no runtime feature |
| 24 | `github.com/orgs/community/discussions` | live feedback/incident surface | P100 feedback→triage loop |
| 25 | `github.com/orgs/community/repositories` | Community repo inventory | security onboarding/checklist patterns |
| 26 | `github.com/mcp` | MCP ecosystem/discovery URL | MCP capability ecosystem reference; no authority upgrade |
| 27 | `github.com/community/community` | community repository | feedback taxonomy + product signal |
| 28 | `github.com/community` | community landing | discovery/support only |
| 29 | `github.com/explore` | topic/collection discovery repo | capability/research discovery |
| 30 | `github.com/topics` | topic discovery surface | agent research/discovery input |
| 31 | `github.com/collections` | curated collection discovery | research/discovery input |
| 32 | `github.com/resources/events` | event/webinar discovery | knowledge acquisition only |
| 33 | `github.com/sponsors/explore` | sponsor discovery | ecosystem/governance only |
| 34 | `github.com/marketplace` | marketplace catalog | P100 capability packaging/discovery/trust model |
| 35 | `github.com/marketplace?type=apps` | Apps catalog | P100 install/permission/version/security boundary |
| 36 | `github.com/marketplace?type=actions&category=mobile` | mobile Actions catalog | P117 CI/CD/mobile release ecosystem |
| 37 | `github.com/features/ai/github-app` | GitHub Copilot App / agentic development surface | P100 agentic developer-workflow reference |
| 38 | `github.com/codespaces` | Codespaces entry/auth surface | P100 reproducible dev-environment pattern |

## Canonical engineering synthesis

```text
INTENT
 ↓
CONTEXT / SOURCE
 ↓
PLAN
 ↓
AUTHORIZE
 ↓
IMPLEMENT
 ↓
TEST
 ↓
SAST / CODEQL
 ↓
DEPENDENCY / SUPPLY-CHAIN CHECK
 ↓
BUILD ENVIRONMENT IDENTITY
 ↓
ARTIFACT DIGEST
 ↓
PROVENANCE / ATTESTATION
 ↓
DEPLOYMENT RECORD
 ↓
AUTHORITATIVE READBACK
 ↓
VERIFY
 ↓
AUDIT / RELEASE EVIDENCE
```

## Project impact

### P100 — NeXus AI Code OMEGA-X

Highest impact. Absorb Codespaces/dev-container reproducibility, CodeQL, npm provenance/trusted publishing, artifact attestations, GitHub Projects/Actions/Packages, official GitHub MCP integration, Marketplace capability packaging, agentic-workflow/firewall/gateway reference patterns, Electron hardening and typed roadmap/feedback states.

### P117 — NeXus Mobile Multimodal Agent Runtime MAX

Strengthen Android release assurance with Kotlin/Java SAST, mobile Actions patterns, APK/AAB digest/provenance, deployment records and device readback. Marketplace mobile Actions are ecosystem evidence only.

### P119 — OmniMAS Local Android Agent Runtime MAX

Strengthen CI/release controls: Kotlin/Java CodeQL, reproducible environment, dependency policy, artifact digest/provenance, device deployment/readback and selective notification projection. No new Android privilege is inferred from GitHub sources.

### P72 / P114

Strengthen reusable assurance semantics: artifact identity, evidence chain, provenance, credential boundaries and promotion gates.

### New project decision

**No new numbered project.** The complete corpus is still cross-cutting and fits existing control-plane, mobile-release and assurance boundaries.

## Evidence boundaries

- External documentation/page content: **EXTERNAL-VERIFIED CONTEXT**.
- Dynamic/failed retrieval: **BOUNDED / NOT FULLY RETRIEVED**.
- Portfolio mappings: **ARCHITECTURE SYNTHESIS**.
- Existing project implementation: requires independent repository/source evidence.
- CodeQL, provenance, attestations and trusted publishing are **requirements**, not claims of current local implementation.
