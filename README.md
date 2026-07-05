# Data Science & ML

**For ML teams: ship a trustworthy model end-to-end, from EDA to production drift alerts.** — built in-house by [Skill&nbsp;Me](https://skillme.dev).

Reach for this pack when you own an ML model and need it to survive contact with production. It walks the full lifecycle as a connected discipline: profile the data before you model, engineer leakage-safe features, track experiments so results reproduce, evaluate honestly against real baselines and error slices (for both classic models and LLM systems), document the model for the people it affects, and watch for drift so you retrain on evidence instead of vibes. The payoff is a model you can defend to stakeholders and trust over the long haul - not a notebook that worked once.

⭐ **If this is useful, star the repo** — it's how we gauge what to build next.

## Install

- **From the catalog:** [skillme.dev/pack/data-science-ml](https://skillme.dev/pack/data-science-ml) — install the whole pack into Claude in one step.
- **With the skills CLI:** `npx skills add SkillMedev/data-science-ml`
- **Manually:** copy any `skills/<slug>/SKILL.md` into your Claude skills directory.

## Skills in this pack

- **[EDA Playbook](skills/eda-playbook/SKILL.md)** — Runs a structured exploratory data analysis on a new or suspect dataset - schema audit, target analysis, feature profiling, missingness patterns, and leakage checks - ending in a written decision log.
- **[Feature Engineering](skills/ml-feature-engineering/SKILL.md)** — Designs ML features with leakage-safe pipelines, correct categorical encoding by cardinality, numeric transforms, and validation that a feature earns its place.
- **[Feature Store Design](skills/feature-store-design/SKILL.md)** — Designs a reusable, leakage-safe feature store - entity and naming contracts, point-in-time correct training joins, feature versioning, online/offline consistency with staleness SLOs, and governance.
- **[Experiment Tracking](skills/experiment-tracking/SKILL.md)** — Sets up disciplined ML experiment tracking - run logging schemas, artifact versioning, naming conventions, and reproducibility standards - and produces the run-record template a team actually follows.
- **[Model Evaluation Report](skills/model-evaluation-report/SKILL.md)** — Produces a rigorous, honest evaluation report for an ML model - real baselines, business-matched metrics with confidence intervals, slice-level error analysis, calibration checks, and a go/no-go recommendation.
- **[Model Card Writer](skills/model-card-writer/SKILL.md)** — Produces a complete model card - intended use, training data provenance, evaluation results with slices, limitations, and usage guidance - for any model shared beyond its team or affecting people.
- **[Data Drift Monitor](skills/data-drift-monitor/SKILL.md)** — Designs a production drift-monitoring plan for ML systems - statistical tests per feature type, PSI and KS alert thresholds, monitoring cadence, and evidence-based retraining triggers - including a runnable PSI calculator.

## License

MIT — see [LICENSE](LICENSE). Skills are portable `SKILL.md` files; the canonical
copies live in the [Skill&nbsp;Me catalog](https://skillme.dev).
