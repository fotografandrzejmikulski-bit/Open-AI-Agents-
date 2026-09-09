# Prompt Compiler: Constraint, Cognitive and Recursive Evaluation Architecture — 2026-09-09

## Status
`SOURCE_DERIVED → ENGINEERING_SYNTHESIS → PROPOSED`

The supplied "Generowanie Unikalnych Promptów Zmiennych" report is consolidated into the existing Prompt Laboratory / Prompt Compiler lineage. It is not treated as proof that prompts literally navigate or activate specific neuron pathways; those descriptions are retained as source framing/hypotheses.

## 1. Core formula

The report defines a useful engineering decomposition of a high-control prompt:

```text
STRUCTURE
+ CONSTRAINT
+ PERSONA
+ MENTAL MODEL
+ RECURSIVE REFINEMENT
= CONTROLLED PROMPT PROTOCOL
```

It argues that a prompt should be treated as a structured artifact rather than a single sentence. fileciteturn118file3L237-L267

## 2. Structural layer

The source covers zero-shot, few-shot, Chain-of-Thought, meta-prompting and constraint-based prompting. It emphasizes deliberate example selection, explicit output constraints and task-specific reasoning scaffolds. fileciteturn118file3L316-L367

Oulipo-inspired constraints such as lexical restrictions, semantic restrictions and syntactic rules are presented as ways to force a generator away from default formulations. They are especially useful for controlled creative generation and benchmark design. fileciteturn118file3L368-L401

## 3. Cognitive layer

The report separates persona from mental model. Example mental operators include First Principles, Inversion and Second-Order Thinking. Their engineering value is as explicit analysis policies, not as evidence that a model possesses a human mind. fileciteturn118file3L402-L448

## 4. Recursive evaluation layer

The proposed Refiner loop is:

```text
GENERATE
   ↓
CRITIQUE
   ↓
REFACTOR
   ↓
EVALUATE
   ↓
REPEAT / ACCEPT
```

The report also describes LADDER as a difficulty-escalation strategy and Tree-of-Explanations / Tree-of-Thoughts as branching-and-pruning patterns. fileciteturn118file3L466-L507

## 5. Agentic extension

The source predicts a transition from prompts that request outputs toward goal-oriented protocols that specify success criteria, resource constraints and permitted tools. It also proposes interactive preference learning and dynamic personalization. fileciteturn118file3L563-L592

Repository implementation should represent these as typed objects:

```text
PromptSpec
 ├─ persona
 ├─ context
 ├─ task
 ├─ constraints[]
 ├─ reasoning_policy
 ├─ tool_policy
 ├─ evaluator
 ├─ acceptance_criteria
 └─ revision_policy
```

## 6. Verification boundary

Claims about emergent abilities, latent-space behavior, or large accuracy changes must remain hypotheses unless independently reproduced. The prompt compiler should measure outcomes, not assume the proposed cognitive mechanism is literally true.

## 7. Integration

Primary targets are Projects 16, 20, 24, 27, 35 and 58. The contribution is a richer prompt grammar and evaluation protocol, not a new numbered project.
