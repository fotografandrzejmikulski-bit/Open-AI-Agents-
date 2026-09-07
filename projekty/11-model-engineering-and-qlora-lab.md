# Model Engineering & QLoRA Lab

## Objective
Establish a reproducible local pipeline for adapting open-weight models while preserving model quality, rollback capability and evaluation discipline.

## Pipeline

```text
Dataset design
   |
JSONL validation
   |
Train/validation split
   |
Base model + tokenizer lock
   |
4-bit quantization / QLoRA
   |
LoRA adapter training
   |
Offline evaluation
   |
Merge or adapter deployment
   |
GGUF / runtime packaging
   |
Ollama or local serving
```

The supplied QLoRA report describes a local workflow from JSONL data through Unsloth/QLoRA to GGUF and Ollama, with 4-bit NF4 quantization and frozen base weights plus low-rank adapters. It emphasizes that consumer hardware can be sufficient for selected 8B–14B-class workflows when memory is managed aggressively. fileciteturn206file9L2-L20 fileciteturn206file9L45-L62

## Maximum-practical improvement

- Maintain immutable base-model artifacts and adapter artifacts separately.
- Version dataset, tokenizer, hyperparameters and evaluation suite together.
- Reject dataset leakage and duplicate samples before training.
- Run holdout and regression benchmarks before promotion.
- Track catastrophic forgetting using general capability benchmarks.
- Prefer adapter-based rollback before weight merging.
- Record model card, provenance, licensing and safety scope.

## Evaluation matrix

Task quality, instruction following, domain accuracy, hallucination rate, refusal behavior, latency, memory footprint and energy cost.

## Promotion rule

No fine-tuned model becomes the default runtime model solely because training loss improved. Promotion requires benchmark evidence plus a regression report.

## Integration

The lab feeds the broader Agent Runtime through a `ModelProvider` abstraction. This keeps fine-tuning independent from orchestration and MCP/tool layers.