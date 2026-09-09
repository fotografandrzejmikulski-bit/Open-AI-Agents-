# Defensive Influence Literacy & Behavioral Security — 2026-09-09

## Status

`SOURCE_DERIVED → DEFENSIVE_ENGINEERING_SYNTHESIS → PROPOSED`

The supplied material describes covert influence concepts including embedded commands, presuppositions, nominalizations, extended quotations and recursive narrative loops. This artifact converts the material into a defensive literacy and detection model. It does not provide an operational recipe for covertly manipulating a person.

## 1. Core threat model

The source frames communication as operating at multiple levels: explicit content, assumptions and structural cues. It describes the intended manipulation pattern as occupying conscious attention with overt content while attempting to influence interpretation through hidden structure. fileciteturn74file9L7-L27

For defensive systems, the important abstraction is:

```text
MESSAGE
 ├── explicit proposition
 ├── presupposition
 ├── imperative / call-to-action
 ├── emotional framing
 ├── attribution / authority cue
 └── unresolved narrative dependency
```

## 2. Linguistic indicators

The supplied corpus identifies several classes of influence cues: embedded imperatives, nominalizations, presuppositions and commands attributed to a third party. fileciteturn74file9L31-L55

A defensive analyzer can flag these as **signals**, not proof of malicious intent. Context, speaker authority, user goals and alternative interpretations must remain visible.

## 3. Recursive influence detection

The material describes nested narrative loops and the Zeigarnik effect as mechanisms intended to maintain unresolved attention. fileciteturn74file9L59-L67

A defensive agent should therefore track:

```yaml
InfluenceSignal:
  cue_type:
  location:
  explicit_content:
  implied_assumption:
  requested_action:
  emotional_pressure:
  authority_claim:
  unresolved_dependency:
  confidence:
  alternative_interpretations: []
```

The presence of a cue is not equivalent to manipulation.

## 4. Human-agency invariant

For agentic systems, the critical invariant is that persuasive language must never silently become authorization. A system should distinguish:

`understanding → persuasion → user decision → authorization → execution`.

No linguistic pattern should bypass consent, policy or capability boundaries.

## 5. AI security applications

The model applies directly to prompt-injection and social-engineering defense. An input may contain a legitimate task plus hidden instructions attempting to alter the agent's priorities. The defensive pipeline is:

```text
INPUT
 → STRUCTURAL PARSE
 → INSTRUCTION / DATA SEPARATION
 → AUTHORITY CHECK
 → POLICY CHECK
 → USER-INTENT CHECK
 → TOOL AUTHORIZATION
 → EXECUTION ONLY AFTER VALIDATION
```

This complements the repository's existing cognitive-security and runtime-assurance layers.

## 6. Evaluation

Adversarial tests should include:

- hidden imperative language;
- presupposition traps;
- authority laundering through quotations;
- escalating emotional pressure;
- recursive unfinished tasks;
- contradictory instructions embedded in otherwise valid documents;
- prompt injection disguised as metadata or quoted material.

Success means the system preserves user agency and authorization boundaries while explaining uncertainty rather than silently obeying the strongest linguistic cue.

## 7. Portfolio integration

This material strengthens Projects 26/49/54/60/72 and the repository's broader human-agency/security lineage. It is a defensive capability layer, not a covert-influence execution module.

## Final principle

`Language can influence interpretation; it must never substitute for authorization.`
