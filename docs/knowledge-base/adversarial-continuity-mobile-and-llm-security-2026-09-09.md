# Adversarial Continuity — Mobile Surveillance, Jailbreak and Chain-of-Attack Security

## Source corpus
This note consolidates the supplied mobile-stealth/spyware analysis, the LLM Chain-of-Attack report, and related jailbreak material already present in the portfolio. Offensive construction details are deliberately transformed into defensive architecture, detection and evaluation requirements.

## Threat model
The sources describe multi-stage compromise, exploit chaining, payload/C2 stages, indirect prompt injection, multilingual/encoding bypasses and context-dependent attacks. Their common property is **stateful progression**: a harmless-looking step can become dangerous when combined with earlier context or compromised state.

## Defensive continuity model
A security decision must evaluate:
- current input;
- interaction trajectory;
- persistent memory/state;
- tool history;
- capability requests;
- external content provenance;
- observed environment changes.

A stateless input/output filter is insufficient for these attack classes.

## Mobile-security translation
The supplied mobile analysis emphasizes sandboxing, code signing, ASLR/PAC, SELinux, Verified Boot and foreground/background constraints. These become **defensive trust-boundary test cases** for the agent platform:

```text
SIGNED BASELINE
→ SANDBOX
→ LEAST PRIVILEGE
→ MEMORY / IPC ISOLATION
→ TELEMETRY
→ TAMPER DETECTION
→ REVOCATION / ROLLBACK
```

No capability should depend on an assumption that a client application or device is inherently trustworthy.

## Chain-of-Attack detector
Represent an interaction as a temporal graph:

```yaml
AttackTrajectory:
  session_id:
  nodes: [intent, input, memory_write, tool_call, output, state_change]
  edges: [depends_on, conditions, escalates, contradicts]
  risk_features:
  provenance:
  detector_versions:
```

Detection signals include semantic drift, privilege escalation, repeated boundary probing, contradiction between stated and observed objectives, hidden instructions in retrieved content, and unusual capability sequences.

## Memory poisoning
Durable memory is a security boundary. Writes require typed schema validation, provenance, source confidence and policy checks. High-impact claims need independent corroboration before becoming durable state.

## Multilingual / encoded content
Normalize Unicode and encoding, preserve the raw artifact, produce a canonical analysis representation, and compare semantic intent across transformations. A normalization result must not be allowed to execute as an instruction automatically.

## Multimodal injection
Images, audio, OCR, metadata and tool outputs are all untrusted inputs. The detector tracks cross-modal instruction agreement and conflicts rather than assuming one modality is authoritative.

## Independent action/state verification
For consequential tasks, authorization and success must be determined from typed capability requests and authoritative state rather than from model explanations or CoT.

## Evaluation matrix
- single-turn jailbreak regression;
- multi-turn Chain-of-Attack detection;
- indirect prompt injection;
- memory poisoning;
- multilingual/encoding transformation;
- multimodal injection;
- tool-result injection;
- monitor-awareness / evaluation-aware behavior;
- mobile sandbox escape simulation;
- revocation under active model cooperation failure.

## Safety boundary
The sources' exploit development, covert surveillance and evasion techniques are retained only as threat categories and defensive test requirements. This knowledge base does not provide deployable spyware, zero-click exploit chains, persistence instructions or covert behavioral-control implementations.
