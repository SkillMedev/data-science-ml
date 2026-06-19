---
name: Feature Store Design
description: Guides the design of a reusable, leakage-safe feature store including entity modeling, transformation versioning, and point-in-time correctness. Apply when sharing features across models, building ML platform infrastructure, or diagnosing training-serving skew.
---

# Feature Store Design

Feature stores exist to solve three problems at once: reuse across models, point-in-time correctness during training, and consistency between training and serving. A design that solves only one of these is incomplete.

## 1. Entity and Feature Naming Conventions

Consistent naming is load-bearing — it is the API contract for every downstream model.

- Entity format: <entity-type>_id (e.g., user_id, item_id, session_id)
- Feature format: <entity-type>__<source>__<transformation>__<window> (e.g., user__payments__sum__30d)
- Avoid abbreviations not defined in a project glossary
- Each feature must have exactly one owning team or owner string in metadata

## 2. Point-in-Time Correctness

The most common feature store bug is silent label leakage from future data.

- Every feature retrieval must accept an as-of timestamp parameter
- Offline training joins must use point-in-time correct lookups — never a naive left join on entity ID
- Audit any feature derived from a slowly-changing dimension for the correct SCD type
- Document the event-time vs processing-time distinction for every feature source

## 3. Feature Versioning and Backfills

Changing a feature definition without a new version is a breaking change.

- Increment feature version when: transformation logic changes, source table changes, window size changes
- Old version must remain readable during any transition period
- Backfills must be idempotent; document the backfill strategy (full vs incremental)
- Store the transformation code reference (git commit or DAG run ID) alongside feature values

## 4. Online vs Offline Store Split

Online and offline stores have different consistency requirements.

- Offline store: append-only, partitioned by entity and date, optimized for bulk training retrieval
- Online store: low-latency key-value lookup, serves latest value only
- Dual-write pipelines must have a lag monitor — divergence beyond acceptable threshold triggers an alert
- Document acceptable staleness SLOs per feature (e.g., 15-minute max lag for online store)

## 5. Governance and Discovery

A feature store no one can discover is a feature store no one reuses.

- Every feature must have: description, entity, dtype, source table, owner, SLO, and a freshness check
- Deprecation process: mark deprecated, notify owners of dependent models, hard-delete after 90 days
- Track feature usage by model to identify orphaned features and high-value shared features
