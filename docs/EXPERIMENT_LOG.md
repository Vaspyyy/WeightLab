# Experiment Log

This file records completed and attempted experiments. Planned work belongs in [PROJECT_PLAN.md](PROJECT_PLAN.md).

## Status legend

- **PLANNED:** not run yet
- **RUNNING:** currently executing
- **COMPLETE:** results recorded
- **FAILED:** execution failed for a technical reason
- **INCONCLUSIVE:** execution completed, but the evidence does not answer the question

## DEC-001: Initial project direction

- **Status:** RECORDED
- **Date:** 2026-11-03
- **Endgame:** both abliteration and capability-oriented weight modification, eventually a general-purpose weight manipulation framework.
- **Initial model strategy:** investigate published weight-space programming reproduction and small-model abliteration; start with the cleanest reproducible setup.
- **Opus workflow:** begin manually supervised, then progressively automate.
- **API budget:** research-first; record usage/cost and surface expensive runs before execution.
- **Environment:** Linux.
- **Additional notes:** none supplied.
- **Model changes:** none.
- **Evaluation:** none.

## EXP-000: Repository initialization

- **Status:** COMPLETE
- **Purpose:** establish the project and documentation structure.
- **Result:** documentation initialized.
- **Model changes:** none.
- **Evaluation:** none.

## Experiment template

Copy this section for every experiment.

### EXP-NNN: Short title

- **Status:**
- **Date:**
- **Research track:** abliteration / weight-space programming / evaluation / other
- **Question:**
- **Hypothesis:**
- **Source model and revision:**
- **Tokenizer revision:**
- **Architecture notes:**
- **Base checkpoint hash:**
- **Edit method and code revision:**
- **Changed tensors / layers:**
- **Runtime and hardware:**
- **Dtype / quantization:**
- **Evaluation suite and revision:**
- **Decoding parameters:**
- **Baseline results:**
- **Candidate results:**
- **Regression checks:**
- **Artifacts / logs:**
- **Conclusion:** supported / rejected / inconclusive
- **Known limitations:**
- **Next step:**

## Reporting rules

- Do not invent missing values. Mark them as unknown.
- Separate measured results from interpretations.
- Preserve failed and negative results.
- Record whether results are from a full-precision checkpoint or a quantized deployment artifact.
- Record any changes to prompts, decoding settings, or evaluation code.
