# Project Architecture

**Status:** Proposed baseline under approved foundation  
**Architecture style:** Single analytical project with clear responsibility boundaries

## 1. Architectural objective

Provide a simple, reproducible workflow from synthetic source data to validated analytical outputs and executive communication. The architecture should support the first Payments Performance case without introducing production-platform complexity.

## 2. Logical flow

1. **Synthetic source data** — deterministic, documented payment records and reference values.
2. **SQL Server 2022** — relational storage, constraints, data exploration, quality checks, and analytical queries.
3. **Analysis and validation** — T-SQL as the primary analytical engine; Excel or Python/pandas for independent checks where useful.
4. **Power BI** — reporting model, measures, visualisations, and stakeholder-facing views.
5. **Executive outputs** — documented findings, limitations, interpretations, and recommendations.

## 3. Component responsibilities

| Component | Responsibility | Boundary |
|---|---|---|
| Synthetic data generation | Create repeatable fictional records | Must not encode desired findings as if discovered |
| SQL Server database | Store source and reference data consistently | Not a production banking database |
| T-SQL analysis | Define populations, calculate measures, investigate trends | Queries must document assumptions and filters |
| Validation | Test quality, reconcile totals, verify calculations | A successful query execution alone is insufficient |
| Excel / Python | Independent or supplementary checks | Use only where justified |
| Power BI | Communicate approved measures and analysis | Visuals must agree with validated definitions |
| Executive brief | Explain evidence and decision implications | No unsupported causal claims |

## 4. Initial data model direction

The initial relational model is expected to include payment transactions and reference entities for statuses, channels, and payment types. A calendar dimension may support consistent time-based reporting. Customer and product dimensions are deferred until a case requires them.

The transaction grain is proposed as **one row per payment attempt**. This must be confirmed during detailed requirements and data design before schema implementation.

Candidate transaction attributes include transaction identifier, event timestamp, channel, payment type, amount, currency, status, processing duration, and failure reason. Optional fields must be justified by the analytical questions.

## 5. KPI and semantic consistency

The KPI dictionary is the authoritative business definition. SQL calculations and Power BI measures must implement the same approved population, denominator, exclusions, and aggregation rules. Where independent calculations are used, differences must be investigated and documented.

## 6. Quality and security boundaries

All records are synthetic. Do not include real customer identifiers, account numbers, credentials, personal data, confidential business data, or production connection strings. Keep secrets out of version control. Document intentionally injected quality defects separately from legitimate business conditions.

## 7. Deferred architecture decisions

The following are not approved or required for the first release: cloud hosting, data lake, distributed processing, message brokers, microservices, workflow orchestration, and production deployment. Revisit only when a demonstrated requirement justifies the cost and complexity.

## 8. Architecture change control

Changes that materially affect architecture, technology, security boundaries, data integrity, dependencies, or infrastructure require Product Owner approval. Record approved decisions in `DECISIONS.md`.
