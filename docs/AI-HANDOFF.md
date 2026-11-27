# AI Handoff — FinTech Executive Analytics Studio

**Last updated:** 2026-11-27  
**Maintainer:** ChatGPT (Primary AI; documentation and integration owner)  
**Authority:** Product Owner  
**Repository:** `obakengshepherd/FINTECH-EXECUTIVE-ANALYTICS-STUDIO`  
**Governing workflow:** [FNEOS v1.1](AI-COLLABORATION.md)

## 1. Verified repository baseline

- **Latest main inspected before this documentation update:** `128819849aeb7b0dea741e05067a2c3691d20f0b`.
- **Historical baseline:** `e795c97d7eec671f47bb64b13178b5d8889db0cb` (2026-11-25).
- **Local working tree:** Not inspected; do not infer local status from GitHub.
- **Current documentation commit:** To be recorded after this update is committed and verified.

The historical project baseline and accepted foundation are preserved. The 26 November workflow arrangements remain in history but are superseded where inconsistent with active FNEOS.

## 2. Current project status

- **Foundation / Phase 0:** ACCEPTED.
- **Business requirements and KPI design / Phase 1:** ACCEPTED on 2026-11-27 under D-007.
- **Synthetic data environment / Phase 2:** IN PROGRESS.
- **Implementation:** NOT STARTED; Claude has been issued FEA-SYN-001 but has not yet returned code.
- **First scenario:** Payments Performance Analytics.
- **Approved toolkit:** SQL Server 2022/T-SQL, Excel, Power BI, Python where justified.
- **D-007:** ACCEPTED.
- **D-008:** ACCEPTED.
- **Active increment:** FEA-SYN-001 — Deterministic Synthetic Payments Source Dataset.

## 3. Authoritative approved references

- `docs/DECISIONS.md` — D-007 approved analytical baseline; D-008 FNEOS governance.
- `docs/business/ANALYTICAL-REQUIREMENTS.md` — approved population, status, snapshot, time, currency, exclusions, outputs, validation.
- `docs/business/KPI-DICTIONARY.md` — canonical PAY-001 through PAY-008 definitions.
- `docs/business/PAYMENTS-PERFORMANCE-CASE.md` — approved case specification.
- `docs/quality/DATA-QUALITY-STANDARDS.md` — approved case-specific quality/reconciliation controls.
- `docs/PROJECT-ARCHITECTURE.md` — simple synthetic-source → SQL Server → analysis/validation → Power BI → executive output architecture.
- `docs/IMPLEMENTATION-PLAN.md` — phase status and exit criteria.
- `docs/AI-COLLABORATION.md` — active streamlined FNEOS workflow.

## 4. FEA-SYN-001 — Deterministic Synthetic Payments Source Dataset

**Status:** ISSUED — awaiting Claude implementation response  
**Phase:** Phase 2 — Synthetic Data Environment  
**Base main SHA:** `128819849aeb7b0dea741e05067a2c3691d20f0b`  
**Assigned specialist:** Claude  
**Assignment mode:** One independent review followed by implementation under this same handoff.

### 4.1 Objective

Implement a deterministic, configurable Python generator that creates a clean canonical CSV source population of synthetic payment attempts for the approved twelve-month Payments Performance period and fixed outcome snapshot.

The generated source is fictional. It must not contain real customer, account, card, credential, or confidential banking data. It must not encode a desired analytical conclusion or claim real institutional behaviour.

### 4.2 Approved rules and references

Follow D-007 and the approved documents in section 3. Key parameters:
- Initiation period: 2025-10-01 through 2026-09-30 inclusive.
- Outcome snapshot: 2026-10-31 23:59:59 SAST (UTC+02:00).
- Store timestamps in UTC; use SAST for reporting dates and Monday–Sunday weeks.
- Currency: ZAR only; amount precision: two decimal places.
- Canonical grain: one distinct payment attempt.
- Distinct retry IDs are separate attempts and may share a payment-instruction ID.
- Snapshot outcomes: SUCCESSFUL, FAILED, PENDING, CANCELLED.
- Pending/cancelled are excluded from resolved rates.
- Fixed seed must reproduce byte-for-byte equivalent logical output.

### 4.3 Exact files Claude may create

1. `src/data_generation/generate_payments.py`
2. `tests/test_generate_payments.py`

**Generated runtime output (not an assigned source file):** `data/generated/payments_attempts.csv`. The generator must create the parent directory when needed. Do not include a generated CSV in the code-file return unless explicitly requested; the user will generate it locally.

### 4.4 Explicitly excluded files and work

- All project documentation, including README, decision register, handoff, roadmap, requirements, KPI dictionary, case, quality standards, and architecture.
- SQL schema, SQL load scripts, database objects, SQL queries, Power BI files, Excel workbooks, dashboards, APIs, web applications, cloud infrastructure, and deployment.
- Dependencies beyond the Python standard library.
- Intentional quality-defect injection, test/internal/non-ZAR records, or conflicting duplicate source records. FEA-SYN-001 generates a clean canonical eligible population; quality-defect scenarios belong to a later separately scoped increment.
- GitHub writes, branches, commits, pull requests, or modifications outside the two assigned files.

### 4.5 Environment and implementation assumptions

- Python 3.11+.
- Standard library only (for example: csv, datetime, decimal, pathlib, random, argparse, zoneinfo, unittest).
- No network access, external API, secrets, or production connection strings.
- Default target volume: 20,000 attempts, configurable by command-line arguments or a simple documented function interface.
- Use a documented fixed default seed and permit seed override.
- Use Decimal for monetary calculations and serialize two decimal places.
- Use explicit UTC-aware timestamps; convert to SAST only for business reporting derivations.
- Model outcome status as observed at the approved snapshot. A PENDING attempt has no terminal outcome timestamp. Terminal outcome timestamps must not exceed the snapshot and must not precede initiation.
- Use controlled, documented channel and payment-type domains. Failure reason is optional and must be coherent with the outcome.
- Distributions should be plausible and varied, but neutral: do not deliberately create a trend, channel effect, or failure concentration to manufacture an insight.
- Retry generation must be explicit and auditable through shared instruction IDs and distinct attempt IDs.

### 4.6 Expected output fields

At minimum:
- `payment_attempt_id`
- `payment_instruction_id`
- `initiated_at_utc`
- `outcome_status_as_of_snapshot`
- `outcome_at_utc` (blank for PENDING)
- `payment_channel`
- `payment_type`
- `amount_zar`

Additional fields are allowed only when justified by the approved analytical requirements (for example, controlled failure reason). Document every field and its meaning in the generator's module documentation or CLI help; do not add customer PII.

### 4.7 Required behaviour and acceptance criteria

1. Running with the same seed and parameters produces identical logical rows and stable CSV output.
2. The configured number of canonical attempt rows is generated.
3. Every payment_attempt_id is unique.
4. Genuine retries have distinct attempt IDs and a shared payment_instruction_id.
5. Every record has a valid instruction ID, channel, payment type, timestamp, ZAR amount, and approved snapshot outcome.
6. Initiation timestamps fall within the inclusive approved period.
7. Timestamps are UTC-aware in the generator's internal representation and serialize consistently in UTC.
8. Outcome timestamps for terminal outcomes are at or before the fixed snapshot and not earlier than initiation; PENDING has a blank outcome timestamp.
9. Monetary amounts are positive, represented to two decimal places, and parseable as exact decimal values.
10. The four snapshot outcome counts sum exactly to the canonical eligible population.
11. Resolved count equals SUCCESSFUL + FAILED; success/failure rates sum to 100% when resolved count is positive; zero resolved count yields undefined/None rather than zero.
12. CSV header and field ordering are stable and documented.
13. Output directory is configurable or safely defaulted to the repository-relative generated-data path.
14. Automated tests cover determinism, row count, uniqueness, retry linkage, domains, monetary precision, date boundaries, snapshot/outcome timestamp constraints, and reconciliation.
15. The generator runs without third-party packages.

### 4.8 Required commands and expected outcomes

Claude must provide exact commands for:
- Running the generator with default parameters.
- Running with an explicit seed and output path.
- Running automated tests using the standard library test runner.

Expected outcomes:
- Generator exits successfully and writes the requested CSV.
- The same seed/configuration yields identical output.
- All automated tests pass.
- A concise generation summary reports row count, outcome counts, date range, snapshot, and output path. Do not report invented results; clearly label any expected sample output as illustrative.

### 4.9 Complete-file return and VS Code assembly

Return the complete contents of both assigned files in Claude's chat, each preceded by its exact repository-relative path. Do not return partial snippets or diffs as a substitute.

Then provide:
1. Implementation explanation and assumptions.
2. Python version/dependency statement.
3. VS Code instructions to create the two files at the exact paths.
4. Exact PowerShell commands from the repository root.
5. Expected console summary and test outcome.
6. Actual tests Claude ran, clearly distinguished from tests the user must run locally.
7. Known limitations and any non-blocking observations.

### 4.10 One-review rule and stop conditions

First perform one independent review of the approved design and this handoff. Then:
- If findings are NON-BLOCKING, document them briefly and proceed with implementation without another review cycle.
- If a genuine BLOCKING issue prevents correct implementation, stop only the affected part and report exact issue, impact, and proposed resolution.
- If a PRODUCT OWNER DECISION is genuinely necessary because the approved business meaning, architecture, security, or data integrity boundary would change, stop and request that precise decision.
- Do not reopen settled D-007 rules or request approval for routine implementation details within this scope.
- If no blocker exists, do not wait for another confirmation; implement and return the files.

## 5. Return/alignment checkpoint

When the user returns with Claude's response or local assembly evidence, ChatGPT must inspect latest main, compare the returned files against FEA-SYN-001, review actual VS Code test results, and identify defects/omissions before the next increment. No local working-tree state or test result is assumed until supplied.

## 6. Next action

Claude is to execute FEA-SYN-001 under section 4. The Product Owner assembles and runs the returned files in VS Code. ChatGPT then performs the single return/alignment checkpoint.

**No SQL schema, database load, SQL analysis, or Power BI implementation is included in FEA-SYN-001.**
