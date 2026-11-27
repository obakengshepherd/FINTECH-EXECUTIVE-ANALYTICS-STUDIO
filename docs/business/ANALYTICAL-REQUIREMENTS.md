# Analytical Requirements — Payments Performance

**Version:** 1.0  
**Status:** APPROVED — Product Owner, 2026-11-27  
**Decision authority:** D-007  
**Business owner:** Fictional Payments Operations Manager  
**Analytical owner:** Project Data Analyst

## 1. Business objective

Provide Payments Operations management with a consistent weekly view of payment-attempt volumes and outcomes, gross successful attempt value, and differences across payment channels and payment types. The report should identify where performance has changed and where further investigation may be warranted.

The analysis is descriptive and diagnostic. It does not, by itself, establish causes or prove that a channel, payment type, or operational factor caused an outcome.

## 2. Decisions the analysis should support

- Understand payment-attempt volume and outcome mix over time.
- Monitor the proportion of resolved attempts that succeed or fail.
- Identify weeks or segments with material observed changes.
- Understand the volume and value context behind rate movements.
- Identify pending items for operational follow-up.
- Decide which patterns warrant further investigation.

No operational targets or SLA breaches will be prescribed without an independently approved target and measurement rule.

## 3. Population and grain

**Canonical grain:** One row per distinct payment attempt.

**Eligible KPI population:** Initiated payment attempts in the selected reporting period that pass mandatory identity and validity checks, are not explicitly identified as test/internal records, and are denominated in ZAR.

A payment instruction may have more than one attempt. Each genuine retry with a distinct attempt identifier is counted as a separate attempt. A repeated copy of the same attempt ID and same payload is a duplicate ingestion/data-quality issue; it counts once and the duplicate is quantified. If the same attempt ID appears with conflicting payloads, all conflicting versions for that ID are quarantined from the eligible KPI population and reported as a quality exception. Similar amounts or timestamps alone are insufficient evidence to deduplicate two attempts.

Retain a payment-instruction identifier to associate retries with their originating instruction. Initial operational KPIs remain attempt-based, not instruction-based.

Explicitly identified test/internal records, invalid mandatory identity/validity records, unknown/missing/invalid/conflicting status records, conflicting attempt-ID records, and non-ZAR records are excluded from the eligible KPI population and quantified in the quality/exclusion summary. Do not silently discard them or force them into valid categories. Exact duplicate copies of an otherwise valid attempt are deduplicated to one canonical attempt and reported separately.

## 4. Outcome model and snapshot

Each eligible attempt has exactly one reporting outcome at the fixed initial snapshot of **2026-10-31 23:59:59 SAST (UTC+02:00)**:

- **SUCCESSFUL:** the attempt completed successfully on or before the snapshot.
- **FAILED:** the attempt reached a defined failure outcome on or before the snapshot.
- **PENDING:** no successful, failed, or cancelled terminal outcome was available at the snapshot.
- **CANCELLED:** the attempt was cancelled before a successful or failed terminal outcome and on or before the snapshot.

The four categories are mutually exclusive and exhaustive for the eligible canonical attempt population. A later terminal outcome does not silently alter this initial snapshot. A later as-of snapshot must be labelled and reported separately.

Pending and cancelled attempts are reported separately and excluded from resolved success/failure denominators. Reversals, refunds, and chargebacks are post-success financial adjustments outside this scenario.

## 5. Time attribution and reporting cadence

- Store event timestamps in UTC.
- Derive reporting date and reporting week using SAST (UTC+02:00).
- Cohort attempts by their initiation timestamp, not by a later outcome timestamp.
- Reporting weeks run Monday–Sunday in SAST.
- Reporting period: **2025-10-01 through 2026-09-30 inclusive**, twelve complete calendar months.
- Initial fixed outcome snapshot: **2026-10-31 23:59:59 SAST**.
- Monthly summaries may be provided as roll-ups of the weekly analysis.

The snapshot is an as-of rule, not an SLA or an assertion that all attempts should resolve within a month. A later snapshot or restatement must be explicitly identified and must not silently rewrite previously published results.

## 6. Currency and monetary scope

The initial eligible KPI population is ZAR-only. Non-ZAR records are excluded from KPI calculations and counted in the exclusion summary. No foreign-exchange conversion or cross-currency aggregation is performed.

Amounts are represented to two decimal places. **Gross Successful Attempt Value (ZAR)** is the sum of amounts on eligible successful attempts. It is not revenue, fee income, margin, profit, net settlement, or unique payment-instruction value. Retries are separate attempts and are counted separately when successful.

## 7. Dimensions

Required dimensions:
- Reporting date/week.
- Payment channel.
- Payment type.
- Outcome status.

Failure reason may be included where definitions are controlled and sufficiently populated. Customer-level analysis is not required.

Segmented rates must always be presented with attempt and resolved denominators. Small populations should be flagged for cautious interpretation; no arbitrary minimum-volume threshold is imposed.

## 8. Required analytical outputs

1. Weekly payment-attempt volume and outcome counts.
2. Weekly resolved success and failure rates.
3. Weekly gross successful attempt value in ZAR.
4. Outcome mix including pending and cancelled attempts.
5. Channel and payment-type comparisons with denominators.
6. Data-quality and exclusion summary, including duplicate, quarantined, invalid, test/internal, and non-ZAR counts.
7. Concise executive insight brief documenting findings, limitations, interpretation, and recommendations.

## 9. Validation and reconciliation requirements

- Canonical attempt identifiers are unique in the eligible attempt population.
- Duplicate identical copies are counted once and separately quantified.
- Conflicting attempt-ID payloads are quarantined and separately quantified.
- Status categories are valid, mutually exclusive, and exhaustive for the eligible snapshot population.
- Successful + failed + pending + cancelled counts reconcile exactly to eligible canonical attempts.
- Resolved attempts equal successful + failed attempts.
- Success and failure rates sum to 100% when the resolved denominator is positive.
- Gross successful attempt value reconciles to the sum of eligible successful attempt amounts in ZAR.
- Non-ZAR, test/internal, invalid identity/validity, and status exceptions are quantified outside the eligible KPI population.
- UTC-to-SAST conversion and Monday–Sunday week boundaries are tested.
- SQL and Power BI outputs reconcile for identical populations, dates, and filters.

## 10. Explicit exclusions

The first scenario excludes fraud detection and fraud-loss measurement; reversals, refunds, chargebacks, and net settlement accounting; revenue, fee income, margin, and profitability; multi-currency conversion; customer lifetime value and customer-level profiling; predictive modelling and causal inference; and SLA/target compliance claims without approved target definitions.

## 11. Approval

The Product Owner approved this baseline on **2026-11-27** under **D-007**. These requirements are implementation authority for the first Payments Performance synthetic data increment. Material changes require Product Owner approval and must be recorded in the decision register.
