# Data Quality Standards

**Status:** Baseline standard approved in principle; Payments Performance controls approved under D-007 on 2026-11-27.

## 1. Purpose

Ensure analytical outputs are based on data that has been assessed, qualified, and validated. Data quality must be evaluated before results are treated as decision-support evidence.

## 2. Quality dimensions

| Dimension | Meaning | Example control |
|---|---|---|
| Completeness | Required values are present | Required attempt/instruction identifiers and timestamps are populated |
| Uniqueness | Records meet the defined uniqueness rule | One canonical record per attempt ID |
| Validity | Values conform to accepted domains and ranges | Amount, currency, timestamp, and status values meet approved rules |
| Consistency | Related representations agree | Status mapping and retry relationships are consistent |
| Referential integrity | References resolve correctly | Channel and payment-type values exist in controlled domains |
| Timeliness | Events fall within expected time rules | Timestamp and snapshot cut-off checks |
| Reconciliation | Totals agree across defined views | Source, SQL, and report counts/values reconcile |

## 3. Payments Performance controls

- Canonical grain is one distinct payment attempt.
- Identical duplicate copies of an attempt ID/payload count once and are quantified.
- Conflicting payloads sharing an attempt ID are quarantined and excluded; all affected records are quantified.
- Explicit test/internal records, invalid mandatory identity/validity records, unknown/missing/invalid/conflicting statuses, and non-ZAR records are excluded from the eligible KPI population and quantified.
- Eligible snapshot outcomes are SUCCESSFUL, FAILED, PENDING, and CANCELLED; these categories are mutually exclusive and exhaustive for eligible canonical attempts.
- Successful + failed + pending + cancelled must reconcile exactly to eligible canonical attempts.
- Resolved attempts equal successful + failed.
- Success and failure rates sum to 100% when the resolved denominator is positive; rates are NULL when it is zero.
- Gross successful attempt value reconciles to eligible successful ZAR amounts.
- UTC-to-SAST conversion and Monday–Sunday reporting-week boundaries are tested.
- SQL and Power BI outputs reconcile for identical populations and filters.

## 4. Controls before analysis

- Inspect row counts, schema, data types, and date ranges.
- Profile nulls, duplicates, distinct values, and distributions.
- Validate status and reference domains.
- Check referential integrity.
- Identify out-of-range amounts and invalid timestamps.
- Review currency consistency.
- Establish the applicable snapshot and treatment of unresolved/late-arriving records.

## 5. Defects versus business events

Synthetic data may include deliberately injected quality defects in a separately controlled increment. Such defects must be labelled and documented in the generation specification.

A legitimate failed, pending, or cancelled payment is not automatically a data-quality defect. Do not silently remove inconvenient records or modify source data to produce a preferred result. FEA-SYN-001 creates a clean canonical eligible source population; deliberate defect injection and exclusion demonstrations are deferred to a separately specified increment.

## 6. Issue recording

For each material issue, record issue identifier, affected dataset/fields, quality dimension, detection method/evidence, affected population/count, analytical impact, treatment, owner/status, and resolution evidence.

## 7. Acceptance principle

A query executing successfully does not prove data quality. A KPI is suitable for reporting only when its population, calculation, exclusions, and limitations are documented and validation evidence is available.
