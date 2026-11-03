# WeightLab Project Plan

## Agreed project decisions

These decisions were supplied by the project owner and guide the initial implementation.

| Decision | Selection | Implementation consequence |
|---|---|---|
| Endgame | **C: Both** | Abliteration and capability-oriented weight modification are both core tracks; long-term direction is a general-purpose weight manipulation research framework. |
| Initial model strategy | **C: Both** | Investigate published weight-space edit reproduction and a small-model abliteration target. Start with whichever has the cleanest reproducible setup, while keeping both tracks active. |
| Opus workflow | **C: Staged automation** | Begin manually supervised, then automate proposal and evaluation after the protocol is validated. |
| API budget | **C: Research-first** | Useful experiments take priority over minimizing spend. Still record token usage and cost estimates, and surface expensive runs before execution. |
| Environment | **Linux** | Linux is the target development environment. Distribution and exact Python/CUDA versions remain to be confirmed. |
| Additional notes | None | No further constraints supplied. |

## Mission

Build a reproducible research framework for modifying open-weight language models and testing what the modifications actually change.

The project has two initial experimental pillars:
1. Investigate refusal-behaviour modification (commonly called abliteration).
2. Investigate weight-space programming, where a capable external model proposes targeted changes to a model's weights.

These are separate techniques and should have separate experiment tracks. A successful abliteration result does not establish general capability improvement, and a successful narrow weight-space edit does not establish recursive self-improvement.

The longer-term goal is to unify these experiments under a general-purpose framework for controlled weight manipulation, evaluation, and checkpoint management.

## Research questions

1. Can we reproduce a published weight-space edit using the authors' original artifacts and evaluation setup?
2. How much does a controlled abliteration edit change refusal behaviour?
3. What general-capability regressions, if any, accompany that change?
4. Can an external coding/reasoning model propose edits that survive a fixed evaluation suite?
5. Can we make this workflow practical on a consumer machine with 8 GB VRAM and 64 GB system RAM?
6. Which parts of the workflow can be automated reliably without compromising reproducibility or experimental control?

## Tracks and priorities

### P0: Reproducible evaluation
- Record model identifier, revision, tokenizer, dtype, quantization, runtime, prompts, decoding settings, and random seeds where applicable.
- Keep a frozen baseline and held-out evaluation set.
- Report individual metrics, not only a single aggregate score.
- Save output samples and exact configuration for every run.

### P0: Published weight-space edit reproduction
- Start from the original model checkpoint and original released edit artifacts.
- Verify source model identity and tensor shapes before applying changes.
- Apply edits to a copy of the checkpoint.
- Compare baseline and edited models under matching inference/evaluation settings.
- Do not describe a reproduction as exact unless the original setup is matched closely enough to justify that wording.

### P0: Abliteration study
- Choose an architecture with well-supported loading and activation extraction.
- Establish baseline refusal and general-capability behaviour.
- Record the exact prompt sets and activation-extraction procedure.
- Apply one documented modification at a time.
- Evaluate refusal reduction and collateral changes separately.
- Keep the original checkpoint immutable.

### P1: Model-proposed weight editing
- Initially, use a manually supervised workflow with Opus 5.5 as the proposed external reasoning/editor model.
- Give the model architecture metadata, clearly scoped task information, and evaluation findings rather than unrestricted access to the machine.
- Require proposals to state a hypothesis, affected tensors, expected effect, risks, and a rollback plan.
- Execute proposed edits in a constrained Python process.
- Reject malformed, non-finite, or out-of-budget modifications.
- Run evaluation before promoting any candidate checkpoint.

### P1: Progressive automation
- First automate deterministic operations: checkpoint inspection, validation, evaluation, result comparison, and artifact logging.
- Next automate bounded proposal/evaluation cycles with human approval gates.
- Consider more autonomous iteration only after the harness demonstrates reliable evaluation and rollback.
- Record external-model token usage and cost estimates. Research is prioritized over strict cost minimization, but expensive runs should be visible before they are launched.

### P1: Generalization
- Repeat promising experiments on another model or task.
- Use held-out prompts to reduce benchmark overfitting.
- Track whether gains persist across seeds, prompt styles, and evaluation formats.

## Initial model selection

The owner selected a dual-track strategy: investigate both a published weight-space programming reproduction and a small-model abliteration experiment. The first runnable experiment should be whichever has the clearest source artifacts, architecture support, and evaluation procedure. Do not abandon the other track; keep its preparation moving in parallel where practical.

A published Qwen experiment may be the easiest reproduction target if its original checkpoint and exact edit artifacts are available. However, verify its architecture rather than assuming it is a conventional dense transformer. Architecture complexity is a reason to defer a model, not to silently substitute a different one.

For the abliteration track, choose a small model with reliable activation extraction and checkpoint tooling. Record why it was selected before running edits.

LFM3 1.7B Q4 is the user's current fast local model and should remain untouched initially. Its hybrid architecture and quantized format make it a poor first target for generic tensor-editing experiments.

## Hardware and memory strategy

Target system:
- Ryzen 7 5800X
- RTX 3070 8 GB VRAM
- 64 GB RAM
- Linux

Still to confirm:
- Linux distribution and kernel.
- NVIDIA driver and CUDA runtime/toolkit.
- Python version and environment manager.
- PyTorch build and supported CUDA version.
- Available disk space for source and candidate checkpoints.

Plan around the distinction between:
- **Editing:** usually best performed on original floating-point checkpoint tensors, with CPU RAM as an option.
- **Evaluation:** use GPU inference when the model and runtime fit; use CPU or partial offload where necessary.
- **Deployment:** quantize a validated candidate separately and measure the quantized version again.

Never assume an edit made to full-precision weights will retain the same effect after quantization. Never treat direct edits to a quantized GGUF as the default workflow.

## Experiment lifecycle

1. **Question:** define one measurable target behaviour.
2. **Baseline:** run the untouched model and save results.
3. **Hypothesis:** state what the edit is expected to change and what could regress.
4. **Edit:** apply a bounded, versioned change to a copy.
5. **Validation:** check tensor names, shapes, dtypes, finite values, and change magnitude.
6. **Evaluation:** run the same suite on baseline and candidate.
7. **Decision:** accept, reject, or mark inconclusive.
8. **Record:** save configuration, code revision, logs, outputs, and checkpoint hashes.

## Acceptance criteria

A candidate is not considered improved merely because it performs better on the target prompts. It must also be checked for regressions on general instruction following, ordinary reasoning, formatting, and language modelling where suitable metrics are available.

For abliteration, success means the target refusal behaviour changed as intended while collateral regressions remain measured and acceptable for the stated use case. It does not mean the model became generally more capable.

For weight-space programming, success means a predefined held-out evaluation improves against the baseline, with enough repeated evidence to rule out obvious prompt or measurement artefacts.

## Out of scope for the first milestone

- Training a model from scratch.
- Building a large autonomous agent platform.
- Claiming recursive self-improvement from one successful weight edit.
- Editing the only copy of a model checkpoint.
- Adding a complex UI before the CLI experiment loop works.
