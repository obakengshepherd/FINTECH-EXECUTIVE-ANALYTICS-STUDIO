# Payments Performance Analytics — Case Specification

**Status:** Case baseline and detailed analytical requirements APPROVED — 2026-11-27  
**Decision:** D-007  
**Stakeholder:** Fictional Payments Operations Manager  
**Environment:** Synthetic South African financial institution

## 1. Business context

Management needs a consistent view of payment activity and outcomes over time. The analysis should help identify changes in payment volumes, resolved outcomes, and gross successful attempt value, and highlight segments that may warrant further investigation.

This is a fictional business scenario. It does not describe actual FNB or FirstRand operations.

## 2. Primary business question

How is payment performance changing over time, and where should management investigate potential operational issues?

## 3. Initial analytical questions

- How many eligible payment attempts occurred in the reporting period?
- How many attempts were successful, failed, pending, or cancelled at the snapshot?
- What is the success rate among resolved attempts?
- How does the failure rate change over time?
- What is the gross value of successful attempts?
- Do outcomes differ across payment channels or payment types?
- Are there unusual movements that warrant investigation?

## 4. Approved population and grain

- **Grain:** One canonical row per distinct payment attempt.
- **Retries:** A genuine retry with a distinct attempt ID is a separate attempt; retain the instruction ID to associate attempts.
- **Duplicates:** Identical duplicate copies count once and are quantified. Conflicting payloads for the same attempt ID are quarantined and excluded.
- **Eligible population:** Valid, non-test/internal, ZAR-denominated attempts initiated from 2025-10-01 through 2026-09-30 inclusive.
- **Snapshot:** 2026-10-31 23:59:59 SAST.
- **Exclusions:** Test/internal, invalid mandatory identity/validity, unknown/missing/invalid/conflicting status, conflicting attempt ID, and non-ZAR records; all exclusions are quantified.

## 5. Approved status treatment

At the fixed snapshot, every eligible attempt has one outcome: SUCCESSFUL, FAILED, PENDING, or CANCELLED. Pending and cancelled are reported separately and excluded from resolved-outcome rates. Resolved attempts are successful plus failed attempts. A later snapshot is separately identified and does not silently rewrite this initial snapshot.

## 6. Approved measures

See the canonical [KPI dictionary](KPI-DICTIONARY.md): PAY-001 through PAY-008, including resolved success/failure rates and gross successful attempt value in ZAR.

## 7. Time and currency

Store event timestamps in UTC. Derive reporting dates and Monday–Sunday weeks in SAST (UTC+02:00). Attribute attempts by initiation time. The initial population is ZAR-only; no FX conversion is performed. Amounts use two decimal places.

## 8. Segmentation and outputs

Required dimensions: reporting date/week, payment channel, payment type, and outcome status. Failure reason is optional when controlled and sufficiently populated.

Outputs: weekly attempt volumes/outcome counts; resolved success/failure rates; gross successful attempt value; outcome mix; channel/payment-type comparisons with denominators; quality/exclusion summary; and a concise executive insight brief.

## 9. Limitations and interpretation

Descriptive patterns do not establish causes. A segment with a higher observed failure rate is an investigation lead, not proof that the segment caused failures. Findings must identify the measurement period, population, snapshot, exclusions, data limitations, and validation performed.

## 10. Exclusions

Fraud/fraud-loss, reversals, refunds, chargebacks, net settlement, revenue/fees/profitability, FX conversion, customer profiling/lifetime value, predictive modelling, causal inference, and unsupported SLA/target compliance are outside this first case.

## 11. Approval

The Product Owner approved the detailed case and analytical baseline on 2026-11-27 under D-007. The approved documents are implementation authority for FEA-SYN-001.
