# Frontiers of Knowledge — Unresolved Problems Across Science & Humanities

## Status
`SOURCE_DERIVED → KNOWLEDGE MAP → RESEARCH INPUT`

The two supplied encyclopedia files substantially overlap. They are consolidated here into one research map rather than stored as duplicate knowledge.

## 1. Fundamental physics and cosmology

The corpus highlights quantum gravity, the incompatibility between general relativity and quantum mechanics, dark matter, dark energy, the cosmological-constant problem, proton stability, neutrino mass, baryon asymmetry, fast radio bursts, Planet Nine and the Fermi paradox. The source explicitly presents competing quantum-gravity paradigms as lacking definitive empirical confirmation. fileciteturn80file8L24-L35 fileciteturn80file8L37-L53

## 2. Mathematics and theoretical computer science

The corpus identifies unresolved Clay Millennium problems and computational frontiers including the Riemann Hypothesis, P vs NP and Navier–Stokes regularity. fileciteturn82file3L154-L179

Engineering rule:

`OPEN PROBLEM ≠ AVAILABLE SOLUTION`

A research system should preserve the distinction between a recognized open problem, a conjecture, a proposed approach, a computational experiment and a proof.

## 3. Life, biology and consciousness

The source map includes abiogenesis, the RNA-world problem, homochirality, the Cambrian explosion, virus origins, blood-group evolution, the hard problem of consciousness and physical memory/engram questions. fileciteturn80file9L41-L70

These are heterogeneous questions. They should not be collapsed into a single “consciousness” or “life” theory; each requires domain-specific definitions and evidence.

## 4. Research frontier representation

The reusable architecture is:

```yaml
ResearchProblem:
  domain:
  question:
  known_constraints:
  competing_hypotheses:
  evidence_for:
  evidence_against:
  open_variables:
  falsification_tests:
  computational_tests:
  status: open|partially_resolved|candidate_solution|resolved
  last_verified:
```

## 5. Research-agent integration

The knowledge frontier becomes useful when connected to an evidence graph and experiment registry:

```text
OPEN QUESTION
   ↓
LITERATURE / DATA
   ↓
HYPOTHESES
   ↓
FORMAL MODEL
   ↓
SIMULATION / EXPERIMENT
   ↓
COUNTEREXAMPLE SEARCH
   ↓
REPRODUCTION
   ↓
STATUS UPDATE
```

The system must never infer resolution merely because a simulation produces an attractive result.

## 6. Portfolio integration

This module strengthens existing scientific-verification, epistemic-control and research-agent capabilities. It is a knowledge map, not a new numbered project.
