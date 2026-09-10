# Knowledge Corpus — Iteration 26

Date: 2026-09-10

## Scope

This corpus integrates nine substantive uploaded sources from the current batch. `account_confirmation.PDF` is deliberately excluded from the knowledge base because it contains personal/financial account-identifying data and is not project knowledge.

## 1. AI digital products / commercialization

`7 Easy AI Digital Products.pdf` is a short visual guide to packaging AI-assisted digital products for sale. The visible pages emphasize themed content packs, reusable pre-written email/newsletter templates, niche-specific bundles, platform selection such as Etsy/Gumroad/Shopify/Teachers Pay Teachers, mockups, keyword-rich listings, bundle pricing/upsells, customer feedback and iterative refinement. The document explicitly frames the process as a roadmap for creating and selling AI-powered digital products. fileciteturn858file0L11-L19

Interpretation: opportunity/catalog material rather than a new engineering architecture. It reinforces P34/P56/P66/P67 commercialization patterns and the repository distinction between business hypothesis and verified business outcome.

## 2. Android AI launchers

`AI Launchery Android_ Ranking 2025-2026.PDF` describes a transition from static Android home screens toward contextual/predictive interfaces. It identifies algorithmic optimization, cloud integration and on-device processing as major architecture paths. fileciteturn858file1L31-L61

The report describes UsageStatsManager behavior sequences, contextual signals such as GPS, accelerometer, battery and time-of-day, and LLM-based semantic understanding of notifications/user intent. It also identifies NPU-enabled local inference and agentic launchers capable of performing actions inside applications without necessarily sending sensitive data to the cloud. fileciteturn858file1L67-L89

Interpretation: this is not a new project identity because the repository already has the PUI/Android launcher lineage in P57/P61. It strengthens the local-first, contextual and privacy-aware launcher branch.

## 3. Virtual-token/client-state security

`Analiza narzędzi do manipulacji żetonami_260402_174419.pdf` is a security/deconstruction corpus focused on client-side state, virtual currencies/tokens, browser storage, network/API boundaries and business-logic trust assumptions. It explicitly highlights the architectural weakness of treating browser/client state as authoritative. fileciteturn858file2L155-L185

The document surveys cookies, LocalStorage, SessionStorage and IndexedDB and shows why client-side token state must not be trusted without server-side cryptographic/business-logic validation. fileciteturn858file2L197-L215 fileciteturn858file2L324-L365

Repository interpretation: retain as defensive threat-model knowledge under P54/P72/P59. Offensive manipulation procedures are not promoted as capabilities; the reusable engineering lesson is authoritative-server state, integrity verification and abuse-resistant business logic.

## 4. AI App Builder / OmniStack architecture

`Analiza Repozytoriów i Projekt Aplikacji.PDF` compares Convex Chef, Wasp MAGE, Open Lovable, Open Design, CodinIT.dev, December, Dyad and Bolt.diy, then proposes an OmniStack AI synthesis. The source highlights differences between browser sandboxes, local daemons, Electron/Docker environments and compiler-oriented systems. fileciteturn858file3L425-L452

Key reusable patterns include MCP integration, multi-agent orchestration, hybrid browser/local execution, AST-RAG, visual design contracts, vendor-neutral model access, Docker isolation, Smart Context/Deep Smart Context and iterative test/repair. fileciteturn858file3L525-L554 fileciteturn858file3L571-L599

The roadmap describes a browser MVP, multi-agent v1, hybrid local Docker execution, AST-RAG and a later MCP/plugin/skill ecosystem. fileciteturn854file10L724-L756

Interpretation: absorbed into P100/P40/P61/P72/P80 rather than creating a duplicate app-builder project.

## 5. GGUF Agent Studio

`Aplikacja GGUF .pdf` documents a concrete Python + FastAPI + `llama-cpp-python` application. It directly loads GGUF files, streams chat through WebSockets, stores agent definitions and provides an Agents Builder. fileciteturn859file0L11-L29

The initial safe workspace intentionally limits tools to list/read/write inside a bounded workspace and omits default shell execution. fileciteturn859file0L95-L103

The later implementation record describes model routing, multi-model loading, purpose-specific models, agent graph editing, handoffs, agent memory/versioning/tests, Pydantic tool schemas, self-healing tool calls, Docker/Kubernetes sandboxes, RBAC, secret/PII/prompt-injection scanning, signed audit logs, repo ingestion, AST parsing, diff generation, PR foundations, React Flow, Monaco, live timelines and observability. fileciteturn853file9L465-L510 fileciteturn853file10L564-L680

Interpretation: this is a concrete implementation witness for P100, not a separate project. It materially improves the GGUF/local-model, agent-registry, sandbox and developer-environment layers.

## 6. IBM Cloud game backend

`Architektura Backendu IBM Cloud.PDF` specifies a Clean Architecture Go backend for a cognitive game using IBM Cloudant, IBM COS, Watsonx and IBM IAM. The architecture separates domain, use-case and infrastructure layers. fileciteturn858file4L710-L721

The source uses asynchronous Watsonx calls followed by Cloudant optimistic concurrency using `_rev`, retrying on 409 conflicts. It also validates JWTs locally from cached JWKS keys and uses authoritative server-side state rather than accepting client-provided game-stat values. fileciteturn858file4L736-L769

Interpretation: reusable backend architecture for game projects and P40/P72 security patterns; no distinct project identity. Important invariant reinforced: client intent is not authoritative state.

## 7. Private AI App Builder / Lovable architecture

`Architektura własnej platformy typu AI App Builder.PDF` analyzes Lovable as a blueprint for a private AI application builder. It describes Vite/React/TypeScript/Tailwind/Shadcn, Supabase, sandboxed execution and deployment modes ranging from managed cloud to self-managed Docker/Kubernetes. fileciteturn859file3L585-L620 fileciteturn859file3L635-L703

The report emphasizes Git as source of truth, MCP integration, Build/Plan modes, semantic Skills/RAG, RBAC/SSO and pre-publish security gates. fileciteturn859file3L725-L754 fileciteturn859file3L773-L796 fileciteturn859file3L799-L824

Interpretation: absorbed into P100/P40/P61/P72/P90. It strengthens the private/local-first and policy-gated application-builder design.

## 8. Animal adoption questionnaire

`ankietaadopcyjnapsy.pdf` is an adoption-screening questionnaire. It asks about household composition, children, time at home, allergies, existing animals, previous animals, travel, time alone, housing, walks, behavioral preparedness, training, costs, sterilization, pre/post-adoption visits and the ability to retrieve the animal. fileciteturn859file2L443-L489 fileciteturn859file2L490-L534

The puppy section adds questions about house training, frequent outings, socialization, destructive behavior, activity level and sterilization obligations. fileciteturn859file2L536-L574

Interpretation: this is a useful structured-procedure witness for P90 (SOP/process compiler) and potentially future animal-welfare workflows, but the single questionnaire does not justify a new project identity. Any future automated matching must treat questionnaire answers as evidence requiring human review, not as an autonomous welfare verdict.

## 9. Autonomous Unity AI

`Autonomiczne AI w Unity.PDF` defines a Unity-specific autonomous agent that transforms a blueprint/GDD/story into scenes, prefabs, scripts and game logic. The source stresses that the hard problem is state and 3D-space management, requiring an intermediate layer translating narrative intent into structured, verifiable engineering operations. fileciteturn859file1L128-L163

The architecture separates the AI brain from the Unity Editor and proposes MCP/UTCP for structured editor interaction. It describes scene hierarchy, console, prefab and project-state tools, plus UTCP/Code Mode for chaining editor operations. fileciteturn859file1L257-L304

The report proposes Roslyn in-memory C# compilation to avoid repeated domain reloads, including syntax parsing, metadata-reference resolution, compilation, memory emission and isolated loading. fileciteturn859file1L305-L373

For scene generation it recommends structured JSON/JSON Schema rather than unconstrained C# generation, with a Unity-side parser and explicit prefab persistence through UnityEditor APIs. fileciteturn859file1L395-L428

Decision: this crosses the threshold for a distinct project because it owns a Unity-specific narrative-to-production compiler/executor boundary. Created **P103 — OmniGame Unity Autonomous Production Engine MAX**.

## 10. Cross-corpus synthesis

Common engineering pattern:

`INTENT → STRUCTURED REPRESENTATION → CAPABILITY BROKER → SANDBOX → AUTHORITATIVE READBACK → VERIFY → AUDIT → PROMOTE/ROLLBACK`

Recurring hard invariants:
- model capability != authorization;
- client/UI state != authoritative state;
- generated code/assets remain untrusted until tested;
- MCP/tool integration != authorization;
- simulation != production evidence;
- memory/retrieval != permission;
- business opportunity != verified commercial outcome;
- adaptive interfaces require privacy/consent/reversibility;
- self-healing remains versioned candidate evolution.
