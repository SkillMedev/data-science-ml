---
name: Model Evaluation Report
description: Produces a rigorous, honest evaluation of an ML model including baselines, business-relevant metrics, and slice-level error analysis. Apply before any model promotion, stakeholder demo, or retraining decision.
---

# Model Evaluation Report

A model that beats a naive baseline on aggregate accuracy can still be worse than useless in production. Honest evaluation means choosing the right metrics, establishing real baselines, and examining where the model fails.

## 1. Establish Baselines First

No model result is meaningful without a comparison point.

- Majority-class classifier (classification) or mean-predictor (regression) is the floor
- Prior production model or rule-based system is the real bar to beat
- Human-level performance should be noted when it is measurable
- Report all baselines in the same table as the candidate model

## 2. Choose Metrics That Match the Business Problem

Accuracy is rarely the right primary metric.

- For imbalanced classification: prefer F1, precision-recall AUC, or Matthews Correlation Coefficient
- For ranking: use NDCG or MAP, not accuracy
- For regression: report both MAE and RMSE; large RMSE-to-MAE ratios signal outlier sensitivity
- Identify one primary metric and state it before looking at results — post-hoc metric selection is p-hacking

## 3. Confidence Intervals and Statistical Significance

Point estimates without uncertainty are incomplete.

- Bootstrap confidence intervals (1000 resamples minimum) for all primary metrics
- For A/B-style comparisons: report p-value and effect size, not just significance
- Flag any evaluation set smaller than 500 samples as underpowered

## 4. Slice-Level Error Analysis

Aggregate metrics hide the groups where the model fails.

- Segment performance by: each categorical feature, buckets of key numeric features, and time (if applicable)
- Flag any slice where performance is more than 10 percentage points below overall
- Report slice sample sizes — a slice with 12 examples is not actionable
- Equity audit: check performance parity across demographic-correlated features if data permits

## 5. Calibration and Confidence Quality

For probabilistic models, calibration matters as much as discrimination.

- Plot a reliability diagram (calibration curve) for classifiers
- Expected Calibration Error (ECE) should be reported
- A well-discriminating but poorly calibrated model needs Platt scaling or isotonic regression before deployment

## 6. Evaluation Report Structure

The report is the artifact, not the notebook.

- One-page executive summary: task, primary metric, baseline, result, recommendation
- Full metric table with confidence intervals
- Slice analysis table with flagged underperformers
- Known failure modes and mitigations
- Go / No-go recommendation with explicit criteria
