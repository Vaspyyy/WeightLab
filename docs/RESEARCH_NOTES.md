# Research Notes

This document captures current assumptions and open questions. Update it as evidence changes.

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
2. Which small model has the best combination of architecture simplicity, checkpoint access, and evaluation support?
3. Which refusal and general-capability evaluation sets should be included in the first abliteration run?
4. How should the project invoke Opus 5.5: manual copy/paste initially, or a programmatic API harness once the experimental protocol is stable?
5. What is the acceptable API spend per iteration?
6. Which Linux distribution and Python/CUDA environment will be used for the actual run?
