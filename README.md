# WeightLab

**Weight-space experimentation for open-weight language models.**

WeightLab is a research project exploring practical, reproducible methods for modifying model weights and measuring the effects. The first milestones cover refusal-behaviour modification (abliteration) and reproduction of published weight-space programming experiments. The longer-term goal is a general-purpose framework for controlled weight-space experiments, including frontier-model-proposed edits.

This repository starts as a research notebook and experiment harness, not a claim that arbitrary models can be made smarter by editing weights.

## Agreed project direction

The project owner selected the following direction:

- **Endgame:** pursue both abliteration and broader model improvement through weight modifications, eventually building a general-purpose weight manipulation research framework.
- **Initial model strategy:** investigate both published weight-space programming reproduction and a small-model abliteration experiment. Choose the first runnable target based on reproducibility, architecture support, and evaluation quality.
- **Opus workflow:** begin with manually supervised proposals and execution, then progressively automate the workflow after the method and evaluation harness are validated.
- **API budget:** research-first. API spending is secondary to useful experiments, but usage and estimated costs should be recorded, especially before expensive runs.
- **Environment:** Linux.
- **Additional constraints or notes:** none supplied.

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
9. Begin with human-supervised experiments; automate only after the process is understood and validated.
10. Record external-model usage and cost for each Opus-assisted experiment.

## Planned milestones

1. [x] Establish project scope and research tracks.
2. [x] Record initial project decisions and target environment (Linux).
3. [ ] Record exact Linux distribution, Python/CUDA stack, and API access details.
4. [ ] Select and reproduce a published weight-space edit from its original artifacts.
5. [ ] Select and run a first controlled abliteration experiment.
6. [ ] Build a repeatable baseline/evaluation runner shared by both tracks.
7. [ ] Add a manually supervised Opus-proposed edit workflow.
8. [ ] Progressively automate proposal, validation, evaluation, and rollback.
9. [ ] Explore whether results generalize across model families.

## Documentation

- [Project plan](docs/PROJECT_PLAN.md)
- [Experiment log](docs/EXPERIMENT_LOG.md)
- [Research notes](docs/RESEARCH_NOTES.md)

## Current status

**Planning / setup.** No model experiments have been run by this repository yet. Results and conclusions will be added only after reproducible tests.

## Initial hardware target

- CPU: AMD Ryzen 7 5800X
- GPU: NVIDIA GeForce RTX 3070, 8 GB VRAM
- RAM: 64 GB
- Environment: Linux (distribution and exact software stack to be confirmed)
- Current local baseline: LFM3 1.7B, Q4 quantization (kept separate from the first experimental target)

The first experimental model should be selected based on architecture support, availability of original weights and evaluation artifacts, and whether it fits the workflow. Do not assume a quantized GGUF is suitable for direct weight editing.
