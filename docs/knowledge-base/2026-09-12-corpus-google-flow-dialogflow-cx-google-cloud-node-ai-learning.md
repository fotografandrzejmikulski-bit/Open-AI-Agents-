# Knowledge Corpus — Google Flow / Dialogflow CX / Google Cloud Node.js / Google AI Professional Certificate

Date: 2026-09-12
Evidence class: mixed current official product/documentation evidence plus secondary source and educational reference.

## Sources reviewed

- Google Cloud Node.js client libraries repository.
- Dialogflow CX Node.js `Flow` API reference.
- Dialogflow CX official Flow concept documentation.
- Google Flow official product/help pages.
- Google Flow Agent, tools, projects/assets, video/image editing and model-support documentation.
- Google Workspace administrator documentation for enabling Flow.
- Google AI Professional Certificate on Coursera.
- AtlasCloud secondary Veo 3.1 / Flow guide.

## Google Cloud Node.js client library layer

The official `google-cloud-node` repository is the umbrella for idiomatic Node.js client libraries for Google Cloud services. The repository currently lists libraries including Dialogflow CX API, Generative Language, Vertex AI, Storage, Kubernetes Engine, Monitoring, Secret Manager, Video Intelligence, Vision and many other services.

The repository recommends the listed service-specific libraries for Node.js applications. Before interacting with a service, its API must be enabled. Authentication guidance includes Application Default Credentials and explicitly warns not to commit service-account credential files to source control.

The libraries follow the Node.js release schedule, use Semantic Versioning, and distinguish Stable and Preview quality levels. `0.x.y` releases may contain backwards-incompatible changes.

## Dialogflow CX Flow model

Official Dialogflow CX documentation defines Flows as structures for organizing conversational topics and associated conversational paths. Every agent has a Default Start Flow; more complex agents can use multiple flows owned/maintained by different development responsibilities.

A Flow has a Start page. The official Node.js API reference exposes Flow properties including:
- advancedSettings;
- description;
- displayName;
- eventHandlers;
- knowledgeConnectorSettings;
- locked;
- multiLanguageSettings;
- name;
- nluSettings;
- transitionRouteGroups;
- transitionRoutes.

The API supports serialization/verification plus create/update/patch-oriented resource operations through the generated client model. The official concept documentation also describes creating and importing/exporting flows and conflict handling when importing referenced resources.

Architectural interpretation:

`FLOW = explicit conversational state-space + routes + event handlers + NLU/settings + knowledge connectors`

This is useful as a reusable state-machine/control-flow abstraction, not as evidence that Dialogflow should become the canonical orchestration authority for all P100 agents.

## Google Flow — current product surface

Official Google Flow documentation currently describes Flow as an AI filmmaking tool for creating cinematic clips, scenes and stories with consistency. It supports web/desktop and mobile app surfaces; the most advanced editing features are available on computer.

Current access documentation says users need age verification, a supported region and an eligible Google AI subscription, with qualifying Workspace editions receiving Flow access under the documented conditions.

## Google Flow Agent

The official Flow Agent is a built-in creative collaborator. It can:
- brainstorm and plan storyboards/mood boards;
- refine prompts;
- generate images/videos and select an appropriate model;
- edit selected media;
- batch-generate variations;
- rename/group/delete assets;
- use project/device references as context;
- maintain project-specific sessions;
- receive project-level Agent Instructions.

The Agent's generated media uses Flow credits. Agent queries themselves do not currently consume credits but are subject to daily quotas.

The official documentation exposes a confirmation control before actions that consume AI credits. This is an important human-approval pattern for P97/P100: consequential generation can have a pre-action approval state.

## Google Flow tools / mini-apps

Official documentation states that users can create custom reusable Tools and mini-apps using natural language. Flow generates the code and interface, after which the user reviews and saves changes. Tools can be edited conversationally, favorited, pinned, remixed and shared.

Sharing a Tool exposes its code, name and thumbnail to anyone with the link; a shared link represents the version of the Tool at the time the link was generated. This is a concrete supply-chain/provenance consideration for P100.

Tool-generated media uses Flow credits, and Flow displays a warning when a Tool may consume credits.

## Flow project/asset architecture

Official documentation describes project-scoped organization of images, videos, characters, scenes and uploads. Projects/assets synchronize between supported Flow surfaces. Characters can bundle visual and audio references into reusable entities, including a selected or custom voice.

Collections can be nested and used for organization. The Agent can rename files, create collections and remove unused assets.

This maps strongly to CineMatrix Film World State:

`PROJECT → ASSET REGISTRY → CHARACTER → SCENE → VIDEO/IMAGE ASSET → COLLECTION`

but CineMatrix retains its own canonical Film World State and provenance rather than treating a vendor UI library as the system of record.

## Flow generation and continuity capabilities

Official video documentation supports generation from text prompts, ingredients/references, frames and other videos. Ingredients allow repeated use of the same visual references for characters and key objects.

Current model documentation shows feature differences across Veo 3.1 Lite/Fast/Quality and Gemini Omni Flash. Examples include text-to-video, first-frame and first+last-frame generation, ingredients/references, video-to-video editing and clip extension depending on model.

The current documentation explicitly instructs users to check the active model, resolution and latest credit costs before generation.

This reinforces P113's live model registry requirement and P97's model-adapter/provenance model.

## Flow editing / scene building

Flow preserves previous versions of edited media in a History panel along with prompts. Generated Veo clips can be extended under documented model constraints. Frames can be saved as reusable ingredients/start/end frames. Scenebuilder can arrange, reorder, trim and preview multiple clips as a sequence and download a scene.

Architectural extraction:

`GENERATE → VERSION HISTORY → FRAME/REFERENCE EXTRACTION → SCENE ASSEMBLY → PREVIEW → EXPORT`

This is directly relevant to CineMatrix shot continuity and render lineage.

## Flow data / privacy boundary

Official documentation states that Google collects interactions, tool outputs, related product-usage information and feedback, and documents controls concerning improvement/training-related settings and project deletion. Flow Tool and Agent data can also be deleted through documented controls.

Therefore Flow must not be treated as an automatically local/private renderer. P97/P100 should classify the Flow provider surface according to current account, workspace, data-use and project policy before sensitive assets are routed to it.

## Google AI Professional Certificate

The current Coursera page describes an 8-course Google AI Professional Certificate focused on AI fluency and practical workplace applications. It includes AI fundamentals, responsible use, prompting, brainstorming/planning, research, writing/communication, content creation, data analysis, app building and deployment.

The program emphasizes evaluating AI outputs for accuracy/bias and applying critical thinking, as well as building and testing custom applications and preparing them for sharing/access control.

Architectural value for the repository:
- educational material is a competency/reference layer;
- prompt patterns become reusable strategies;
- responsible-AI evaluation becomes an evaluation dimension;
- completion/certification never grants production capability authorization.

## Secondary source

AtlasCloud's Veo 3.1 guide is treated as secondary practical guidance only. Its recommendations about prompting, model selection, consistency and export workflows are useful hypotheses/workflow hints, but official Google documentation remains authoritative for current product capabilities, supported features and access conditions.

## Cross-project integration

### P97 CineMatrix
- Google Flow becomes a verified external video/image generation adapter candidate.
- Flow Agent becomes a benchmark for agent-assisted cinematic planning and batch generation.
- Flow project/asset/character/scene concepts map to CineMatrix's Film World State.
- History, frames, ingredients and Scenebuilder strengthen shot lineage and continuity modeling.
- Flow credit consumption becomes part of cost-aware render routing.

### P113 OmniVisual Prompt Compiler
- live Google capability/model registry;
- model-specific feature matrix;
- first/last-frame and ingredients capability flags;
- model/resolution/cost compatibility checks;
- provider-neutral canonical scene/shot IR.

### P100 NeXus AI Code / OMEGA-X
- Google Cloud Node.js client libraries as provider SDK/adapter inventory;
- Dialogflow CX Flow as a state-machine/control-flow adapter;
- Flow Tools as generated-code candidate artifacts requiring provenance, review and activation controls;
- Google Cloud authentication/secret handling as capability-bound credential policy;
- Flow Agent confirmation before credit-consuming actions as a human-approval UX benchmark;
- Flow Tool sharing as supply-chain/provenance risk;
- project/asset synchronization as external state, not authority.

### P21 Google AI Sovereign Developer Stack
- Google Cloud Node.js and Dialogflow CX strengthen the Google service-adapter layer;
- Flow provides an additional multimodal creative surface;
- Coursera provides competency/evaluation material.

## Security and epistemic invariants

`FLOW TOOL CODE ≠ TRUSTED CODE`

`SHARED TOOL LINK ≠ AUTHORIZATION`

`FLOW PROJECT STATE ≠ CANONICAL PROJECT STATE`

`MODEL FEATURE AVAILABILITY ≠ UNIVERSAL AVAILABILITY`

`GENERATION SUCCESS ≠ CINEMATIC CORRECTNESS`

`AGENT CONFIRMATION ≠ COMPLETE SECURITY`

`GOOGLE CLOUD SDK ≠ AUTHORIZATION`

`COURSE COMPLETION ≠ PRODUCTION AUTHORITY`

`SECONDARY GUIDE ≠ PRIMARY PRODUCT DOCUMENTATION`

## Decision

No new numbered project is justified. The material is absorbed primarily into **P97, P100, P113 and P21** as provider/capability/verification extensions.
