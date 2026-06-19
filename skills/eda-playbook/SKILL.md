---
name: EDA Playbook
description: Guides an analyst through a structured exploratory data analysis before any modeling begins. Apply when receiving a new dataset, debugging unexpected model behavior, or auditing data quality upstream.
---

# EDA Playbook

Skipping EDA before modeling is the single most common source of silent failures in ML pipelines. This skill establishes a repeatable, thorough checklist that surfaces problems early.

## 1. Shape and Schema Audit

Before anything else, verify the dataset dimensions and types match expectations.

- Confirm row count is in the expected range; flag if orders of magnitude off
- Check every column dtype; coerce-or-drop mismatches before downstream steps
- List columns with any null values and their null rates
- Flag columns with null rate above 20% for explicit handling decisions

## 2. Target Variable Analysis

Understand the label distribution before touching features.

- For classification: compute class frequencies and imbalance ratio
- For regression: plot the full distribution; check skew and kurtosis
- Identify any label values that are implausible or out of range
- Document the target definition precisely — ambiguity here cascades everywhere

## 3. Univariate Feature Profiling

Profile each feature independently before studying interactions.

- Numeric: min, max, mean, median, std, 1st and 99th percentiles
- Categorical: cardinality, top-5 values, frequency of the modal value
- Flag near-zero-variance features (std / mean below 0.01 for numerics; single value covering more than 98% for categoricals)
- Do NOT drop anything yet — document and defer

## 4. Missingness Patterns

Random missingness and structural missingness require different treatment.

- Compute a missingness correlation matrix across columns
- Columns that are always missing together suggest a data pipeline branch — investigate the source
- MCAR vs MNAR determination should be documented as an assumption when not verifiable

## 5. Bivariate and Leakage Checks

Correlation with the target is useful; perfect correlation is a red flag.

- Any feature with Pearson or Spearman r above 0.95 with the target warrants a leakage investigation
- Timestamp-derived features must be verified to use only information available at prediction time
- Identifiers (IDs, keys) should be excluded from modeling features unless deliberate

## 6. Summary and Decision Log

EDA output is only valuable if it drives decisions.

- Produce a written summary: dataset health, top risks, proposed handling for each flagged issue
- Record decisions (drop, impute, transform, flag) with rationale — not just the outcome
- Treat this log as a living document that gets updated when modeling reveals new issues
