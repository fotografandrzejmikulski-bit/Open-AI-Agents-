# Local QLoRA Fine-Tuning & Model Deployment — 2026-09-09

## Status
`SOURCE_DERIVED → ENGINEERING_SYNTHESIS → PROPOSED`

The two supplied QLoRA PDFs are overlapping versions of the same technical report. Their common material is consolidated here instead of duplicated.

## 1. End-to-end pipeline

The supplied report defines a practical local workflow:

```text
SOURCE / DOMAIN DATA
      ↓
DATASET ENGINEERING (JSONL)
      ↓
BASE MODEL SELECTION
      ↓
4-BIT QUANTIZATION / QLoRA
      ↓
LoRA ADAPTER TRAINING
      ↓
EVALUATION / OVERFIT CHECK
      ↓
MERGE OR ADAPTER PACKAGING
      ↓
GGUF CONVERSION
      ↓
OLLAMA DEPLOYMENT
      ↓
INFERENCE EVALUATION
      ↓
ROLLBACK / ITERATE
```

The source explicitly covers JSONL engineering, Unsloth/hyperparameter optimization, GGUF compilation and Ollama deployment. fileciteturn102file2L949-L967

## 2. Why QLoRA

The report contrasts full fine-tuning with parameter-efficient adaptation. LoRA freezes the base weights and learns low-rank matrices `A` and `B`, with `ΔW = BA`. QLoRA adds 4-bit quantization of the frozen base model, using NF4 and double quantization. fileciteturn103file17L702-L714

The source presents this as a way to move model adaptation toward consumer hardware. It gives approximate memory figures and hardware examples; these are **source-derived estimates**, not universal capacity guarantees. fileciteturn103file17L715-L722

## 3. Unsloth acceleration layer

The report attributes substantial efficiency gains to Unsloth's specialized LoRA/MLP backpropagation kernels implemented with Triton. It reports 2–5× training-speed improvement in its cited comparison and also describes large VRAM reductions. These performance figures must be independently benchmarked for the actual model, sequence length, batch configuration, GPU and software versions before being used as engineering guarantees. fileciteturn103file17L723-L731

## 4. Dataset doctrine

The source argues that relatively small, well-designed datasets can imprint domain knowledge or style while limiting catastrophic forgetting. Its example is on the order of 500 samples. The repository treats this as a **hypothesis/configuration heuristic**, not a universal rule: dataset size, diversity, quality, duplication, formatting, target behavior and evaluation design must determine the actual result. fileciteturn102file2L960-L967

Recommended contract:

```yaml
Dataset:
  source_provenance:
  license:
  task_definition:
  train:
  validation:
  holdout:
  contamination_checks:
  deduplication:
  quality_rules:
  expected_behavior:
```

## 5. Evaluation and rollback

A production fine-tuning pipeline must compare the adapted model against the base model on both target capability and regression suites. The key acceptance dimensions are:

- target-task performance;
- general capability retention;
- hallucination/error profile;
- instruction following;
- safety/security regression;
- latency and memory;
- reproducibility;
- rollback to the base model or prior adapter.

The supplied corpus strongly supports the broader repository doctrine that generated/model artifacts remain untrusted until independently evaluated.

## 6. Integration with the portfolio

Primary mapping:

- **Project 11** — Model Engineering and QLoRA Lab;
- **Project 10** — Sovereign AI Local-First Stack;
- **Project 37/38** — Sovereign Edge AI runtime;
- **Project 17** — Adaptive Model Router;
- **Project 58** — Monitorability-Aware Oversight.

This corpus strengthens Project 11 rather than creating another fine-tuning project.

## 7. Engineering boundary

The source cites multiple external guides and documentation for Unsloth, LoRA hyperparameters, GGUF and Ollama. The repository records their concepts but does not treat source-reported performance or hardware limits as verified until reproduced in the target environment. fileciteturn103file2L157-L188
