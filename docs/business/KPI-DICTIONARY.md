# KPI Dictionary — Payments Performance

**Status:** Proposed KPI definitions; Product Owner/business-rule approval required before implementation  
**Authority:** This document is the intended canonical business definition for project KPIs.

## 1. General conventions

- Define the eligible population before calculating any KPI.
- State the measurement period and record grain.
- Distinguish attempts from unique payment instructions or customers.
- Report pending/unresolved outcomes separately.
- Do not combine currencies without an approved conversion methodology.
- Show numerator, denominator, exclusions, and volume context alongside rates.
- SQL and Power BI implementations must agree with these definitions.

## 2. Initial KPI catalogue

| ID | KPI | Proposed calculation | Unit |
|---|---|---|---|
| PAY-001 | Total Payment Attempts | Count of eligible payment-attempt records | Count |
| PAY-002 | Successful Payments | Count of eligible attempts classified successful | Count |
| PAY-003 | Failed Payments | Count of eligible attempts classified failed | Count |
| PAY-004 | Pending Payments | Count of eligible attempts classified pending/unresolved | Count |
| PAY-005 | Payment Success Rate | Successful attempts / resolved attempts × 100 | Percent |
| PAY-006 | Payment Failure Rate | Failed attempts / resolved attempts × 100 | Percent |
| PAY-007 | Successful Payment Value | Sum of amount for eligible successful attempts, grouped by currency | Currency amount |

## 3. Denominator and status convention

Proposed resolved attempts:

`Resolved Attempts = Successful Attempts + Failed Attempts`

Proposed success rate:

`Successful Attempts / Resolved Attempts × 100`

Proposed failure rate:

`Failed Attempts / Resolved Attempts × 100`

Pending/unresolved attempts are excluded from these denominators and reported separately. If the resolved denominator is zero, the rate is undefined/NULL, not zero.

## 4. Required metadata per KPI

Before implementation, each KPI must have:
- KPI ID and business name.
- Business purpose and stakeholder.
- Formula and calculation grain.
- Numerator and denominator definitions.
- Eligible population and filters.
- Exclusions and status mapping.
- Time attribution and reporting period.
- Currency and aggregation rules where relevant.
- Null/zero denominator handling.
- Source fields and lineage.
- Validation/reconciliation checks.
- Reporting frequency and owner.
- Version and approval status.

## 5. Important unresolved business rules

The current definitions are proposals, not final operational truth. Phase 1 must resolve:
- Whether a retry is a separate attempt.
- How duplicate submissions are identified.
- Whether a payment can change status and which event is authoritative.
- Treatment of reversals, cancellations, timeouts, and late-arriving outcomes.
- Whether successful value is gross, net of reversals, or another measure.
- Currency scope and any conversion rules.
- Eligible test, internal, or invalid records.

## 6. Proposed Phase 1 business-rule alignment

The accompanying [`ANALYTICAL-REQUIREMENTS.md`](ANALYTICAL-REQUIREMENTS.md) proposes an attempt-level grain, distinct retry attempts, duplicate attempt-ID exclusion, snapshot outcome categories (successful, failed, pending, cancelled), initiation-time weekly cohorting in SAST, ZAR-only gross successful value, and explicit exclusions for reversals/refunds and revenue/profitability. These are proposals pending Product Owner approval.

## 7. Validation expectations

- Successful + failed + pending categories reconcile to the eligible attempt population if the categories are mutually exclusive and exhaustive.
- Resolved attempts equal successful + failed attempts.
- Success and failure rates sum to 100% where the resolved denominator is positive and categories are exhaustive.
- Successful payment value reconciles to the eligible successful records by currency.
- SQL and Power BI totals reconcile for identical filters and periods.

No KPI is approved for executive reporting until its business rules are agreed and its implementation is verified.
