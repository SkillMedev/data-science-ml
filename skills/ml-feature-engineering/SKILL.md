---
name: Feature Engineering
description: Design ML features with correct encoding, scaling, and leakage prevention.
---

# Feature Engineering

Transform raw data into features that improve model performance without leaking the target.

## Prevent leakage first

Leakage is the most common and most damaging mistake. Rules:

1. Fit all transformers (scalers, encoders, imputers) on the training fold only, then apply to validation and test.
2. Never use future information relative to the prediction time.
3. Exclude features that are proxies for the label or only known after the outcome.
4. For time series, split by time and never shuffle.

Use scikit-learn Pipelines and ColumnTransformer so fitting always happens inside cross-validation:

```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
pre = ColumnTransformer([
    ("num", StandardScaler(), num_cols),
    ("cat", OneHotEncoder(handle_unknown="ignore"), cat_cols),
])
model = Pipeline([("pre", pre), ("clf", GradientBoostingClassifier())])
```

## Categorical encoding

- One-hot for low cardinality.
- Target/mean encoding for high cardinality, but compute it with out-of-fold means to avoid leakage.
- Hashing for very high cardinality when memory matters.
- Ordinal encoding only when categories have a true order.

## Numeric transforms

- Scale (standardize or min-max) for distance and gradient based models; trees do not need it.
- Apply log or Box-Cox to skewed positive features.
- Bin into quantiles when the relationship is non-monotonic and the model is linear.

## Interaction and derived features

- Ratios and differences often encode domain meaning (price per unit, days since last event).
- Polynomial or explicit interaction terms help linear models capture combined effects.
- Aggregations: group-by statistics (mean, count, std) per entity, computed out-of-fold.

## Datetime features

Extract hour, day of week, month, is_weekend, and cyclical sine/cosine encodings for periodic values. Add elapsed-time features like days since signup.

## Missing values

- Add a binary missing-indicator before imputing; missingness can be informative.
- Impute numerics with median, categoricals with a dedicated category.
- Avoid mean imputation on skewed data.

## Selection and validation

- Remove near-constant and highly collinear features.
- Use permutation importance or SHAP rather than raw model importances.
- Always validate that a new feature improves cross-validated metrics, not just training fit.
- Keep a feature catalog documenting source, transformation, and refresh cadence.
