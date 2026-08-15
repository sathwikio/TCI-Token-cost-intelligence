# TCI — Token Cost Intelligence

> Compare AI model costs against real workloads.

TCI is a planned data product for collecting, normalizing, and analyzing AI model pricing.

Most pricing pages show unit prices. TCI will translate those prices into workload-level estimates so teams can compare models using the usage patterns that matter to them.

## Core Calculation

```text
workload cost =
(input tokens / 1,000,000 × input price)
+
(output tokens / 1,000,000 × output price)
```

The calculation can later incorporate additional pricing dimensions where the source provides them, such as cached tokens or reasoning tokens.

## Planned Capabilities

TCI will:

- Collect pricing and model metadata from multiple sources.
- Preserve raw source responses for traceability.
- Normalize provider and model records.
- Calculate cost for defined workload scenarios.
- Compare models by estimated workload cost.
- Track pricing changes over time.
- Expose decision-ready data through a dashboard.

The initial data source will be Models.dev.

## Data Flow

```text
Pricing sources
      ↓
Ingestion
      ↓
Bronze: raw snapshots
      ↓
Silver: normalized records
      ↓
Gold: workload cost and comparison data
      ↓
DuckDB and dashboard
```

The planned platform may use:

- Airflow for orchestration.
- Databricks for data processing.
- dbt for analytical transformations.
- DuckDB for local analytical access.
- A responsive dashboard for exploration and comparison.

These components are planned. They are not implemented yet.

## Design Principles

- **Transparent:** calculations expose their inputs and assumptions.
- **Reproducible:** source snapshots and transformations can be rerun.
- **Provider-neutral:** the model supports multiple providers and data sources.
- **Workload-oriented:** comparisons reflect usage, not just advertised unit prices.
- **Incremental:** the project proves one complete data path before expanding.

## Current Status

TCI is in the repository foundation stage.

The repository structure exists, but there is currently no production ingestion pipeline, transformation layer, orchestration, database, or dashboard.

The next milestone is a small vertical slice:

```text
Models.dev
   ↓
Raw JSON
   ↓
Normalized pricing table
   ↓
Workload cost calculation
   ↓
Model comparison
```

## Repository Structure

```text
TCI/
├── AGENTS.md
├── agents/
├── knowledge/
├── ingestion/
├── airflow/
├── databricks/
│   ├── bronze/
│   ├── silver/
│   └── gold/
├── dbt/
├── duckdb/
├── dashboard/
├── tests/
├── scripts/
├── docs/
└── .github/
```

TCI is intended to answer one practical question clearly:

> Given a specific workload, which AI model provides the right cost and capability trade-off?
