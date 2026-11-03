# Research Notes

This document captures current assumptions, owner decisions, and open questions. Update it as evidence changes.

## Owner decisions

- Endgame: pursue both abliteration and capability-oriented weight modification, eventually building a general-purpose weight manipulation framework.
- Initial model strategy: investigate both published weight-space edit reproduction and a small-model abliteration target; start with the clearest reproducible experiment.
- Opus workflow: start manually supervised and progressively automate after the method and evaluation harness are validated.
- API budget: research-first, with usage and estimated costs recorded and expensive runs surfaced before execution.
- Environment: Linux.
- Additional notes: none supplied.

## Abliteration versus weight-space programming

These terms should not be used interchangeably.

- **Abliteration** usually refers to methods that identify a direction or representation associated with refusal behaviour and modify model weights to reduce that behaviour.
- **Weight-space programming** is a broader approach in which a model reasons about parameter tensors and proposes direct edits to a neural network. The edit may target a specific behavioural bug or capability.

Both modify weights, but they differ in target, method, and evaluation. Abliteration is not automatically a general capability improvement.

## Reproduction before novelty

The first goal is to reproduce a published example from the original artifacts. This gives the project a known-good path through model loading, checkpoint copying, editing, evaluation, and reporting.

Before claiming reproduction, verify:
- Exact source checkpoint and revision.
- Exact edit artifact or code.
- Correct tensor mapping and shapes.
- Matching tokenizer and inference settings.
- Matching benchmark and scoring procedure.
- Whether the reported result depends on a particular prompt format or stopping condition.

## Staged Opus workflow

The initial external-model workflow is human-supervised:
1. Provide Opus 5.5 with scoped architecture metadata, experiment context, and relevant evaluation findings.
2. Ask for a falsifiable modification proposal and explicit expected effects.
3. Review the proposed code and tensor changes.
4. Execute in a constrained environment against a copied checkpoint.
5. Run the fixed evaluation suite and inspect regressions.
6. Record the outcome and cost before deciding on another iteration.

Automation should be introduced incrementally. Deterministic inspection, validation, evaluation, and logging are good early automation targets. Autonomous proposal/edit loops come later, once rollback and evaluation are dependable.

The project is research-first rather than strictly cost-minimizing. Still, record model, API, token usage, and estimated spend per experiment. Surface unusually expensive runs before starting them.

## Weight editing safety rails

Every edit runner should:
- Read the original checkpoint without modifying it.
- Write to a new candidate directory.
- Validate all tensor names and shapes.
- Reject NaN/Inf values.
- Report per-tensor and aggregate change magnitudes.
- Enforce a configurable maximum edit budget.
- Record a hash for the source and output artifacts.
- Require evaluation before a candidate is marked accepted.

Model-generated code should be reviewed and run in a constrained environment. Treat external model outputs as proposals, not trusted instructions.

## Evaluation pitfalls

- A benchmark can improve because a formatting or stopping bug was fixed, without new underlying knowledge being learned.
- Repeatedly testing on the same prompts can cause overfitting to the evaluation set.
- A single aggregate score can hide major regressions.
- Quantization can alter or erase an edit's effect.
- A before/after comparison is invalid if prompts, tokenizer, decoding settings, or scoring changed.
- A chart posted on social media is a lead, not a substitute for code and methodology.

## Open questions

1. Which released experiment is easiest to reproduce exactly with accessible artifacts?
2. Which small model has the best combination of architecture simplicity, checkpoint access, and evaluation support for abliteration?
3. Which refusal and general-capability evaluation sets should be included in the first abliteration run?
4. Which Linux distribution, Python version, NVIDIA driver, CUDA/PyTorch stack, and environment manager are installed?
5. What API interface will be used for Opus 5.5, and how should usage/cost be captured?
6. What disk budget is available for source checkpoints, candidate checkpoints, and evaluation artifacts?
