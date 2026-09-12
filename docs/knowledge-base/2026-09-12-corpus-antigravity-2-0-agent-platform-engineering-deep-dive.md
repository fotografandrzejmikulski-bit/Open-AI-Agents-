# Corpus: Antigravity 2.0 — Agent Platform Engineering Deep Dive

**Date:** 2026-09-12
**Role:** source-derived engineering corpus + verification delta
**Primary integration:** P100 — NeXus AI Code / OMEGA-X Agentic Development Environment

## 1. Source assessment

The supplied material describes Antigravity 2.0 as an agent-first development platform centered on Projects, a shared agent harness, subagents, artifacts/implementation plans, skills, plugins, MCP, hooks, terminal sandboxing, scheduled tasks, voice transcription and an SDK. This framing is strongly supported by current official Google Antigravity documentation and blog material.

Official verification confirms:
- Antigravity 2.0 is a standalone desktop command center for agents on macOS, Linux and Windows; it operates independently of an IDE and supports synchronous/asynchronous work, system commands, file operations, web search, skills/MCP, subagents, Chrome, artifacts and implementation plans.
- Projects can aggregate one or multiple folders and have isolated agent settings/security settings.
- Plugins can package skills, agents/subagents, rules, MCP servers and hooks; the CLI plugin filesystem uses `plugin.json`, with optional `mcp_config.json`, `hooks.json`, `skills/`, `agents/` and `rules/`.
- Skills use Markdown with frontmatter metadata; global skills can live under `~/.gemini/antigravity-cli/skills/`.
- Hooks can intercept actions immediately before/after tool execution; `/hooks` exposes loaded hooks.
- MCP is supported for local and remote servers; the SDK can connect stdio, SSE and HTTP MCP servers.
- The Terminal Sandbox is documented as a lightweight isolation mechanism for destructive file operations and unauthorized outbound network requests.
- Antigravity SDK is a Python preview exposing the Antigravity agent runtime, built-in tools, declarative safety policy, lifecycle hooks and stateful sessions.
- Dynamic subagents are explicitly documented and inherit the main agent's tool/security permissions rather than acquiring broader authority.
- Current September 2026 product state has moved beyond the original Gemini 3.5 Flash baseline: the official changelog records Antigravity 2.12.2 with Gemini 3.8 Flash via ADC for AGY Enterprise. Therefore any architecture documentation must treat model/version claims as time-indexed rather than permanent.

## 2. Claims that require qualification

The supplied text contains several claims that should NOT be promoted to verified facts without additional primary evidence:

1. "Gemini 3.5 Flash is four times faster than competitors" is a vendor claim with context-dependent comparison; it must be preserved as a dated product claim, not a universal engineering constant.
2. "Milliseconds determine agent loop quality" is an inference, not a demonstrated Antigravity specification.
3. The text asserts a four-surface consolidation/deprecation story and a hard 18 June 2026 migration deadline; the currently inspected official sources do not establish that exact deadline or all claimed deprecations.
4. The text describes Antigravity CLI as rewritten in Go; this was not established by the inspected official documentation and should remain unverified.
5. The supplied model/version statements are already stale relative to the September 2026 changelog.
6. Exact sandbox implementation claims (`nsjail`, `sandbox-exec`, `AppContainer`) and exact `enableTerminalSandbox` configuration semantics require version-specific primary-source confirmation before implementation.
7. Exact hook event taxonomy and precedence described in the supplied text should be treated as source claims until mapped to the current official schema. Official sources confirm hooks but do not, from the inspected material alone, establish every named event and precedence rule.
8. Exact voice-transcription implementation details and claims about Gemini Audio should remain product claims unless documented in current official docs.
9. "Zero startup overhead", "absolute" security guarantees and equivalent language are engineering overclaims; isolation reduces blast radius but does not make an agent trustworthy.
10. A skill is an instruction bundle, not an authorization boundary. `allowed-tools`, rules or descriptions cannot replace server-side capability policy.

## 3. Architectural extraction for P100

The material materially strengthens the P100 architecture in seven areas:

### A. Project-as-security-domain

Treat an agent Project as a scoped execution context:
`PROJECT_ID → FOLDER_SET → RULE_SET → MCP_ALLOWLIST → TOOL_POLICY → NETWORK_POLICY → AGENT_IDENTITY`.

The important P100 extension is to make this scope authoritative in the control plane, not merely a desktop preference.

### B. Plugin/Skill supply chain

Model:
`PLUGIN_MANIFEST → SKILL_METADATA → SKILL_BODY → REFERENCED_RESOURCES → TOOL_SCOPE`.

Every imported skill/plugin becomes an untrusted candidate until:
- provenance is known,
- content is hashed,
- declared capabilities are compared with observed capabilities,
- policy compatibility is checked,
- and activation is explicitly authorized.

### C. Progressive disclosure

Antigravity's skill model supports a useful three-stage optimization:
`DISCOVER METADATA → LOAD INSTRUCTIONS → LOAD REFERENCED RESOURCES`.

P100 should generalize this into a context-budget policy with provenance and ACL checks at every stage.

### D. Hook interception

Hooks become a policy enforcement plane around tool execution:
`PROPOSE → PRE-TOOL POLICY → EXECUTE → POST-TOOL OBSERVATION → VERIFY`.

A hook result is not itself authorization unless the authoritative policy engine says so.

### E. MCP federation

MCP should remain a capability transport/federation layer, never the authority layer:
`AGENT → CAPABILITY BROKER → MCP SERVER → TOOL → READBACK → VERIFY`.

MCP configuration, credentials and tool schemas require identity binding, scope, expiry, provenance and audit.

### F. SDK / embedded runtime

The SDK benchmark adds a programmatic embedding surface to P100:
`APPLICATION → AGENT RUNTIME → POLICY ENGINE → LIFECYCLE HOOKS → MCP/TOOLS → SESSION STATE → AUDIT`.

The SDK must not be allowed to bypass the same authorization and verification path as desktop/CLI agents.

### G. Agent-first SDLC

The supplied `/grill-me → implementation plan → parallel subagents → artifacts → execution → verification` workflow is a strong reference pattern, but P100 should formalize it as:
`OBSERVE → SPECIFY → CHALLENGE → PLAN → AUTHORIZE → DELEGATE → ACT → READBACK → VERIFY → REVIEW → PROMOTE`.

## 4. Security invariants added/strengthened

- `PROJECT_SCOPE ≠ AUTHORIZATION`
- `PLUGIN_MANIFEST ≠ TRUST`
- `SKILL_INSTRUCTION ≠ PERMISSION`
- `MCP_SERVER ≠ TRUSTED_CAPABILITY`
- `HOOK_ALLOW ≠ FINAL_AUTHORIZATION`
- `TOOL_RESULT ≠ POSTCONDITION`
- `SANDBOX_PASS ≠ PRODUCTION_APPROVAL`
- `SDK_ACCESS ≠ POLICY_BYPASS`
- `MODEL_VERSION ≠ PERMANENT_MODEL_IDENTITY`
- `ARTIFACT ≠ VERIFIED_IMPLEMENTATION`
- `SUBAGENT ≠ INDEPENDENT_AUTHORITY`
- `SCHEDULED_TASK ≠ UNBOUNDED_PERSISTENCE`

## 5. New reusable primitives

`project-security-context`
`plugin-supply-chain-record`
`skill-provenance-envelope`
`progressive-context-loader`
`hook-policy-interceptor`
`mcp-capability-lease`
`sdk-runtime-policy-bridge`
`model-version-provenance-record`
`agent-mission-challenge`
`artifact-verification-record`
`scheduled-agent-policy`

## 6. Integration decision

**No standalone project is justified.** The material is a high-value reference architecture and competitive benchmark for P100, especially the Projects + Plugins/Skills + Hooks + MCP + SDK + Subagents stack. It should extend the existing Antigravity/P100 work rather than fragment the portfolio.

## 7. Source links

Official sources inspected on 2026-09-12:
- https://antigravity.google/docs/overview
- https://antigravity.google/docs/projects/
- https://antigravity.google/docs/cli/features/
- https://antigravity.google/docs/cli/plugins/
- https://antigravity.google/docs/mcp
- https://antigravity.google/blog/introducing-google-antigravity-2
- https://antigravity.google/blog/introducing-google-antigravity-sdk
- https://antigravity.google/blog/google-io-2026
- https://antigravity.google/changelog
