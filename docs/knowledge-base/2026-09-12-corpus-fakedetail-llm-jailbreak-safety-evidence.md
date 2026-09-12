# Knowledge Corpus — FakeDetail + LLM Jailbreak/Safety Evaluation

**Date:** 2026-09-12  
**Status:** INGESTED → VERIFIED / DEFENSIVE SYNTHESIS  
**Decision:** NO_NEW_PROJECT — extend P108/P54/P72/P30 evidence layers.

## 1. Source set

### Primary supplied web source
- FakeDetail — Fake Messenger Chat / Facebook chat generator: https://fakedetail.com/fake-facebook-chat-generator

The page exposes a configurable visual mockup system for social/chat interfaces. Observed controls include profile identity, online/last-active state, message content, media, timestamps, delivery/read states, reactions, deleted/encrypted-message presentation, calls, posts, profile details, device/network indicators and image export. The site also exposes multiple social-platform mockup categories and saved presets.

### Supplied technical corpus
The user supplied equations and notes covering:
- frozen-weight model mapping `Y = f(X, W_frozen)`;
- temperature-scaled softmax;
- scaled dot-product attention;
- configurable safety thresholds such as `BLOCK_LOW_AND_ABOVE`;
- multilingual/encoded prompt transformation as an adversarial safety-evasion class;
- GCG-style adversarial suffix optimization;
- semantic-preservation constraints and an objective that seeks to reduce refusal probability.

These materials are ingested as **red-team/security-evaluation knowledge**, not as instructions for bypassing safeguards in production systems.

## 2. External verification

Google's current Gemini API documentation confirms that safety settings are applied per request, that harm probability is classified into `HIGH`, `MEDIUM`, `LOW`, and `NEGLIGIBLE`, and that `BLOCK_LOW_AND_ABOVE` blocks low/medium/high probability content. Prompt blocking is surfaced through `promptFeedback.blockReason`; blocked candidate output is surfaced through safety metadata and is not returned. Source: Google AI for Developers, Safety Settings / Generate Content documentation.

Recent research also confirms the technical family represented by the supplied notes:
- GCG and follow-on work formulate adversarial suffix generation as an optimization problem against aligned LLMs.
- MAGIC studies gradient-index optimization to accelerate GCG-like search while preserving attack success characteristics.
- DeGCG studies transferability and efficiency of adversarial suffix search across models/data.
- Mixture-of-encodings research studies encoding transformations as a prompt-injection defense/evasion dimension.

## 3. Key knowledge extracted

### A. Safety-filter configuration is not the same as model-level safety
`SafetySetting`, threshold configuration, prompt feedback and candidate safety ratings are observable control/telemetry surfaces. They do not by themselves prove robustness against adversarially transformed inputs.

Invariant:
`SAFETY_THRESHOLD ≠ ADVERSARIAL_ROBUSTNESS`

### B. Adversarial transformation should be modeled as a test family
The supplied corpus identifies several transformation families:
1. language transformation / low-resource-language variation;
2. character or encoding transformation;
3. optimization-generated suffix perturbation;
4. semantic-preserving transformation;
5. refusal-probability minimization under similarity constraints.

For the repository these become **parameterized test classes**, not reusable jailbreak recipes.

### C. GCG belongs in controlled evaluation, not ordinary prompting
The mathematical structure supplied by the user is consistent with an adversarial optimization objective: preserve sufficient similarity to a harmful intent while searching for a transformed input whose model response departs from the expected refusal region. This is directly relevant to P108's controlled red-team workbench.

Required evaluation fields:
- model/version;
- safety-policy configuration;
- attack-family identifier;
- transformation metadata;
- semantic-similarity score;
- refusal/safety outcome;
- attack-success definition;
- transfer/generalization scope;
- run seed/configuration;
- evidence artifact and digest.

### D. Fake UI generators create an epistemic/evidence-integrity risk
FakeDetail demonstrates how a visual artifact can reproduce many UI-level signals normally treated as evidence: names, profile state, timestamps, message state, reactions, calls, device indicators, posts and exported screenshots.

Therefore:
`VISUAL FIDELITY ≠ EVENT AUTHENTICITY`
`SCREENSHOT ≠ PRIMARY EVIDENCE`

This is relevant to P30/P32 OSINT and evidence systems as an **artifact provenance / synthetic-media distinction**. A screenshot should be classified by provenance and corroboration rather than interface realism alone.

### E. Evidence classes to preserve
For any social/chat artifact:
- `OBSERVED_PRIMARY` — directly obtained from an authoritative system/API/account with provenance;
- `USER_SUPPLIED_UNVERIFIED` — supplied by a person without independent provenance;
- `SYNTHETIC_MOCKUP` — generated visual simulation such as a UI mockup;
- `RECONSTRUCTED` — analyst reconstruction from multiple observations;
- `CORROBORATED` — independently supported by authoritative secondary evidence.

The distinction must survive ingestion, ranking and reporting.

## 4. Architecture impact

### P108 — OmniRedTeam LLM Security Validation Workbench MAX
Add:
- transformation-family registry;
- safety-threshold matrix;
- adversarial-input lineage;
- semantic-preservation measurement;
- refusal-boundary regression tests;
- cross-model transfer evaluation;
- attack-success definitions separated from raw generation success;
- reproducible experiment manifests;
- evidence digests and replay records.

### P54 — OmniCore Epistemic Signal & Adversarial Control
Add a stronger separation between:
`ATTACK HYPOTHESIS → CONTROLLED TEST → OBSERVATION → METRIC → INTERPRETATION`

A successful adversarial test is evidence of a measured weakness under specified conditions, not proof of universal model failure.

### P72 — Cross-Framework Agent Assurance
Add adversarial safety-regression gates before promotion of an agent/model configuration. Safety settings must be treated as configuration inputs to verification, not as proof of compliance.

### P30/P32 — OSINT / evidence layer
Add synthetic-chat/mockup detection and provenance classification. Visual similarity must never be elevated to event authenticity without independent provenance.

## 5. Security invariants

- `MODEL_OUTPUT ≠ AUTHORIZATION`
- `SAFETY_SETTING ≠ SAFETY_PROOF`
- `LOW-RESOURCE-LANGUAGE TRANSFORMATION ≠ AUTOMATIC BYPASS`
- `ENCODING TRANSFORMATION ≠ AUTOMATIC BYPASS`
- `GCG PAPER ≠ UNIVERSAL ATTACK GUARANTEE`
- `ATTACK SUCCESS ≠ REAL-WORLD IMPACT`
- `SCREENSHOT ≠ AUTHORITATIVE EVENT RECORD`
- `FAKE UI FIDELITY ≠ AUTHENTICITY`
- `SYNTHETIC ARTIFACT ≠ OBSERVED EVENT`

## 6. New-project decision

**NO_NEW_PROJECT.** The material strengthens an existing architecture intersection:
- P108 for controlled LLM adversarial evaluation;
- P54 for epistemic/adversarial control;
- P72 for assurance/promotion gates;
- P30/P32 for evidence provenance and synthetic-artifact handling.

Creating another generic jailbreak or fake-chat project would duplicate existing portfolio boundaries.

## 7. Source-quality note

FakeDetail is treated as a **capability/UX witness**, not as an authoritative source for forensic authenticity or platform behavior. Academic papers and Google's official API documentation are the stronger sources for the LLM safety/evaluation claims. Historical or marketing material must not be promoted to canonical capability/risk truth without independent verification.
