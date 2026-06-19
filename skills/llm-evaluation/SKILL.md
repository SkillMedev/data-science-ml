---
name: LLM Evaluation
description: Build eval frameworks for LLM output quality.
---

# LLM Evaluation

Measure whether your LLM system actually works, and catch regressions.

## Why evals

Prompt/model changes that look fine on one example often break others. Evals turn "seems good" into a number you can track across changes.

## Build a dataset first

1. Collect 50-200 real, representative inputs — include hard and edge cases.
2. Label expected outputs or acceptance criteria.
3. Hold out a frozen test set; iterate on a separate dev set to avoid overfitting.

## Metric types

- Deterministic: exact match, regex, JSON-schema validity, contains/excludes — cheap and reliable when applicable.
- Reference-based: similarity to a gold answer (use sparingly; surface form varies).
- Faithfulness/groundedness: does the answer stay within provided context (for RAG)?
- LLM-as-judge: a strong model scores outputs against a rubric for subjective quality.
- Human preference: pairwise comparisons for the final say.

## LLM-as-judge

```text
Rubric: Score 1-5 for whether the answer is correct AND grounded in the context.
Return JSON: { "score": n, "reason": "..." }.
```

- Use a clear rubric and ask for a structured score + justification.
- Calibrate the judge against human labels on a sample; judges have biases (length, position).
- Prefer pairwise (A vs B) over absolute scoring — it's more reliable.

## Pipeline

- Run the eval on every prompt/model change in CI.
- Track per-metric scores over time; alert on regressions.
- Report not just averages but failures — inspect the worst cases.

## Rules

- Separate dev and test sets; never tune on the test set.
- Include adversarial and out-of-distribution inputs.
- Make evals reproducible: pin model versions, temperature, and seeds where possible.
- Measure cost and latency alongside quality.

## Edge cases

- Non-determinism: run multiple samples and report variance.
- Judge cost: use a cheaper model for screening, strong model for close calls.
- Data leakage: ensure eval inputs aren't in the prompt's few-shot examples.
