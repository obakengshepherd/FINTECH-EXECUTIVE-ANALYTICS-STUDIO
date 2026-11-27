# FEA-SYN-001 — Synthetic Payments Dataset Specification

**Document ID:** FEA-SYN-001  
**Version:** 1.0  
**Effective:** 2026-11-27  
**Status:** ISSUED — implementation handoff already active  
**Phase:** 2 — Synthetic Data Environment  
**Authority:** Product Owner; D-007 is binding  
**Companion assignment:** `docs/AI-HANDOFF.md`, section 4

## 1. Purpose and scope

Specify the deterministic, clean canonical synthetic source dataset for the first Payments Performance Analytics case. The dataset enables reproducible SQL analysis and KPI reporting without using real customer data or representing actual FNB, FirstRand, or other institutional performance.

This document formalises the data contract for the already-issued FEA-SYN-001 generator. It does not create a second assignment, change its two-file implementation scope, or amend D-007.

**In scope:** one CSV source file, one row per eligible canonical payment attempt, deterministic generation, controlled domains, repeatability, and automated generator tests.

**Out of scope:** defect injection, test/internal or non-ZAR source records, conflicting duplicate source versions, SQL schema/load work, SQL analysis, Power BI, Excel deliverables, APIs, deployment, and production integrations. Those are later increments.

## 2. Binding business rules

The approved requirements and KPI dictionary remain authoritative:
- Initiation period: 2025-10-01 through 2026-09-30 inclusive.
- Fixed initial outcome snapshot: 2026-10-31 23:59:59 SAST (UTC+02:00).
- Store event timestamps in UTC; derive reporting dates and Monday–Sunday weeks in SAST.
- Currency scope is ZAR only; amounts have two decimal places.
- Grain is one distinct payment attempt.
- A genuine retry has a distinct attempt ID and shares its payment-instruction ID with related attempts.
- Snapshot outcome is exactly one of SUCCESSFUL, FAILED, PENDING, CANCELLED.
- Pending and cancelled are excluded from resolved success/failure denominators.
- Resolved = successful + failed. Rates are NULL when resolved is zero.
- Gross Successful Attempt Value is the sum of eligible successful attempt amounts, not revenue, fees, profit, net settlement, or unique instruction value.
- No later outcome may silently rewrite the fixed initial snapshot.

No KPI formula, denominator, population rule, exclusion, or business interpretation is changed here.

## 3. Entities, grain and relationships

### 3.1 Payment instruction

A fictional payment instruction represents the business instruction from which one or more payment attempts may arise. It is represented in this source file by `payment_instruction_id`; it is not a separate row or separate CSV in this increment.

### 3.2 Payment attempt

A payment attempt is one execution attempt associated with an instruction.

- **Grain:** one row per distinct canonical payment attempt.
- **Primary key:** `payment_attempt_id`.
- **Parent relationship:** many attempts may reference the same `payment_instruction_id`.
- **Retry rule:** a retry must have a new `payment_attempt_id`; it must not be collapsed into the preceding attempt.
- **Uniqueness:** `payment_attempt_id` is unique across all output rows.
- **No inferred deduplication:** similar amounts or timestamps are not sufficient to merge attempts.

### 3.3 Controlled reference domains

Payment channel, payment type and outcome status are controlled categorical attributes on the attempt record. Their allowed values must be declared centrally in the generator and documented in its module help. The initial implementation may use compact, realistic fictional domain values, but must not imply that they are official FirstRand/FNB taxonomies.

No customer, account, card, beneficiary, credential, or other personally identifying entity is required.

## 4. CSV data contract

Output path: `data/generated/payments_attempts.csv`  
Encoding: UTF-8  
Delimiter: comma  
Header: required  
Column order: fixed and deterministic  
Null representation: empty field only where explicitly nullable  
Rows: exactly the configured number of canonical attempts (default 20,000)

| Field | Logical type | Required | Contract |
|---|---|---:|---|
| `payment_attempt_id` | String / SQL candidate `varchar(40)` | Yes | Stable unique synthetic identifier; primary key |
| `payment_instruction_id` | String / SQL candidate `varchar(40)` | Yes | Stable synthetic instruction identifier; shared by genuine retries |
| `initiated_at_utc` | UTC timestamp / SQL candidate `datetime2(0)` | Yes | ISO-8601 UTC timestamp; initiation instant |
| `outcome_status_as_of_snapshot` | String / SQL candidate `varchar(12)` | Yes | Exactly SUCCESSFUL, FAILED, PENDING or CANCELLED |
| `outcome_at_utc` | Nullable UTC timestamp / SQL candidate `datetime2(0)` | Conditional | Required for terminal outcomes; blank for PENDING |
| `payment_channel` | Controlled string / SQL candidate `varchar(30)` | Yes | Value from documented channel domain |
| `payment_type` | Controlled string / SQL candidate `varchar(30)` | Yes | Value from documented payment-type domain |
| `amount_zar` | Decimal(18,2) logical / SQL candidate `decimal(18,2)` | Yes | Positive ZAR amount, serialized with exactly two fractional digits |

SQL types above are mapping guidance for a later schema design, not a SQL implementation instruction in this increment. CSV values must parse losslessly to the stated logical types. Monetary calculations must use Python `Decimal`, never binary floating-point arithmetic.

The `amount_zar` field is explicitly ZAR-denominated; a separate currency column is unnecessary in this ZAR-only clean source. Do not add fields unless they are necessary to implement the approved requirements and are documented.

## 5. Time, reporting and snapshot semantics

- All generated timestamps must be timezone-aware internally.
- Serialize timestamps consistently as ISO-8601 UTC (for example, a trailing `Z` or explicit `+00:00`; use one representation throughout the file).
- Every `initiated_at_utc` must fall within the approved inclusive SAST initiation period after conversion from UTC.
- The SAST snapshot instant must be converted correctly to UTC for timestamp comparisons.
- For SUCCESSFUL, FAILED and CANCELLED, `outcome_at_utc` must be present, not earlier than initiation, and not later than the fixed snapshot.
- For PENDING, `outcome_at_utc` must be empty. Pending means no terminal outcome was available at the snapshot.
- Do not create an outcome after the snapshot and then label it as the initial snapshot outcome.
- Reporting date and reporting week are derived analytical attributes, not required source columns. Derive them from initiation time after conversion to SAST. Weeks begin Monday and end Sunday in SAST.

## 6. Synthetic generation principles and distributions

### 6.1 Reproducibility

- Use a documented fixed default seed; allow a caller-supplied seed.
- Same seed and same parameters must produce identical ordered rows and byte-stable CSV output.
- Keep generation independent of network access, machine-local current time, and external services.
- Stable ordering must be defined (for example, deterministic attempt sequence/order).

### 6.2 Neutrality and plausibility

- Default target volume is 20,000 attempts and must be configurable.
- Populate the entire approved twelve-month initiation period; do not cluster all records into a small number of dates.
- Use multiple values from each controlled channel and payment-type domain.
- Use a varied, positive, right-skew-friendly amount distribution with two-decimal precision; do not present the generated values as observed market or bank data.
- Include a mix of all four outcome statuses where compatible with the configured population, but do not hardcode KPI targets or tune probabilities to achieve a preferred success rate.
- Generate a modest, explicit share of retry instructions, with distinct attempt IDs and shared instruction IDs. Document the chosen generation parameters in code/help.
- Avoid deliberate trends, seasonal effects, channel effects, payment-type effects, failure concentrations, or causal stories. Random variation is acceptable; manufactured findings are not.
- The generator may expose deterministic parameters for volume/seed/output path. It must not expose business-rule overrides that silently alter D-007.

There are no approved target percentages for outcome mix, channel share, payment-type share, retry share, or payment amount distribution. Implementation choices for these distributions are technical generation assumptions, not business facts; document them as such and do not treat them as actual institutional benchmarks.

## 7. Edge cases and expected treatment

| Condition | FEA-SYN-001 treatment |
|---|---|
| First attempt for an instruction | New instruction ID and new attempt ID |
| Genuine retry | Reuse instruction ID; generate a new unique attempt ID |
| Pending at snapshot | Status PENDING; outcome timestamp empty |
| Terminal outcome | Timestamp present and between initiation and snapshot inclusive |
| Initiation at period boundary | Include if within the inclusive SAST date/time period |
| Initiation outside period | Must not appear in clean output |
| Outcome after snapshot | Must not appear as a terminal outcome in this snapshot dataset |
| Zero or negative amount | Invalid; generator must not emit |
| More than two monetary decimals | Invalid; generator must not emit |
| Unknown status/domain value | Invalid; generator must not emit |
| Duplicate attempt ID | Invalid; generator must not emit |
| Same instruction ID across attempts | Valid only as explicit retry linkage |
| Empty required field | Invalid; generator must not emit |
| Empty outcome timestamp for non-pending | Invalid |
| Populations with zero resolved attempts | KPI rates remain undefined/NULL; tests of rate logic must not substitute zero |

The clean generator does not simulate duplicate ingestion, conflicting identifiers, invalid statuses, test records, internal records, or non-ZAR exclusions. Those cases are reserved for a separately specified quality demonstration.

## 8. KPI compatibility and reconciliation

The generated source must support the approved PAY-001 through PAY-008 measures without changing their definitions:

- PAY-001: count canonical attempt rows.
- PAY-002/003/004/008: count the four mutually exclusive snapshot outcomes.
- Resolved supporting measure: SUCCESSFUL + FAILED.
- PAY-005/006: calculate rates using resolved attempts only; return NULL/None for a zero denominator.
- PAY-007: sum `amount_zar` for SUCCESSFUL attempts only.

Required population reconciliation:

`Total Attempts = Successful + Failed + Pending + Cancelled`

Required resolved reconciliation:

`Resolved = Successful + Failed`

When resolved is positive:

`Success Rate + Failure Rate = 100%`

Gross successful attempt value must equal an independent Decimal sum of successful attempt amounts. Retries count as separate attempts and may each contribute if successful.

Quality exclusions and duplicate/quarantine counts are not represented in this clean canonical CSV and must not be fabricated as zero-valued operational findings. They are addressed in later quality work.

## 9. Validation and acceptance tests

Automated standard-library tests must cover:

1. Same seed and parameters produce byte-identical CSV output.
2. Different seeds can produce different output while preserving all invariants.
3. Configured row count is exact; default is 20,000.
4. Attempt IDs are unique and non-empty.
5. Instruction IDs are non-empty; retry relationships are valid and testable.
6. All required columns exist in the documented order; no undocumented columns appear.
7. Channel, payment type and status values belong to declared domains.
8. Initiation timestamps parse as UTC and fall within the approved inclusive SAST period.
9. Terminal outcome timestamps parse as UTC, are not before initiation and do not exceed the snapshot.
10. PENDING rows have an empty outcome timestamp; terminal statuses have one.
11. Amounts parse as Decimal, are positive, and have exactly two decimal places.
12. All four outcome counts reconcile to total rows.
13. Resolved count equals successful plus failed.
14. Success and failure rates sum to 100% for positive resolved counts; zero denominator is represented as None/NULL.
15. Gross successful attempt value reconciles to an independent Decimal sum.
16. Output directory creation and explicit output path work without relying on the current working directory.
17. The generator and tests run using Python 3.11+ standard library only.

Acceptance requires complete code files, exact local commands, actual test results clearly distinguished from unrun tests, and a generation summary. No test may be reported as passed unless it was executed.

## 10. Implementation boundary and handoff

Claude's exact assigned source files remain:
1. `src/data_generation/generate_payments.py`
2. `tests/test_generate_payments.py`

Runtime output remains `data/generated/payments_attempts.csv`.

Claude must follow this document together with D-007, the approved requirements, KPI dictionary, quality standards and the existing FEA-SYN-001 handoff. The one-review-then-implement rule remains in force. Claude may not modify documentation, SQL, Power BI, or any unassigned files.

The next phase after accepted generator output is a separately bounded minimal SQL Server relational model and loading increment. It is not part of FEA-SYN-001.

## 11. Approval and change control

This specification operationalises the already-approved D-007 baseline and existing FEA-SYN-001 assignment. It does not amend D-007. Any change to KPI meaning, population, denominator, snapshot, time attribution, currency scope, or exclusion rules requires explicit Product Owner approval and a recorded decision. Routine technical implementation choices within this contract do not require another approval loop.
