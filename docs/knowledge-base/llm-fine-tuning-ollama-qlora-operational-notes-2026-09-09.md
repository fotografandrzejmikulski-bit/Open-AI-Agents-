# LLM Fine-Tuning / QLoRA / Ollama — Operational Notes — 2026-09-09

## Status
`SOURCE_DERIVED → ENGINEERING_SYNTHESIS`

The newly supplied material duplicates the existing QLoRA lineage. No duplicate project is created. The reusable additions are deployment and failure-mode notes.

## 1. Ollama deployment contract

The supplied fine-tuning material shows an Ollama Modelfile with explicit chat-template delimiters and stop parameters. It warns that missing stop tokens can cause the model to continue generating another conversational turn, producing malformed output or apparent hallucination. fileciteturn117file8L401-L422

## 2. Small-dataset overfitting

The source identifies a particular risk when fine-tuning on approximately 500 examples: training loss can collapse while the model memorizes examples instead of generalizing. It proposes NEFTune as one mitigation and recommends checking generalization on unseen prompts. fileciteturn117file8L423-L432

## 3. Generation loops

The supplied notes identify missing EOS handling and incomplete stop-token configuration as common causes of infinite or repeated generation. fileciteturn117file8L433-L439

## 4. Repository integration

These controls belong in Project 11 and should become explicit acceptance tests:

- template correctness;
- EOS correctness;
- stop-sequence correctness;
- held-out generalization;
- memorization detection;
- regression tests after model export;
- deterministic model/config metadata;
- rollback to the prior adapter/model artifact.

## 5. Boundary

The source contains implementation-specific claims about performance and hardware. Those remain source-derived until reproduced on the actual target environment.
