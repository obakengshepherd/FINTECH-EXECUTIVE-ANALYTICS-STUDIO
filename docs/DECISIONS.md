# Decision Register

## D-007 — Phase 1 analytical requirements baseline

- **Original proposal date:** 2026-11-25
- **Approval date:** 2026-11-27
- **Status:** ACCEPTED
- **Authority:** Product Owner.
- **Decision:** Approve the Payments Performance analytical population, attempt grain, outcome taxonomy, KPI formulas, time attribution, reporting period, snapshot, currency scope, exclusions, and validation rules as recorded in `docs/business/ANALYTICAL-REQUIREMENTS.md` and `docs/business/KPI-DICTIONARY.md`.
- **Approved rules:**
  1. One canonical row per distinct payment attempt. A genuine retry with a new attempt ID is a separate attempt; exact duplicate copies of an ID/payload count once and are recorded as a quality issue; conflicting records sharing an attempt ID are quarantined and excluded from the KPI population.
  2. Retain payment-instruction ID to identify attempts belonging to the same instruction.
  3. Exclude explicitly identified test/internal records and records failing mandatory identity/validity checks from the eligible KPI population, while quantifying and reporting exclusions. Unknown, missing, invalid, or conflicting outcome statuses are quality exceptions outside the eligible KPI population and are not coerced into a valid status.
  4. Classify each eligible attempt at the fixed snapshot as exactly one of SUCCESSFUL, FAILED, PENDING, or CANCELLED. Pending and cancelled are reported separately and excluded from the resolved success/failure denominator.
  5. Resolved attempts = successful + failed. Success rate = successful / resolved × 100. Failure rate = failed / resolved × 100. Rates are NULL when resolved attempts are zero.
  6. Attribute attempts to initiation date/time. Store event timestamps in UTC and derive reporting dates/weeks in SAST (UTC+02:00), with Monday–Sunday weeks.
  7. Reporting population: 2025-10-01 through 2026-09-30 inclusive (twelve complete calendar months). Fixed initial outcome snapshot: 2026-10-31 23:59:59 SAST. Later snapshots must be separately identified; do not silently rewrite a previously published snapshot.
  8. ZAR-only. Non-ZAR records are excluded from KPI calculations and quantified in exclusions. Amounts use two decimal places.
  9. Gross Successful Attempt Value (ZAR) is the sum of amounts on eligible successful attempts. It is not revenue, fees, profit, net settlement, or unique instruction value. Reversals, refunds, and chargebacks are outside this initial scenario.
  10. Initial dimensions are reporting date/week, channel, payment type, and outcome status. Failure reason is optional where controlled and sufficiently populated. No customer profiling, fraud modelling, causal inference, or unsupported SLA claims.
- **Consequences:** D-007 is implementation authority for the first Payments Performance synthetic dataset and subsequent analytical work. The detailed case and KPI documents must remain aligned with this decision.

## D-008 — Four-Nexus Engineering Operating Standard

- **Date:** 2026-11-27
- **Status:** ACCEPTED
- **Decision:** Adopt FNEOS v1.0 as the governing AI collaboration and repository workflow for this project.
- **Authority:** Product Owner.
- **Operating model:** ChatGPT owns architecture, requirements, documentation, assignments, and main-branch integration; Claude performs one independent review within the same bounded implementation handoff and proceeds unless a genuine blocker or Product Owner decision prevents it; the user assembles and tests in VS Code; ChatGPT performs one return/alignment checkpoint and integrates approved work.
- **Ownership:** ChatGPT owns project documentation. Claude may read documentation but may not modify it without explicit Product Owner-approved ownership transfer. Claude owns only assigned code files during an active engineering assignment.
- **Repository governance:** No Claude GitHub writes, branches, commits, or pull requests. Branch-based work is prohibited unless explicitly authorised by the Product Owner. Preserve history; no force-push or history rewriting.

## D-006 — Foundation documentation accepted

- **Date:** 2026-11-25
- **Status:** ACCEPTED
- **Decision:** Product Owner accepted the eight-file foundation documentation baseline.
- **Consequence:** Phase 0 is ACCEPTED and Phase 1 requirements work may proceed.

Record material business, analytical, technical, and governance decisions here. Newest decisions appear first. Proposed decisions must not be represented as approved.

## D-001 — Project foundation approval

- **Date:** 2026-11-25
- **Status:** APPROVED
- **Decision:** Establish FinTech Executive Analytics Studio as a synthetic financial-services Data Analysis portfolio project.
- **Authority:** Product Owner
- **Rationale:** Demonstrate the conversion of business questions and raw data into validated, actionable insights and executive communication.
- **Consequences:** Repository documentation and subsequent work must preserve synthetic-data boundaries and analytical discipline.

## D-002 — First analytical scenario

- **Date:** 2026-11-25
- **Status:** APPROVED
- **Decision:** Begin with Payments Performance Analytics.
- **Business question:** How is payment performance changing over time, and where should management investigate potential operational issues?
- **Rationale:** A bounded operational scenario provides a practical foundation for requirements, KPI governance, SQL analysis, validation, and executive reporting.

## D-003 — Initial toolkit

- **Date:** 2026-11-25
- **Status:** APPROVED
- **Decision:** Use SQL Server 2022/T-SQL as the primary analytical engine, Excel for supporting inspection and reconciliation, Power BI for visualisation and reporting, and Python where justified.
- **Rationale:** Prioritise practical analytical capability over unnecessary technology.

## D-004 — Clean-slate repository

- **Date:** 2026-11-25
- **Status:** CONFIRMED
- **Decision:** Use the supplied GitHub repository as a new project baseline.
- **Evidence:** Repository metadata showed public visibility, default branch `main`, size 0 KB; contents endpoint reported that the repository was empty and branch listing returned no branches.
- **Consequence:** No prior project implementation or documentation was inherited.

## D-005 — Initial architecture direction

- **Date:** 2026-11-25
- **Status:** PROPOSED BASELINE
- **Decision:** Use a single analytical project with synthetic source data, SQL Server, T-SQL analysis and validation, optional Excel/Python support, Power BI reporting, and executive outputs.
- **Rationale:** This is the simplest structure that satisfies the approved first scenario.
- **Constraint:** Material architecture changes require Product Owner approval.
