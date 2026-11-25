# Payments Performance Analytics — Case Specification

**Status:** Case baseline accepted; detailed requirements proposed in `ANALYTICAL-REQUIREMENTS.md` and awaiting Product Owner approval  
**Stakeholder:** Fictional Payments Operations Manager  
**Environment:** Synthetic South African financial institution

## 1. Business context

Management needs a consistent view of payment activity and outcomes over time. The analysis should help identify changes in payment volumes, resolved outcomes, and successful payment value, and highlight segments that may warrant further investigation.

This is a fictional business scenario. It does not describe actual FNB or FirstRand operations.

## 2. Primary business question

How is payment performance changing over time, and where should management investigate potential operational issues?

## 3. Initial analytical questions

- How many payment attempts occurred in the reporting period?
- How many attempts reached successful, failed, or pending states?
- What is the success rate among resolved attempts?
- How does the failure rate change over time?
- What is the value of successful payments?
- Do outcomes differ across payment channels or payment types?
- Are there unusual movements that warrant investigation?

## 4. Proposed population and grain

- **Population:** Eligible payment attempts recorded during the approved measurement period.
- **Grain:** One row per payment attempt, subject to confirmation during data design.
- **Period:** A proposed 12-month synthetic history; exact dates and reporting cut-offs to be approved during Phase 1.
- **Currency:** Currency must be explicit. ZAR may be the initial scenario currency; aggregation across currencies must not occur without a defined conversion policy.

## 5. Status treatment

The initial conceptual categories are successful, failed, and pending/unresolved. The detailed status lifecycle, terminal states, reversals, retries, cancellations, and duplicate attempts must be clarified before KPI implementation.

Pending records should be reported separately and excluded from resolved-outcome rates unless an approved business rule specifies otherwise.

## 6. Initial measures

- Total eligible payment attempts.
- Successful attempts.
- Failed attempts.
- Pending/unresolved attempts.
- Successful payment value.
- Resolved payment success rate.
- Resolved payment failure rate.

All measures remain subject to final KPI definitions and population rules.

## 7. Segmentation

Channel and payment type are candidate dimensions. Segment comparisons should include denominators and relevant volumes; small populations must be clearly identified to avoid overinterpreting unstable rates.

## 8. Outputs

- Requirements and KPI specification.
- Data-quality assessment.
- Reproducible SQL analysis.
- Reconciliation evidence.
- Power BI report.
- Executive insight brief.

## 9. Limitations and interpretation

Descriptive patterns do not establish causes. A segment with a higher observed failure rate is an investigation lead, not proof that the segment caused failures. Findings must identify the measurement period, population, exclusions, data limitations, and validation performed.

## 10. Phase 1 requirements

See [`ANALYTICAL-REQUIREMENTS.md`](ANALYTICAL-REQUIREMENTS.md) for the detailed proposed population, attempt grain, status treatment, time attribution, currency scope, dimensions, outputs, exclusions, and validation requirements.

## 11. Open questions for Product Owner approval

1. What exact business decision should the report support?
2. What counts as an eligible payment attempt?
3. How are retries and duplicate submissions treated?
4. Which statuses are terminal, and how are pending items aged?
5. Are reversals and refunds in scope?
6. What is the authoritative event timestamp?
7. Are multiple currencies included?
8. What reporting frequency and comparison baseline are useful?
9. Which segment dimensions are required?
10. What thresholds, if any, are approved by the business rather than inferred from the data?
