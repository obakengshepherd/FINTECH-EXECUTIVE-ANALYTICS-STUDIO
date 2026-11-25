# Project Foundation

**Project:** FinTech Executive Analytics Studio  
**Version:** 1.0  
**Status:** Foundation approved; implementation not started  
**Authority:** Product Owner  
**Primary specialisation:** Data Analysis

## 1. Purpose

Create a realistic, reproducible synthetic financial-services analytics environment that demonstrates the process of translating business questions and operational data into validated, actionable, and clearly communicated insights.

The project is intended to demonstrate professional analytical judgement, not merely dashboard construction or query-writing ability.

## 2. Business context

The project uses a fictional South African financial institution. Its customers, accounts, transactions, products, channels, and operational events are synthetic. No FNB, FirstRand, or other institution's internal systems, confidential information, or production data are accessed or represented.

The initial stakeholder is a fictional Payments Operations Manager.

## 3. First analytical scenario

**Payments Performance Analytics**

Business question: How is payment performance changing over time, and where should management investigate potential operational issues?

The first release focuses on payment attempts, resolved outcomes, successful and failed payments, pending transactions, successful payment value, and performance trends. Channel and payment-type segmentation may be included where the data supports it.

## 4. Initial scope

### In scope
- Business problem definition and analytical requirements.
- Synthetic payment transaction data.
- SQL Server 2022 relational storage and T-SQL analysis.
- Data exploration and quality assessment.
- KPI definitions and calculation controls.
- Trend, variance, and segmentation analysis.
- Excel-based reconciliation where useful.
- Power BI reporting and executive communication.
- Python/pandas only where it provides justified value.

### Out of scope for the initial release
- Fraud detection and credit-risk modelling.
- Regulatory compliance monitoring.
- Predictive machine learning.
- Enterprise-wide financial consolidation.
- Production banking integrations or deployment.
- Unnecessary distributed infrastructure or orchestration.

## 5. Analytical discipline

Every investigation must record:
1. Business question and intended decision.
2. Stakeholder and relevant population.
3. Measurement period and record granularity.
4. KPI definitions and calculation methodology.
5. Filters, exclusions, and assumptions.
6. Data limitations and quality findings.
7. Validation and reconciliation evidence.
8. Actual findings and supporting evidence.
9. Business interpretation.
10. Recommendations and their evidential basis.

Correlation is not causation. An observed difference is not automatically an explanation. Recommendations must be proportionate to the evidence.

## 6. Approved toolkit

| Tool | Responsibility |
|---|---|
| SQL Server 2022 / T-SQL | Primary data store, exploration, analysis, KPI calculations, validation |
| Excel | Inspection, reconciliation, supporting business analysis |
| Power BI | Semantic model, visualisation, stakeholder reporting |
| Python / pandas | Supplementary synthetic data generation, analysis, or validation when justified |

## 7. Engineering principles

Prioritise correctness, simplicity, maintainability, security, reliability, testability, explainability, and practical business value. Do not add infrastructure, frameworks, dependencies, or architectural complexity without demonstrated need.

Follow **DISCOVER → DESIGN → BUILD → VERIFY → REVIEW → RECORD**. Inspect the repository before modifying it. Preserve verified work. Obtain Product Owner approval for material changes to business requirements, scope, architecture, technology, security boundaries, data integrity rules, dependencies, or infrastructure commitments.

## 8. Evidence and maturity

Use the status vocabulary:
- NOT STARTED
- IN PROGRESS
- BLOCKED
- IMPLEMENTED
- VERIFIED
- ACCEPTED

Implemented does not mean verified; verified does not mean accepted. Never claim production usage, deployment, business impact, or access to real banking data without evidence.

## 9. Initial success definition

The first scenario is successful when a reader can trace a business question through documented requirements, defined KPIs, synthetic source data, quality checks, reproducible SQL analysis, reconciled results, an appropriately designed Power BI output, and a concise executive insight brief.

## 10. Product ownership

The user is Product Owner and final decision-maker. The AI collaborator may execute approved work and make routine implementation decisions within the approved boundaries. Material decisions require approval and must be recorded in the repository.
