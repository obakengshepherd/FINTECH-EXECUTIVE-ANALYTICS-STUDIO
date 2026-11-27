# Implementation Plan

**Status:** Phase 0 ACCEPTED · Phase 1 ACCEPTED · Phase 2 IN PROGRESS  
**Delivery method:** Incremental, evidence-based phases  
**Governance:** Four-Nexus Engineering Operating Standard (FNEOS); see `docs/AI-COLLABORATION.md`

## Phase 0 — Foundation and repository baseline
**Status:** ACCEPTED

- [x] Product Owner approved project foundation.
- [x] Product Owner approved Payments Performance Analytics as the first scenario.
- [x] Product Owner approved the initial toolkit.
- [x] Repository metadata and empty state inspected.
- [x] Foundation documentation reviewed and accepted.

**Exit evidence:** Approved foundation, repository documentation, and recorded decisions.

## Phase 1 — Business requirements and KPI design
**Status:** ACCEPTED — 2026-11-27

- [x] Confirm stakeholder decision needs and business question.
- [x] Define eligible population, attempt grain, retries, duplicate handling, and exclusions.
- [x] Approve four-status snapshot model and pending/cancelled treatment.
- [x] Approve UTC storage, SAST reporting, Monday–Sunday weeks, reporting period, and snapshot.
- [x] Approve ZAR-only scope and gross successful attempt value.
- [x] Approve KPI catalogue, formulas, denominators, NULL handling, dimensions, outputs, and reconciliations.
- [x] Record Product Owner approval in D-007.
- [x] Align case specification, analytical requirements, KPI dictionary, and quality standards.

**Exit evidence:** D-007 ACCEPTED; approved analytical requirements and KPI dictionary committed to main.

## Phase 2 — Synthetic data environment
**Status:** IN PROGRESS — FEA-SYN-001 issued; Claude implementation NOT STARTED

- [ ] Implement deterministic synthetic payments attempt generator.
- [ ] Implement automated tests for repeatability, schema/domain validity, status reconciliation, and reporting-period/snapshot boundaries.
- [ ] Generate the initial CSV dataset and inspect its output.
- [ ] Review dataset grain, distributions, and data-quality profile.
- [ ] Define the minimal SQL Server relational model in a subsequent bounded increment.
- [ ] Create SQL schema/load scripts after the model is approved within the existing architecture.

**Current increment:** FEA-SYN-001 — deterministic source CSV generator and tests. It generates a clean canonical eligible population only; deliberate defect injection is deferred.

**Exit evidence:** Reproducible synthetic source dataset, passing test evidence, documented grain and generation instructions. Database schema/load work is a subsequent increment, not part of FEA-SYN-001.

## Phase 3 — Exploration and data quality
**Status:** NOT STARTED

- Profile record counts, ranges, nulls, duplicates, and distributions.
- Test referential integrity and domain validity.
- Assess quantified exclusions and separately controlled injected defects.
- Record limitations and remediation/exclusion decisions.

**Exit evidence:** Reproducible quality checks and reviewed assessment.

## Phase 4 — SQL analytical development
**Status:** NOT STARTED

- Implement documented analytical queries.
- Calculate approved KPIs.
- Build time-series and segment analyses.
- Reconcile counts and values independently.
- Test date boundaries, filters, nulls, and status edge cases.

**Exit evidence:** Version-controlled queries, validation evidence, and reproducible findings.

## Phase 5 — Power BI reporting
**Status:** NOT STARTED

- Define reporting model and relationships.
- Implement measures aligned with the approved KPI dictionary.
- Build visuals that answer the approved questions.
- Validate report totals against SQL outputs.
- Document refresh and setup requirements.

**Exit evidence:** Report artifact and documented SQL-to-report reconciliation.

## Phase 6 — Executive insight communication
**Status:** NOT STARTED

- Summarise the business question, period, and population.
- Present validated findings and relevant comparisons.
- Explain interpretation, limitations, and uncertainty.
- Distinguish observations from hypotheses.
- Recommend proportionate next steps.

**Exit evidence:** Reviewed executive insight brief supported by reproducible evidence.

## Phase 7 — Verification, review, and portfolio presentation
**Status:** NOT STARTED

- Run the agreed validation suite.
- Review analytical logic, report consistency, and documentation.
- Record unresolved issues and limitations.
- Obtain Product Owner acceptance.
- Prepare an honest portfolio presentation.

**Exit evidence:** Verification record, review outcome, and Product Owner acceptance.

## Definition of done

A phase is not complete because files exist. Its exit evidence must be produced and reviewed. Use NOT STARTED, IN PROGRESS, BLOCKED, IMPLEMENTED, VERIFIED, and ACCEPTED precisely. Never claim tests or validation that were not actually performed.
