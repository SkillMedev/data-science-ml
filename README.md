# Data Science & ML

**For ML teams: ship a trustworthy model end-to-end, from EDA to production drift alerts.** — built in-house by [Skill&nbsp;Me](https://skillme.dev).

Reach for this pack when you own an ML model and need it to survive contact with production. It walks the full lifecycle as a connected discipline: profile the data before you model, engineer leakage-safe features, track experiments so results reproduce, evaluate honestly against real baselines and error slices (for both classic models and LLM systems), document the model for the people it affects, and watch for drift so you retrain on evidence instead of vibes. The payoff is a model you can defend to stakeholders and trust over the long haul — not a notebook that worked once.

⭐ **If this is useful, star the repo** — it's how we gauge what to build next.

## Install

- **From the catalog:** [skillme.dev/pack/data-science-ml](https://skillme.dev/pack/data-science-ml) — install the whole pack into Claude in one step.
- **With the skills CLI:** `npx skills add aouellets/data-science-ml`
- **Manually:** copy any `skills/<slug>/SKILL.md` into your Claude skills directory.

## Skills in this pack

- **[EDA Playbook](skills/eda-playbook/SKILL.md)** — Run a structured exploratory data analysis before modeling.
- **[Feature Engineering](skills/ml-feature-engineering/SKILL.md)** — Designs ML features: encoding, scaling, interaction terms, and leakage prevention.
- **[Feature Store Design](skills/feature-store-design/SKILL.md)** — Design reusable, leakage-safe features and a feature store schema.
- **[Experiment Tracking](skills/experiment-tracking/SKILL.md)** — Set up disciplined ML experiment tracking for reproducibility and comparison.
- **[Model Evaluation Report](skills/model-evaluation-report/SKILL.md)** — Evaluate an ML model honestly against baselines, metrics, and error slices.
- **[Model Card Writer](skills/model-card-writer/SKILL.md)** — Write a model card documenting intended use, training data, evaluation, and limitations.
- **[Data Drift Monitor](skills/data-drift-monitor/SKILL.md)** — Monitor production models for data and concept drift, set alert thresholds, and decide when to retrain.

## License

MIT — see [LICENSE](LICENSE). Skills are portable `SKILL.md` files; the canonical
copies live in the [Skill&nbsp;Me catalog](https://skillme.dev).
