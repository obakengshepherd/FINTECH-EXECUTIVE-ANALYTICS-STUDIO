# AI Handoff — FinTech Executive Analytics Studio

**Last updated:** 2026-11-27  
**Maintainer:** ChatGPT (Primary AI; documentation and integration owner)  
**Authority:** Product Owner  
**Repository:** `obakengshepherd/FINTECH-EXECUTIVE-ANALYTICS-STUDIO`  
**Governing workflow:** [FNEOS v1.1](AI-COLLABORATION.md)

## 1. Verified repository baseline

- **Main SHA before this documentation alignment:** `f24843016754c38c65ed0c44e96d53e14e14a435`.
- **Documentation commits made in this alignment:** specification `e00a19eb3f3f5006484b2932b7e6e897c03d48f7`; implementation log `69b7b6adf67af8bc95a688ba4e27f4be13b124b1`.
- **Latest main must be re-read before Claude begins or ChatGPT integrates any subsequent work.**
- **Historical baseline:** `e795c97d7eec671f47bb64b13178b5d8889db0cb` (2026-11-25).
- **Local working tree:** Not inspected; do not infer local status from GitHub.

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

## 3. Authoritative references

- `docs/DECISIONS.md` — D-007 approved analytical baseline; D-008 FNEOS governance.
- `docs/business/ANALYTICAL-REQUIREMENTS.md` — approved population, status, snapshot, time, currency, exclusions, outputs, validation.
- `docs/business/KPI-DICTIONARY.md` — canonical PAY-001 through PAY-008 definitions.
- `docs/business/PAYMENTS-PERFORMANCE-CASE.md` — approved case specification.
- `docs/quality/DATA-QUALITY-STANDARDS.md` — approved case-specific quality/reconciliation controls.
- `docs/data/FEA-SYN-001-SYNTHETIC-DATASET-SPECIFICATION.md` — detailed field-level dataset contract, generation principles, edge cases, KPI compatibility and acceptance tests.
- `docs/PROJECT-ARCHITECTURE.md` — synthetic source → SQL Server → analysis/validation → Power BI → executive output architecture.
- `docs/IMPLEMENTATION-PLAN.md` — complete Phase 0–7 roadmap and exit criteria.
- `docs/AI-COLLABORATION.md` — active streamlined FNEOS workflow.
- `docs/engineering/IMPLEMENTATION-LOG.md` — actual work, test evidence, decisions and outstanding issues.

## 4. FEA-SYN-001 — Deterministic Synthetic Payments Source Dataset

**Status:** ISSUED — awaiting Claude implementation response  
**Phase:** Phase 2 — Synthetic Data Environment  
**Assigned specialist:** Claude  
**Assignment mode:** One independent review followed by implementation under this same handoff.

### 4.1 Objective

Implement a deterministic, configurable Python generator that creates a clean canonical CSV source population of synthetic payment attempts for the approved twelve-month Payments Performance period and fixed outcome snapshot.

The generated source is fictional. It must not contain real customer, account, card, credential, or confidential banking data. It must not encode a desired analytical conclusion or claim real institutional behaviour.

### 4.2 Binding specification and approved rules

The complete data contract is in `docs/data/FEA-SYN-001-SYNTHETIC-DATASET-SPECIFICATION.md`. Claude must read and follow it alongside D-007 and the approved documents in section 3.

Key parameters:
- Initiation period: 2025-10-01 through 2026-09-30 inclusive.
- Outcome snapshot: 2026-10-31 23:59:59 SAST (UTC+02:00).
- Store timestamps in UTC; use SAST for reporting dates and Monday–Sunday weeks.
- Currency: ZAR only; amount precision: two decimal places.
- Canonical grain: one distinct payment attempt.
- Distinct retry IDs are separate attempts and may share a payment-instruction ID.
- Snapshot outcomes: SUCCESSFUL, FAILED, PENDING, CANCELLED.
- Pending/cancelled are excluded from resolved rates.
- Fixed seed must reproduce byte-for-byte equivalent CSV output.

### 4.3 Exact files Claude may create

1. `src/data_generation/generate_payments.py`
2. `tests/test_generate_payments.py`

**Generated runtime output (not an assigned source file):** `data/generated/payments_attempts.csv`. The generator must create the parent directory when needed. Do not include a generated CSV in the code-file return unless explicitly requested; the user will generate it locally.

### 4.4 Explicitly excluded files and work

- All project documentation, including README, decision register, handoff, roadmap, requirements, KPI dictionary, case, quality standards, architecture, and the new FEA-SYN-001 companion specification.
- SQL schema, SQL load scripts, database objects, SQL queries, Power BI files, Excel workbooks, dashboards, APIs, web applications, cloud infrastructure, and deployment.
- Dependencies beyond the Python standard library.
- Intentional quality-defect injection, test/internal/non-ZAR records, or conflicting duplicate source records. FEA-SYN-001 generates a clean canonical eligible population only; quality-defect scenarios belong to a later separately scoped increment.
- GitHub writes, branches, commits, pull requests, or modifications outside the two assigned files.

### 4.5 Environment and implementation assumptions

- Python 3.11+.
- Standard library only; no network access, external API, secrets, or production connection strings.
- Default target volume: 20,000 attempts, configurable by command-line arguments or a simple documented function interface.
- Use a documented fixed default seed and permit seed override.
- Use Decimal for monetary calculations and serialize two decimal places.
- Use explicit UTC-aware timestamps; convert to SAST only for business reporting derivations.
- A PENDING attempt has no terminal outcome timestamp. Terminal outcome timestamps must not exceed the snapshot and must not precede initiation.
- Use controlled, documented channel and payment-type domains. Failure reason is optional and must be coherent with the outcome.
- Distributions must be plausible and neutral. Do not deliberately create a trend, channel effect, or failure concentration to manufacture an insight.
- Retry generation must be explicit and auditable through shared instruction IDs and distinct attempt IDs.
- Detailed field contract, nullability, timestamp rules, domain constraints, distribution neutrality, edge cases, reconciliations and test expectations are defined in the companion specification.

### 4.6 Required output fields

At minimum:
- `payment_attempt_id`
- `payment_instruction_id`
- `initiated_at_utc`
- `outcome_status_as_of_snapshot`
- `outcome_at_utc` (blank for PENDING)
- `payment_channel`
- `payment_type`
- `amount_zar`

The exact logical types, candidate SQL mappings, requiredness and field contracts are in the companion specification. Do not add customer PII or undocumented columns.

### 4.7 Required behaviour and acceptance criteria

1. Same seed and parameters produce identical ordered rows and byte-stable CSV output.
2. The configured number of canonical attempt rows is generated.
3. Every payment_attempt_id is unique and every instruction ID is non-empty.
4. Genuine retries have distinct attempt IDs and a shared payment_instruction_id.
5. Every record has valid required fields and approved snapshot outcome.
6. Initiation timestamps fall within the inclusive approved SAST period.
7. Timestamps are UTC-aware internally and serialize consistently in UTC.
8. Terminal outcome timestamps are at or before the fixed snapshot and not earlier than initiation; PENDING has a blank outcome timestamp.
9. Monetary amounts are positive, Decimal-exact, and represented to two decimal places.
10. The four snapshot outcome counts sum exactly to the canonical eligible population.
11. Resolved count equals SUCCESSFUL + FAILED; success/failure rates sum to 100% when resolved count is positive; zero resolved count yields undefined/None rather than zero.
12. CSV header and field ordering are stable and documented.
13. Output directory creation and explicit output paths work reliably.
14. Automated tests cover determinism, row count, uniqueness, retry linkage, domains, monetary precision, date boundaries, snapshot/outcome timestamp constraints, KPI reconciliation, and output path handling.
15. Generator and tests run without third-party packages.

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

Claude is to execute the existing FEA-SYN-001 assignment under section 4 and the companion dataset specification. The Product Owner assembles and runs the returned files in VS Code. ChatGPT then performs the single return/alignment checkpoint.

**No SQL schema, database load, SQL analysis, or Power BI implementation is included in FEA-SYN-001.**
