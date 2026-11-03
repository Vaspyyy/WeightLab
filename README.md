# WeightLab

**Weight-space experimentation for open-weight language models.**

WeightLab is a research project exploring practical, reproducible methods for modifying model weights and measuring the effects. The first milestone is refusal-behaviour modification (abliteration); the broader goal is a framework for controlled weight-space experiments, including frontier-model-proposed edits.

This repository starts as a research notebook and experiment harness, not a claim that arbitrary models can be made smarter by editing weights.

## Research tracks

- **Abliteration:** study refusal-related activations and weight modifications, then measure refusal changes alongside general-capability regressions.
- **Weight-space programming:** reproduce published edits where artifacts are available, then test model-proposed modifications under controlled evaluation.
- **Evaluation:** fixed baselines, held-out prompts, regression checks, reproducible configurations, and checkpoint provenance.
- **Hardware practicality:** prioritize experiments that can be prepared or evaluated on a consumer system with an 8 GB GPU and 64 GB system RAM.

## Principles

1. Preserve the untouched source checkpoint.
2. State a falsifiable hypothesis before each experiment.
3. Change one major variable at a time.
4. Separate training/editing precision from inference quantization.
5. Evaluate both target behaviour and general capabilities.
6. Keep prompts, configurations, scripts, logs, and diffs versioned.
7. Treat social-media claims as leads to investigate, not established results.
8. Never report a successful improvement without recording the evaluation method and baseline.

## Planned milestones

1. [x] Establish project scope and research tracks.
2. [ ] Record hardware, software, model, and API constraints.
3. [ ] Reproduce a published weight-space edit from its original artifacts.
4. [ ] Build a repeatable baseline/evaluation runner.
5. [ ] Run a first controlled abliteration experiment.
6. [ ] Add a model-proposed edit loop with strict evaluation and rollback.
7. [ ] Explore whether results generalize across model families.

## Documentation

- [Project plan](docs/PROJECT_PLAN.md)
- [Experiment log](docs/EXPERIMENT_LOG.md)
- [Research notes](docs/RESEARCH_NOTES.md)

## Current status

**Planning / setup.** No experiments have been run by this repository yet. Results and conclusions will be added only after reproducible tests.

## Initial hardware target

- CPU: AMD Ryzen 7 5800X
- GPU: NVIDIA GeForce RTX 3070, 8 GB VRAM
- RAM: 64 GB
- Preferred environment: Linux
- Current local baseline: LFM3 1.7B, Q4 quantization (kept separate from the first experimental target)

The first experimental model should be selected based on architecture support, availability of original weights and evaluation artifacts, and whether it fits the workflow. Do not assume a quantized GGUF is suitable for direct weight editing.
