# Corpus — Google Antigravity 2.0 / Remote Control / A2UI / Recursive Agent Orchestration

Date: 2026-09-12
Classification: external architecture benchmark + strategic extension for P100

## 1. Input

The user supplied a strategic architecture report proposing three pillars for Google Antigravity: graph-based Mission Control with Generative UI, mobile/remote human-in-the-loop control, and a Master Agent / Agent Factory capable of creating persistent agent definitions in the project filesystem.

The report proposes:
- Mission Control as a graph rather than a linear task list;
- A2UI-style declarative decision surfaces;
- artifact-centric review and annotation;
- a mobile decision console;
- Zero Trust remote access;
- a Master Agent that creates specialized agents;
- filesystem-persisted SKILL.md definitions;
- hot-loading of newly created skills/agents;
- sandboxed self-testing and repair before promotion.

## 2. Current external verification

Current Google Antigravity documentation materially changes the baseline assumed by the supplied report. Antigravity 2.0 is now documented as a standalone desktop command center, separate from the IDE, supporting synchronous and asynchronous agent orchestration, system commands, file operations, web search, skills, MCP servers, subagents, Chrome interaction, artifacts and implementation plans. The official documentation therefore confirms that the product category has already moved beyond the earlier "IDE + Mission Control" framing.

Google also documents Remote Control for Antigravity 2.0: desktop sessions can be driven and monitored from a web browser, including from a mobile device, while preserving the workstation's local filesystem, toolchains, credentials and Git worktrees. Push notifications can signal completion or required user input. This supersedes the supplied report's assumption that a dedicated Flutter mobile application is necessarily the first implementation of remote control.

Antigravity 2.0 also documents project-scoped settings, project-scoped permissions, Git worktrees, browser-agent integration, Git-native review and agent-edit diffs.

The current official agent documentation confirms custom agents, dynamic subagents, subagent monitoring/termination, inline tool approvals and local agent definitions under `.agents/agents/<name>/agent.md`. This validates the strategic direction of persistent specialized agents, but not the stronger claim that Antigravity's core system already contains an autonomous Master Agent that freely generates and hot-loads new agents.

Antigravity's artifact model is directly aligned with the report: implementation plans, code diffs, architecture diagrams, images and browser recordings are structured deliverables used for asynchronous human review and steering.

## 3. A2UI status

The supplied report names A2UI v0.8. The current A2UI documentation identifies v0.8 as a legacy release and points to v0.9.1 as current, v0.9 as stable and v1.0 as a candidate. Therefore any implementation proposal must not freeze a new P100 protocol contract to v0.8 without a compatibility decision.

The A2UI model is relevant to P100 because it separates declarative UI structure from client rendering and uses a catalog contract between agent and renderer. P100 should treat A2UI as a possible protocol adapter, not as an authorization layer. A generated decision surface must still map to explicit authorization state transitions.

## 4. Remote-control security implications

The supplied report's Zero Trust direction is technically compatible with current Cloudflare Tunnel/Access architecture: Cloudflare documents outbound-only Tunnel connections, no required inbound public port, and Access policies for request-level identity enforcement. Service tokens provide machine-to-machine credentials and are rotatable/revocable.

However, a tunnel is transport security, not authorization for consequential agent actions. P100 must retain its invariant:

OBSERVE → PLAN → AUTHORIZE → ACT → READBACK → VERIFY

Remote UI input is a proposal/authorization request until the local capability broker validates identity, scope, freshness, policy and postconditions.

## 5. Strategic extraction for P100

The report strengthens six P100 capabilities:

1. **Mission Graph** — graph projection of agents, dependencies, blockers, dataflow and delegation.
2. **Decision Surface / GenUI** — structured, catalog-versioned UI for approvals and review instead of chat-only interaction.
3. **Artifact Review Plane** — plans, diffs, screenshots, recordings and evidence as first-class review objects.
4. **Remote Control Plane** — browser/mobile control of long-running local sessions without exposing a general-purpose shell.
5. **Persistent Agent Registry** — versioned, project-scoped agent definitions and skills with validation before activation.
6. **Agent Factory / Meta-Orchestrator** — controlled creation of candidate agents, sandbox validation, approval and promotion.

## 6. Required safety boundary

The report's phrase "self-healing" and its recursive Master Agent concept must be constrained. Generated agent definitions, tools and permissions are candidate artifacts. They cannot silently become privileged runtime capabilities.

Required lifecycle:

DRAFT → SCHEMA VALIDATE → STATIC CHECK → SANDBOX TEST → POLICY REVIEW → HUMAN/BOUND AUTHORIZATION → REGISTER → ACTIVATE → OBSERVE → VERIFY → ROLLBACK

No file watcher or hot-reload event is itself authorization.

## 7. Competitive conclusion

Google Antigravity is now a strong external benchmark for P100 because it demonstrates convergence of standalone agent orchestration, subagents, artifacts, MCP/skills, browser control, project-scoped permissions and remote control. The strategic gap for P100 is therefore not simply "build an agentic IDE". The differentiating layer is a provider-neutral, cross-runtime control plane that can apply one authorization, provenance, verification and audit model across Antigravity-like agents, Unity, Unreal, IDEs, mobile agents, local runtimes and other execution surfaces.

## 8. Evidence classification

- User-supplied strategic report: source proposal / architecture hypothesis.
- Google Antigravity official docs: current external product evidence.
- A2UI official specification: protocol evidence.
- Cloudflare official docs: transport/access-control evidence.
- Claims about P100 implementation: design requirements until independently implemented and verified.
