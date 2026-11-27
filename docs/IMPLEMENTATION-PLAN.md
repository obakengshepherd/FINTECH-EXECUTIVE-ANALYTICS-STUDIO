# Implementation Plan

**Status:** Foundation accepted; Phase 1 requirements and KPI definitions proposed and awaiting explicit Product Owner approval  
**Delivery method:** Incremental, evidence-based phases  
**Governance:** Four-Nexus Engineering Operating Standard (FNEOS); see `docs/AI-COLLABORATION.md`

## Phase 0 — Foundation and repository baseline
**Status:** ACCEPTED

- [x] Product Owner approved project foundation.
- [x] Product Owner approved Payments Performance Analytics as the first scenario.
- [x] Product Owner approved the initial toolkit.
- [x] Repository metadata and empty state inspected.
- [x] Foundation documentation reviewed and accepted by Product Owner.

**Exit evidence:** Approved foundation, repository documentation, and recorded decisions.

## Phase 1 — Business requirements and KPI design
**Status:** IN PROGRESS

- [x] Confirm initial stakeholder decision needs and business question.
- [x] Draft proposed analytical requirements in `docs/business/ANALYTICAL-REQUIREMENTS.md`.
- [x] Align the proposed KPI catalogue and validation expectations with the four proposed outcome categories.
- [ ] Complete independent specialist review of analytical requirements and KPI definitions.
- [ ] Resolve review findings and present material business-rule choices to the Product Owner.
- [ ] Obtain explicit Product Owner approval for the eligible population, grain, business rules, KPI definitions, formulas, and exclusions.
- [ ] Finalise the case specification, required dimensions, and analytical outputs after approval.

**Approval gate:** The current requirements and KPI definitions are proposals. This documentation consistency correction does not approve D-007 or any business rule. Do not treat the proposed four-status model, denominators, cancellation treatment, or value definitions as implementation authority until the Product Owner explicitly approves them.

**Exit evidence:** Product Owner-accepted case specification and KPI definitions, with assumptions, exclusions, edge cases, and approval status recorded.

## Phase 2 — Synthetic data environment
**Status:** NOT STARTED

- Design the minimal relational model only after Phase 1 approval.
- Define deterministic synthetic data generation and configuration.
- Document realistic distributions without predetermining analytical conclusions.
- Define controlled data-quality exceptions.
- Create schema and seed scripts after design approval.

**Exit evidence:** Reproducible dataset, documented grain, schema, and generation instructions.

## Phase 3 — Exploration and data quality
**Status:** NOT STARTED

- Profile record counts, ranges, nulls, duplicates, and distributions.
- Test referential integrity and domain validity.
- Separate injected defects from legitimate business events.
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
