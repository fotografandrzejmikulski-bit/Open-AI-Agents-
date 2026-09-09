# Agentic Project Execution: HTA, WBS, SOP and Verification

## Source basis

Derived from the supplied materials on autonomous project management and autonomous task execution. The source material frames project execution as a transition from manual operation toward agent orchestration, with emphasis on task decomposition, structured inputs, external tools, feedback loops, MCP, multi-agent specialization and human approval.

## Core model

The supplied project-management material describes the frozen-weight inference view:

`Y = f(X, W_frozen)`

where the model parameters are fixed during inference and the quality of the outcome is strongly affected by the engineering of `X`: domain data, system instructions, task decomposition and environmental feedback.

For OmniCore this becomes a controlled compilation problem:

`Natural Intent -> HTA/WBS -> Typed Task Graph -> Capability Plan -> Deterministic Execution -> Verification -> State Commit`

## HTA as the decomposition boundary

Hierarchical Task Analysis (HTA) recursively decomposes a high-level objective into sub-goals and atomic operations. The supplied material explicitly requires input and output states for operations rather than merely a textual list of steps.

Each executable task should define:

- objective;
- preconditions;
- input data/resources;
- required capabilities;
- procedure/process;
- expected output;
- measurable success criteria;
- stopping rule;
- failure/rollback path;
- authorization requirements;
- postcondition verification.

The source describes this structure as a route from ambiguous business goals to deterministic action graphs/DAGs suitable for LLM planners.

## WBS contract

The supplied WBS guidance emphasizes:

- outcome-oriented work packages rather than vague actions;
- mutually exclusive work items;
- complete coverage of required work;
- hierarchical decomposition;
- dependency mapping;
- explicit acceptance criteria;
- parameterization of cost, schedule and risk where available.

For OmniCore, WBS is not a document-only artifact. It is a versioned execution graph that can be compiled into typed tasks and capability requests.

## Agent specialization

The materials favor specialized agents over a single general-purpose agent when instruction, tool or policy surfaces materially diverge. A practical decomposition is:

`Researcher -> Analyst -> Builder -> Verifier -> Release/Operator`

Specialization must not imply unrestricted delegation. Each agent receives the minimum capability set required for its assigned task.

## Deterministic execution boundary

The source distinguishes flexible agent reasoning from deterministic execution. A useful architectural rule is:

- **Agent:** proposes, decomposes, evaluates and selects among allowed options.
- **Workflow/runtime:** enforces sequence, state transitions, retries, timeouts and side-effect rules.
- **Capability broker:** decides whether the requested operation is authorized and available.
- **Verifier:** independently checks the resulting state.

Thus the model may decide *what should happen*, but it does not become the authority that decides whether a consequential side effect is permitted.

## MCP integration

The supplied materials treat MCP as an interoperability layer between agents and external tools. Tool contracts must therefore expose explicit input/output schemas and capability boundaries. MCP does not replace authorization, policy enforcement or verification.

## Feedback and consensus

The material describes feedback loops and, for critical phases, independent-agent voting/consensus. OmniCore should generalize this into a graded verification strategy:

- single verifier for low-risk deterministic transformations;
- independent second pass for elevated-risk tasks;
- multi-solver comparison when disagreement is informative;
- human approval for irreversible/high-impact operations;
- authoritative readback after execution.

Consensus is evidence, not authorization.

## Human-in-the-loop

The source explicitly places human approval at sensitive control points, including low-confidence and irreversible operations such as deletion or payment. OmniCore models this as a resumable state transition rather than an informal UI prompt:

`READY -> AWAITING_APPROVAL -> APPROVED/REJECTED -> EXECUTE -> VERIFY`

Approval must be bound to a concrete action, scope, actor, target and expiry.

## Security transformation

The supplied materials contain operational patterns for autonomous execution. These are retained as engineering knowledge but hardened through the existing OmniCore security model:

- model output never grants privileges;
- external data is untrusted;
- agent-to-agent delegation is capability-scoped;
- credentials remain outside prompts and client-side code;
- consequential actions require policy checks;
- generated plans are validated before execution;
- execution produces auditable state deltas;
- failed verification blocks promotion.

## New reusable invariant

`No task is executable until its preconditions, required capability, success criteria, stopping rule and postcondition are represented explicitly.`
