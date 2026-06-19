---
name: Data Drift Monitor
description: Establishes a monitoring strategy for data drift and concept drift in production ML systems, including statistical tests, alert thresholds, and retraining triggers. Apply when deploying a model, building an MLOps pipeline, or investigating unexplained model performance degradation.
---

# Data Drift Monitor

Models trained on historical data degrade when the world changes. Drift monitoring is the early-warning system that distinguishes a model aging gracefully from one silently failing.

## 1. Types of Drift to Monitor

Not all drift requires the same response.

- Data drift (covariate shift): input feature distribution changes; model may still work if the label relationship is stable
- Concept drift: the relationship between features and labels changes; requires retraining regardless of input distribution
- Label drift: ground truth label distribution shifts; relevant for classification thresholds
- Upstream data drift: schema changes or pipeline failures masquerading as real drift

## 2. Statistical Tests by Feature Type

Choose tests matched to the feature type.

- Continuous features: Kolmogorov-Smirnov test or Population Stability Index (PSI)
- Categorical features: chi-squared test or Jensen-Shannon divergence
- PSI thresholds: below 0.1 is stable, 0.1-0.2 is moderate (investigate), above 0.2 is significant (act)
- Use a rolling reference window (last 30 days of training data) rather than a fixed baseline

## 3. Monitoring Cadence and Coverage

Monitor everything at the same frequency is wasteful.

- High-frequency inputs: monitor daily; low-frequency inputs: monitor weekly
- Always monitor the top 10 features by model importance at maximum frequency
- Ground truth labels often lag predictions — account for this delay in concept drift checks

## 4. Alert Thresholds and Escalation

Alerts with no action plan create alert fatigue.

- Warning: PSI above 0.1 or KS p-value below 0.05 — investigate, do not retrain yet
- Critical: PSI above 0.2 or primary business metric drops more than 5% from 30-day baseline — initiate retraining evaluation
- Every alert must route to a named owner; suppress alerts during known events with documented windows

## 5. Retraining Decision Criteria

Retraining has a cost; trigger it on evidence, not on schedule alone.

- Triggers: critical drift alert, primary metric degradation above threshold, or quarterly review minimum
- Before retraining: verify new training data does not contain the drift as label leakage
- After retraining: shadow-deploy and compare metrics on recent production data before full promotion
- Document each retraining event: trigger reason, data window used, metric delta, and promotion decision
