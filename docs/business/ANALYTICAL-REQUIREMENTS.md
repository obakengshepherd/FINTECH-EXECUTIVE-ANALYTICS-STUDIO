# Analytical Requirements — Payments Performance

**Version:** 0.1  
**Status:** PROPOSED — Product Owner approval required  
**Phase:** 1 — Business Requirements and KPI Design  
**Business owner:** Fictional Payments Operations Manager  
**Analytical owner:** Project Data Analyst

## 1. Business objective

Provide Payments Operations management with a consistent weekly view of payment-attempt volumes and outcomes, successful payment value, and differences across payment channels and payment types. The report should identify where performance has changed and where further investigation may be warranted.

The analysis is descriptive and diagnostic. It does not, by itself, establish causes or prove that a channel, payment type, or operational factor caused an outcome.

## 2. Decisions the analysis should support

The outputs should help a manager:
- Understand payment-attempt volume and outcome mix over time.
- Monitor the proportion of resolved attempts that succeed or fail.
- Identify weeks or segments with material observed changes.
- Understand the volume and value context behind rate movements.
- Identify pending items for operational follow-up.
- Decide which patterns warrant further investigation.

The analysis will not prescribe operational targets or SLA breaches until a business-approved target and measurement rule exist.

## 3. Population and grain

**Proposed grain:** One row per distinct payment attempt.

**Proposed eligible population:** Initiated payment attempts in the selected reporting period, excluding explicitly identified test/internal records and records that fail mandatory identity or validity checks. Exclusions must be counted and reported; they must not be silently discarded.

A payment instruction may have more than one attempt. Each genuine retry with a distinct attempt identifier is counted as a separate attempt. A repeated copy of the same attempt identifier is a duplicate ingestion/data-quality issue and must not be counted twice. Similar amounts or timestamps alone are insufficient evidence to deduplicate two attempts.

The data model should retain a payment-instruction identifier to support optional instruction-level analysis, while the initial operational KPIs remain attempt-based.

## 4. Proposed outcome model

Each attempt has one reporting outcome as of a documented data snapshot:
- **Successful:** payment attempt completed successfully.
- **Failed:** payment attempt reached a defined failure outcome.
- **Pending:** no terminal outcome is available at the snapshot cut-off.
- **Cancelled:** attempt was cancelled before a successful or failed terminal outcome.

These categories must be mutually exclusive at the reporting snapshot. The detailed synthetic status mapping and transition assumptions must be documented before data generation.

Pending and cancelled attempts are reported separately and excluded from the resolved success/failure denominator. Reversals and refunds are post-success financial adjustments and are outside the initial scenario; therefore, successful payment value is proposed as gross successful attempt value, not net settlement value.

## 5. Time attribution and reporting cadence

**Proposed time attribution:** Cohort attempts by their initiation timestamp, not by the timestamp at which a later outcome was recorded. This keeps the attempt population anchored to when the payment was initiated.

**Proposed business timezone:** South African Standard Time (SAST, UTC+02:00). Reporting date and week boundaries must use this business timezone consistently.

**Proposed reporting cadence:** Weekly trend reporting, with Monday–Sunday reporting weeks. A monthly summary may be included as a roll-up, not as a separate KPI definition.

**Proposed history:** Twelve complete calendar months, with the exact start/end dates and snapshot cut-off recorded in each analysis. Late outcomes and restatements must be handled using an explicit snapshot/as-of rule; they must not silently rewrite previously published periods.

## 6. Currency and monetary scope

**Proposed initial scope:** ZAR-only synthetic transactions. No foreign-exchange conversion or cross-currency aggregation is required in the first release.

Successful Payment Value is the gross sum of amounts on eligible successful attempts. It is not a measure of revenue, fees, profit, or net settlement.

## 7. Dimensions

Initial required dimensions:
- Reporting week/date.
- Payment channel.
- Payment type.
- Outcome status.

Failure reason may be included as a descriptive dimension if its definitions are controlled and sufficiently populated. Customer-level analysis is not required for the first release.

Segmented rates must always be presented with their attempt and resolved denominators. Small populations should be flagged for cautious interpretation; no arbitrary minimum-volume threshold is imposed in this proposal.

## 8. Required analytical outputs

1. Weekly payment-attempt volume and outcome counts.
2. Weekly resolved success and failure rates.
3. Weekly gross successful payment value in ZAR.
4. Outcome mix including pending and cancelled attempts.
5. Channel and payment-type comparisons with denominators.
6. Data-quality and exclusion summary.
7. Concise executive insight brief documenting findings, limitations, interpretation, and recommendations.

## 9. Validation and reconciliation requirements

- Attempt identifiers are unique in the canonical attempt population.
- Status categories are valid, mutually exclusive, and exhaustive for the reported snapshot.
- Successful + failed + pending + cancelled counts reconcile to the eligible attempt population.
- Resolved attempts equal successful + failed attempts.
- Success and failure rates sum to 100% when the resolved denominator is positive.
- Gross successful value reconciles to the sum of eligible successful attempt amounts in ZAR.
- Weekly boundaries and SAST date attribution are tested.
- SQL and Power BI outputs reconcile for identical populations, dates, and filters.
- Excluded test/internal and invalid records are quantified and documented.

## 10. Explicit exclusions

The first scenario excludes:
- Fraud detection and fraud-loss measurement.
- Reversals, refunds, chargebacks, and net settlement accounting.
- Revenue, fee income, margin, and profitability.
- Multi-currency conversion.
- Customer lifetime value and customer-level profiling.
- Predictive modelling and causal inference.
- SLA or target compliance claims without approved target definitions.

## 11. Open business-rule approvals

The Product Owner must confirm or revise the proposals for:
1. Attempt grain and retry treatment.
2. Duplicate identifier handling.
3. Status definitions and cancelled-attempt treatment.
4. Pending-at-snapshot treatment and late-arriving outcomes.
5. Initiation-time cohorting and SAST week boundaries.
6. Twelve complete months of ZAR-only data.
7. Gross successful value and exclusion of reversals/refunds.
8. Initial dimensions and reporting outputs.

Until approval, these rules remain proposed and must not be treated as implemented requirements.
