# KPI Dictionary — Payments Performance

**Version:** 1.0  
**Status:** APPROVED — Product Owner, 2026-11-27  
**Authority:** D-007 and `docs/business/ANALYTICAL-REQUIREMENTS.md`

## 1. General conventions

- Canonical grain: one distinct payment attempt.
- Eligible population: valid, non-test/internal, ZAR-denominated attempts in the reporting period.
- Measurement period: 2025-10-01 through 2026-09-30 inclusive.
- Initial outcome snapshot: 2026-10-31 23:59:59 SAST.
- Store event timestamps in UTC; report dates and weeks in SAST (UTC+02:00), Monday–Sunday.
- Distinguish attempts from payment instructions.
- Report pending and cancelled separately from resolved outcomes.
- Display numerator, denominator, exclusions, and volume context with rates.
- Do not combine currencies.
- SQL and Power BI must implement the same population, definitions, and filters.

## 2. Approved KPI catalogue

| ID | KPI | Approved calculation | Unit |
|---|---|---|---|
| PAY-001 | Total Payment Attempts | Count of eligible canonical distinct payment attempts | Count |
| PAY-002 | Successful Attempts | Count of eligible attempts with snapshot outcome SUCCESSFUL | Count |
| PAY-003 | Failed Attempts | Count of eligible attempts with snapshot outcome FAILED | Count |
| PAY-004 | Pending Attempts | Count of eligible attempts with snapshot outcome PENDING | Count |
| PAY-005 | Payment Success Rate | Successful Attempts / Resolved Attempts × 100 | Percent |
| PAY-006 | Payment Failure Rate | Failed Attempts / Resolved Attempts × 100 | Percent |
| PAY-007 | Gross Successful Attempt Value | Sum of amount for eligible SUCCESSFUL attempts, in ZAR | ZAR |
| PAY-008 | Cancelled Attempts | Count of eligible attempts with snapshot outcome CANCELLED | Count |

## 3. Supporting measures and denominators

**Resolved Attempts** (supporting measure, not a separate catalogue KPI):

`Resolved Attempts = Successful Attempts + Failed Attempts`

**Outcome reconciliation:**

`Eligible Attempts = Successful + Failed + Pending + Cancelled`

This equality applies to the eligible canonical snapshot population. Quality exceptions and excluded records are counted separately and are not part of its denominator.

**Payment Success Rate:**

`Successful Attempts / Resolved Attempts × 100`

**Payment Failure Rate:**

`Failed Attempts / Resolved Attempts × 100`

Pending and cancelled attempts are excluded from the resolved denominator and reported separately. If Resolved Attempts is zero, both rates are NULL/undefined, not zero. When Resolved Attempts is positive, success and failure rates sum to 100%.

## 4. Population, exclusions and deduplication

- A genuine retry with a distinct attempt ID is a separate attempt.
- An identical repeated copy of the same attempt ID and payload is counted once; duplicate copies are quantified as a quality issue.
- Conflicting payloads for the same attempt ID are quarantined; none of the conflicting versions enters the eligible KPI population.
- Explicit test/internal records, mandatory identity/validity failures, unknown/missing/invalid/conflicting statuses, and non-ZAR records are excluded and quantified.
- Similar amounts or timestamps alone are not a deduplication key.

## 5. Monetary definition

PAY-007 sums the amount on eligible successful attempts only, with amounts expressed in ZAR to two decimal places. Retries are separate attempts and may each contribute if successful. PAY-007 is gross successful attempt value; it is not revenue, fees, profit, net settlement, or unique instruction value. Reversals, refunds, and chargebacks are excluded.

## 6. Time and snapshot

Attempts are attributed to their initiation timestamp. UTC timestamps are converted to SAST (UTC+02:00) for reporting dates and Monday–Sunday weeks. The initial outcome is measured as of 2026-10-31 23:59:59 SAST. Later outcomes require a separately identified later snapshot; previously published snapshots are not silently rewritten.

## 7. Required metadata and validation

Each implementation must document KPI ID, purpose, grain, source fields, population, filters, numerator/denominator, exclusions, time attribution, aggregation, null handling, and validation.

Validation:
- PAY-001 equals the sum of PAY-002, PAY-003, PAY-004, and PAY-008.
- Resolved Attempts equals PAY-002 + PAY-003.
- PAY-005 + PAY-006 equals 100% when Resolved Attempts is positive.
- PAY-007 reconciles to the sum of eligible successful ZAR amounts.
- Quality/exclusion counts are separately reported and never silently absorbed into KPI categories.
- SQL and Power BI totals reconcile under identical filters.

No KPI should be described as independently verified until its implementation has been tested against these definitions and evidence recorded.
