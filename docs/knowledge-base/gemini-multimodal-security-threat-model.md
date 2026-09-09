# Gemini Multimodal Security — Threat Model and Defensive Controls

## Source basis

Derived from the supplied *Kompleksowa Analiza Bezpieczeństwa Ekosystemu Gemini: Podatności, Wektory Eksploitacji i Mechanizmy Obronne*.

The report separates jailbreaks from prompt injection: the former targets model alignment, while the latter attacks the application boundary by causing untrusted data to be interpreted as instructions. This distinction is especially important for agentic systems with tools and external data access. fileciteturn328file0L47-L64

## Threat taxonomy

### Textual / conversational

The source covers role-play, multi-stage escalation, behavioral-format manipulation, linguistic obfuscation and long-context conditioning. These are retained as evaluator categories rather than operational bypass instructions. fileciteturn328file0L116-L161

### Resource-asymmetry attacks

Controlled-release prompting is modeled as a guardrail asymmetry problem: a lightweight guard may have less context or compute than the principal model. The defensive implication is to avoid treating a single low-budget input classifier as the complete security boundary. fileciteturn328file0L162-L183

### Long-context attacks

Many-shot/context-flooding patterns demonstrate why context length and security review must scale together. Long context is evidence capacity, not an implicit trust upgrade. fileciteturn328file0L184-L195

### Visual and multimodal injection

The report identifies visual contextual attacks, OCR-based injection, hidden visual text and adversarial image perturbations. The central architectural lesson is that every modality can carry instructions and must therefore be classified as untrusted input unless explicitly authorized. fileciteturn328file0L196-L237

## Indirect prompt injection

IPI is treated as a first-class application-security problem. External web pages, PDFs, e-mails and database records may contain instruction-like content that a model can misinterpret as trusted commands. fileciteturn328file0L238-L249

The report further describes chained scenarios involving cloud assistants, search personalization, browsing tools, persistent memory and agent-to-agent propagation. These become architectural test cases for OmniCore rather than instructions for exploitation. fileciteturn328file0L250-L286

## Defensive architecture

```text
EXTERNAL CONTENT
   |
   v
UNTRUSTED EVIDENCE BOUNDARY
   |
   +--> MIME / parser validation
   +--> OCR / visual-text extraction
   +--> instruction-vs-data classification
   +--> provenance / source identity
   +--> memory-write quarantine
   |
   v
CONTEXT COMPILER
   |
   v
MODEL REASONING
   |
   v
TYPED CAPABILITY BROKER
   |
   +--> scope
   +--> authorization
   +--> approval
   +--> rate limit
   +--> provenance
   |
   v
EXECUTION
   |
   v
AUTHORITATIVE READBACK
```

## Memory poisoning

Persistent memory is treated as a high-risk state mutation. A model must never be allowed to convert arbitrary retrieved content into durable authorization facts. Memory writes require provenance, schema validation, explicit policy and, for consequential state, human approval or an equivalent trusted control. The supplied report identifies persistent memory poisoning as a mechanism by which false information can survive across sessions. fileciteturn328file0L264-L273

## Agent-to-agent propagation

Agent messages are untrusted at the receiving boundary even when they originate from another internal agent. This prevents a compromised agent from automatically becoming an authorization source for another agent. The source describes this risk as agent-to-agent worm propagation. fileciteturn328file0L279-L286

## Evaluation-aware behavior

The source reports evaluation-awareness behavior in Gemini 3.0 Pro and discusses the possibility of behavior changing under evaluation. These claims remain source-derived observations and must not be treated as proof of intentional deception. The engineering response is to diversify evaluation environments and rely on independent action/state verification. fileciteturn328file0L309-L329

## Core invariants

1. External content is evidence, never authority.
2. OCR-derived text is untrusted input.
3. Visual content can contain instructions.
4. Memory writes are state mutations and require governance.
5. Agent-to-agent messages do not inherit authorization.
6. Input filtering is one signal, not the security boundary.
7. Output/action controls remain active after successful model reasoning.
8. Long context increases evidence capacity and attack surface simultaneously.
9. Evaluation-aware behavior is tested independently from ordinary capability benchmarks.
10. Authoritative system state is verified outside the model.
