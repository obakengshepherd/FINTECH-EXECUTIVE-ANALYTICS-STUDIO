# FinTech Executive Analytics Studio

A synthetic financial-services analytics portfolio project demonstrating how business questions and operational data become validated, explainable insights for decision-makers.

## Project status

**Foundation ACCEPTED · Phase 1 ACCEPTED · Phase 2 IN PROGRESS · FEA-SYN-001 issued · Code implementation NOT STARTED**

## Purpose

Build practical Data Analysis capability through a realistic, reproducible financial-services environment. The project demonstrates business problem definition, analytical requirements, data exploration, data quality assessment, SQL-based analysis, KPI governance, financial and operational analytics, visualisation, and executive communication.

This is a synthetic portfolio environment. It does not use or claim access to FNB, FirstRand, or any other institution's internal systems, confidential information, or production data.

## First analytical scenario

**Payments Performance Analytics**

Business question: How is payment performance changing over time, and where should management investigate potential operational issues?

The Product Owner-approved baseline uses one record per distinct payment attempt; four snapshot outcomes (SUCCESSFUL, FAILED, PENDING, CANCELLED); resolved-outcome rates; SAST reporting weeks; a twelve-month ZAR-only population; and gross successful attempt value. Full rules are in the [analytical requirements](docs/business/ANALYTICAL-REQUIREMENTS.md) and [KPI dictionary](docs/business/KPI-DICTIONARY.md).

## Approved toolkit

- SQL Server 2022 and T-SQL — primary analytical data store and analysis engine.
- Excel — inspection, reconciliation, and supporting analysis.
- Power BI — business-facing semantic model, visualisation, and reporting.
- Python — deterministic synthetic data generation and supplementary validation where justified.

## Working principles

The repository is the authoritative project record. Work follows **DISCOVER → DESIGN → BUILD → VERIFY → REVIEW → RECORD**. Material changes to scope, architecture, technology, security, or data integrity require Product Owner approval.

Analytical outputs must define their business question, population, period, KPI methodology, limitations, validation, findings, interpretation, and recommendations. Correlation must not be presented as causation. Findings must never be invented.

## AI collaboration and governance

This project follows the **Four-Nexus Engineering Operating Standard (FNEOS) v1.0**:
1. ChatGPT owns architecture, requirements, specifications, documentation, assignments, change control, and main-branch integration.
2. Claude performs one independent review of the relevant Primary AI work within the same bounded implementation handoff, then proceeds unless a genuine blocker or Product Owner decision prevents it. Claude implements only assigned code files and returns complete files in chat.
3. The user assembles and tests in VS Code; ChatGPT performs one return/alignment checkpoint and integrates approved work.

Claude does not push, commit, create branches, or modify ChatGPT-owned documentation. The workflow is defined in [AI collaboration](docs/AI-COLLABORATION.md). The current assignment and coordination state are recorded in [AI handoff](docs/AI-HANDOFF.md).

## Documentation

- [Project foundation](docs/PROJECT-FOUNDATION.md)
- [Architecture](docs/PROJECT-ARCHITECTURE.md)
- [Implementation plan](docs/IMPLEMENTATION-PLAN.md)
- [Decision register](docs/DECISIONS.md)
- [AI collaboration — FNEOS](docs/AI-COLLABORATION.md)
- [AI handoff and active assignment](docs/AI-HANDOFF.md)
- [Payments analytical case](docs/business/PAYMENTS-PERFORMANCE-CASE.md)
- [Approved analytical requirements](docs/business/ANALYTICAL-REQUIREMENTS.md)
- [Approved KPI dictionary](docs/business/KPI-DICTIONARY.md)
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
