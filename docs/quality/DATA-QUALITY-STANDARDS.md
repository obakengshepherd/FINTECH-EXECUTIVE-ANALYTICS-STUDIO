# Data Quality Standards

**Status:** Baseline standard approved in principle; case-specific rules to be refined during design

## 1. Purpose

Ensure analytical outputs are based on data that has been assessed, qualified, and validated. Data quality must be evaluated before results are treated as decision-support evidence.

## 2. Quality dimensions

| Dimension | Meaning | Example control |
|---|---|---|
| Completeness | Required values are present | Required transaction identifiers and timestamps are populated |
| Uniqueness | Records meet the defined uniqueness rule | No duplicate attempt identifier |
| Validity | Values conform to accepted domains and ranges | Amount and status values meet documented rules |
| Consistency | Related representations agree | Status mapping is consistent across datasets |
| Referential integrity | References resolve correctly | Channel and payment-type identifiers exist |
| Timeliness | Events fall within expected time rules | Timestamp and reporting cut-off checks |
| Reconciliation | Totals agree across defined views | Source, SQL, and report counts/values reconcile |

## 3. Required controls

Before analysis:
- Inspect row counts, schema, data types, and date ranges.
- Profile nulls, duplicates, distinct values, and distributions.
- Validate status and reference domains.
- Check referential integrity.
- Identify out-of-range amounts and invalid timestamps.
- Review currency consistency.
- Establish treatment of late-arriving or unresolved records.

Before reporting:
- Reconcile eligible population counts.
- Reconcile successful, failed, and pending totals.
- Recalculate monetary totals independently where practical.
- Test period boundaries and filter behaviour.
- Compare SQL results with Power BI measures.
- Document exclusions and unresolved defects.

## 4. Defects versus business events

Synthetic data may include deliberately injected quality defects to demonstrate detection and treatment. These must be labelled and documented in the generation specification.

A legitimate failed payment, pending payment, or unusual business pattern is not automatically a data-quality defect. Do not silently remove inconvenient records or modify source data to produce a preferred result.

## 5. Issue recording

For each material issue, record:
- Issue identifier.
- Affected dataset and fields.
- Quality dimension.
- Detection method and evidence.
- Affected population/count where known.
- Analytical impact.
- Treatment (correct, exclude, retain with caveat, or investigate).
- Owner/status and resolution evidence.

## 6. Acceptance principle

A query executing successfully does not prove data quality. A KPI is suitable for reporting only when its population, calculation, exclusions, and limitations are documented and validation evidence is available.
