---
name: Experiment Tracking
description: Establishes a disciplined experiment tracking setup covering logging, artifact versioning, and reproducibility standards. Apply when bootstrapping a new ML project, onboarding a team to a tracking tool, or investigating why a result cannot be reproduced.
---

# Experiment Tracking

An experiment no one can reproduce is a result no one can trust. Disciplined tracking is not overhead — it is the minimum viable scientific practice for ML.

## 1. What to Log on Every Run

Inconsistent logging is as bad as no logging.

- Hyperparameters: every value, including defaults — do not rely on code to reconstruct them
- Dataset: name, version or hash, split sizes, and any sampling applied
- Code: git commit SHA; fail the run if the working tree is dirty unless explicitly allowed
- Environment: Python version, key library versions (framework, numpy, pandas minimum)
- Metrics: train, validation, and test values; log per-epoch curves for iterative models
- Artifacts: model checkpoint path, preprocessor path, and evaluation report path

## 2. Experiment Naming and Organization

Naming is the index — garbage names make the tracker useless.

- Format: <project>/<hypothesis>/<variant> (e.g., churn/feature-selection/drop-low-variance)
- Never reuse a run name; each run is immutable once logged
- Group runs into experiments by hypothesis, not by date or author
- Tag runs with: dataset version, model family, and outcome (promoted / rejected / inconclusive)

## 3. Reproducibility Requirements

A run is reproducible only if it can be re-executed to within metric tolerance.

- Random seeds must be set and logged for: Python random, numpy, framework RNG, and data shuffling
- Dataset splits must be deterministic — hash-based splitting is preferred over random splits
- Containerized environments (Docker image SHA or conda lock file) are the gold standard
- Spot-check reproducibility: re-run the top experiment from scratch quarterly

## 4. Comparison and Promotion Workflow

Tracking only has value if it drives decisions.

- Promotion criterion must be defined before any experiment starts — not after results are in
- Compare runs using the same held-out test set; changing the test set resets the comparison
- Record the reason a run was rejected — negative results are valuable data
- Link every promoted model artifact back to the exact run that produced it

## 5. Tooling Defaults

MLflow is the default for self-hosted setups; Weights and Biases for teams needing collaboration features. Both satisfy the requirements above.

- Use the tracking server, not local file logging, for any team setting
- Set artifact storage to a shared location (S3 or GCS) from day one
- Automate the logging scaffold — a run that requires manual logging steps will be logged inconsistently
