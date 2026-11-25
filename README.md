# FinTech Executive Analytics Studio

A synthetic financial-services analytics portfolio project demonstrating how business questions and operational data become validated, explainable insights for decision-makers.

## Project status

**Foundation accepted · Phase 1 requirements in progress · Implementation not started**

## Purpose

Build practical Data Analysis capability through a realistic, reproducible financial-services environment. The project will demonstrate business problem definition, analytical requirements, data exploration, data quality assessment, SQL-based analysis, KPI governance, financial and operational analytics, visualisation, and executive communication.

This is a synthetic portfolio environment. It does not use or claim access to FNB, FirstRand, or any other institution's internal systems, confidential information, or production data.

## First analytical scenario

**Payments Performance Analytics**

Business question: How is payment performance changing over time, and where should management investigate potential operational issues?

Initial measures include payment attempts, resolved outcomes, successful and failed payments, pending payments, payment success and failure rates, and successful payment value.

## Approved toolkit

- SQL Server 2022 and T-SQL — primary analytical data store and analysis engine.
- Excel — inspection, reconciliation, and supporting analysis.
- Power BI — business-facing semantic model, visualisation, and reporting.
- Python/pandas — supplementary synthetic data generation, analysis, or validation where justified.

## Working principles

The repository is the authoritative project record. Work follows **DISCOVER → DESIGN → BUILD → VERIFY → REVIEW → RECORD**. Material changes to scope, architecture, technology, security, or data integrity require Product Owner approval.

Analytical outputs must define their business question, population, period, KPI methodology, limitations, validation, findings, interpretation, and recommendations. Correlation must not be presented as causation. Findings must never be invented.

## Documentation

- [Project foundation](docs/PROJECT-FOUNDATION.md)
- [Architecture](docs/PROJECT-ARCHITECTURE.md)
- [Implementation plan](docs/IMPLEMENTATION-PLAN.md)
- [Decision register](docs/DECISIONS.md)
- [Payments analytical case](docs/business/PAYMENTS-PERFORMANCE-CASE.md)
- [Analytical requirements](docs/business/ANALYTICAL-REQUIREMENTS.md)
- [KPI dictionary](docs/business/KPI-DICTIONARY.md)
- [Data quality standards](docs/quality/DATA-QUALITY-STANDARDS.md)

## Status vocabulary

- **NOT STARTED** — work has not begun.
- **IN PROGRESS** — work is underway.
- **BLOCKED** — progress depends on an unresolved issue.
- **IMPLEMENTED** — the change exists.
- **VERIFIED** — evidence demonstrates that it behaves or calculates as intended.
- **ACCEPTED** — the Product Owner has approved the deliverable.

## Claims and limitations

This repository demonstrates portfolio capability using synthetic data. It must not imply production deployment, access to confidential banking data, real customer outcomes, or business impact that has not been established.
