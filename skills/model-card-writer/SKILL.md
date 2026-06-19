---
name: Model Card Writer
description: Produces a complete model card covering intended use, training data, evaluation results, limitations, and ethical considerations. Apply before deploying any model that affects people or will be shared beyond the immediate team.
---

# Model Card Writer

A model card is the contract between the team that built a model and the people who will use or be affected by it. It documents not just what the model does but what it should and should not be used for.

## 1. Model Overview Section

Start with the facts any reader needs to orient themselves.

- Model name, version, and release date
- Model type: architecture family (e.g., gradient boosted trees, transformer) in plain language
- Intended use cases: specific, bounded statements of what the model is designed to do
- Out-of-scope uses: explicit list of uses the model is NOT designed for
- Primary contact or owning team

## 2. Training Data Section

Data documentation is as important as model documentation.

- Dataset name(s) and version(s)
- Collection method and time range
- Geographic and demographic scope
- Known gaps or underrepresented populations
- Data preprocessing steps that affect interpretation
- Do NOT include PII or specifics that would allow reconstruction of training records

## 3. Evaluation Results Section

Report results honestly, including failures.

- Primary metric and value with confidence interval
- Baseline comparisons (majority class, prior model, human performance if measured)
- Slice-level results for demographic and domain subgroups
- Known failure modes with estimated frequency
- Evaluation dataset description (distinct from training data)

## 4. Limitations and Risks Section

This section requires more honesty than most teams are comfortable with — do it anyway.

- Performance degradation conditions: distribution shifts, edge cases, adversarial inputs
- Potential for misuse and how it has been mitigated
- Fairness considerations: which groups may be disadvantaged and what was done about it
- Uncertainty: what the team does not know about model behavior in production

## 5. Usage Guidance Section

Give the consumer enough information to use the model responsibly.

- Recommended confidence threshold or decision rules
- Human-in-the-loop requirements for high-stakes decisions
- Monitoring requirements: what signals indicate the model needs retraining
- Version policy: how long this version will be maintained and what triggers a new version

## 6. Format and Publishing

- Model cards should be stored with the model artifact, not in a separate documentation system
- Review and update the card at every model version bump
- A model card that has not been updated in over 12 months should be treated as stale
