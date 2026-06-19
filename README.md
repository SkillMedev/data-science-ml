# Data Science & ML

**Rigorous skills for every stage of the ML lifecycle, from EDA to production monitoring.** — built in-house by [Skill&nbsp;Me](https://skillme.dev).

This pack covers the full ML workflow with opinionated, production-tested guidance. It addresses the most common failure modes in data science: skipped EDA, dishonest evaluation, leaky features, irreproducible experiments, undocumented models, and silent drift. Each skill is self-contained and immediately applicable to real projects.

⭐ **If this is useful, star the repo** — it's how we gauge what to build next.

## Install

- **From the catalog:** [skillme.dev/pack/data-science-ml](https://skillme.dev/pack/data-science-ml) — install the whole pack into Claude in one step.
- **With the skills CLI:** `npx skills add aouellets/data-science-ml`
- **Manually:** copy any `skills/<slug>/SKILL.md` into your Claude skills directory.

## Skills in this pack

- **[EDA Playbook](skills/eda-playbook/SKILL.md)** — Run a structured exploratory data analysis before modeling.
- **[Model Evaluation Report](skills/model-evaluation-report/SKILL.md)** — Evaluate an ML model honestly against baselines, metrics, and error slices.
- **[Feature Store Design](skills/feature-store-design/SKILL.md)** — Design reusable, leakage-safe features and a feature store schema.
- **[Experiment Tracking](skills/experiment-tracking/SKILL.md)** — Set up disciplined ML experiment tracking for reproducibility and comparison.
- **[Model Card Writer](skills/model-card-writer/SKILL.md)** — Write a model card documenting intended use, training data, evaluation, and limitations.
- **[Data Drift Monitor](skills/data-drift-monitor/SKILL.md)** — Monitor production models for data and concept drift, set alert thresholds, and decide when to retrain.
- **[Feature Engineering](skills/ml-feature-engineering/SKILL.md)** — Designs ML features: encoding, scaling, interaction terms, and leakage prevention.
- **[LLM Evaluation](skills/llm-evaluation/SKILL.md)** — Designs eval frameworks for LLM outputs — correctness, faithfulness, and human preference.

## License

MIT — see [LICENSE](LICENSE). Skills are portable `SKILL.md` files; the canonical
copies live in the [Skill&nbsp;Me catalog](https://skillme.dev).
