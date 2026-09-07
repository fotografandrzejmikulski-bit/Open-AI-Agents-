# Cognitive Security & Adversarial Evaluation Platform

## Objective
Convert the supplied research on hidden directives, influence engineering, Chain-of-Attack, jailbreak robustness and GCG into a defensive evaluation platform for agentic systems.

## Threat model

```text
User / Document / Image / Tool Result
                 |
        Provenance + Classification
                 |
      Context / State Integrity Layer
                 |
     Policy + Instruction Hierarchy
                 |
        Agent / Tool Execution
                 |
      Runtime Verification + Audit
```

The Chain-of-Attack material characterizes multi-turn attacks as semantic and contextual, exploiting conversation history rather than one isolated prompt. fileciteturn195file7L44-L65 The GCG report describes a different class: algorithmically optimized adversarial suffixes that target model behavior rather than persuading it semantically. fileciteturn195file9L19-L32

The hidden-influence materials discuss covert commands and perceptual manipulation. For engineering purposes, the platform should treat such material as adversarial content to detect and measure, not as a recipe for covert persuasion. fileciteturn195file6L17-L36

## Defensive capabilities

### 1. Instruction provenance
Track where every instruction-like fragment originated: trusted developer policy, user request, retrieved document, tool result, memory, or generated model text.

### 2. Stateful attack detection
Evaluate the full conversation trajectory, not only the current turn. Flag semantic drift toward a protected objective, unexpected policy changes, or attempts to redefine authority.

### 3. Hidden-content inspection
Scan documents, metadata, markup, OCR-visible text and tool outputs for instruction-bearing payloads. Keep provenance attached after transformation.

### 4. Adversarial regression suite
Run deterministic test cases for role manipulation, instruction injection, multi-turn escalation, tool-result poisoning, long-context attacks, malformed schemas and adversarial suffixes.

### 5. Tool firewall
A tool call is authorized from the structured request and current policy state, never from natural-language content alone.

## Metrics

Attack success rate, false positive rate, protected-intent preservation, unauthorized tool-call rate, policy drift, time-to-detection, recovery success and user-visible friction.

## Safety property

No red-team test should require deploying an offensive payload against an external target. The evaluation harness must operate on local fixtures, synthetic environments and explicitly authorized test models.

## Architecture principle

`detection != blocking != authorization`: each is a separate control layer.