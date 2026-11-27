# AI Handoff — FinTech Executive Analytics Studio

**Last updated:** 2026-11-27  
**Maintainer:** ChatGPT (Primary AI; documentation and integration owner)  
**Authority:** Product Owner  
**Repository:** [obakengshepherd/FINTECH-EXECUTIVE-ANALYTICS-STUDIO](https://github.com/obakengshepherd/FINTECH-EXECUTIVE-ANALYTICS-STUDIO)  
**Governing workflow:** [FNEOS v1.0](AI-COLLABORATION.md)

## 1. Historical baseline and current repository state

- **Historical cutoff:** 2026-11-25.
- **Authoritative historical baseline:** `e795c97d7eec671f47bb64b13178b5d8889db0cb`.
- **Historical status:** Phase 0 ACCEPTED; Phase 1 IN PROGRESS; implementation NOT STARTED.
- **Current main inspected for reset:** `6fe4ffb84717638e99fc6530a0f953a1553b205f` (2026-11-26).
- **Reset outcome:** 26 November AI workflow arrangements are superseded by FNEOS. Their commits remain in history; no history rewriting or deletion is authorised.
- **Working tree:** Local working-tree state is unknown and has not been inspected. Do not infer local status from GitHub.

The 25 November business and foundation baseline remains valid. This reset changes collaboration governance and documentation consistency only; it does not restart the project or approve proposed analytical rules.

## 2. Current project status

- **Foundation:** ACCEPTED by Product Owner.
- **Current phase:** Phase 1 — Business Requirements and KPI Design.
- **Phase 1:** IN PROGRESS.
- **First scenario:** Payments Performance Analytics.
- **Approved toolkit:** SQL Server 2022/T-SQL, Excel, Power BI, Python/pandas where justified.
- **Implementation:** NOT STARTED.
- **Synthetic data modelling:** NOT STARTED; gated on Phase 1 requirements/KPI approval.
- **D-007:** PROPOSED — Product Owner approval required.
- **Analytical requirements:** Proposed; not approved implementation rules.
- **KPI dictionary:** Proposed; not approved implementation rules.

## 3. Authoritative project documents

- `README.md`
- `docs/PROJECT-FOUNDATION.md`
- `docs/PROJECT-ARCHITECTURE.md`
- `docs/IMPLEMENTATION-PLAN.md`
- `docs/DECISIONS.md`
- `docs/AI-COLLABORATION.md`
- `docs/AI-HANDOFF.md`
- `docs/business/PAYMENTS-PERFORMANCE-CASE.md`
- `docs/business/ANALYTICAL-REQUIREMENTS.md`
- `docs/business/KPI-DICTIONARY.md`
- `docs/quality/DATA-QUALITY-STANDARDS.md`

ChatGPT owns modifications to all project documentation. Claude has read/review access unless the Product Owner explicitly transfers ownership of named files.

## 4. Accepted foundation and preserved decisions

- Synthetic financial-services analytics portfolio project; no claim of access to FNB/FirstRand confidential systems or data.
- Payments Performance Analytics is the first scenario.
- SQL Server 2022/T-SQL, Excel, Power BI, and Python/pandas where justified are the approved toolkit.
- The project foundation is accepted; Phase 0 is complete.
- The proposed architecture remains the existing simple analytical-project direction.
- The 25 November requirements, KPI dictionary, analytical case, and data-quality standards are preserved.

## 5. Phase 1 approval gates

The following remain open and must be resolved before synthetic data modelling:
1. Eligible population and attempt grain.
2. Retry, duplicate submission, and duplicate attempt-ID treatment.
3. Status lifecycle and successful/failed/pending/cancelled classification.
4. Pending snapshot, late-arriving outcome, and cancellation treatment.
5. Initiation-time attribution, SAST timezone, and week boundaries.
6. ZAR-only scope and gross successful payment value.
7. Reversal/refund exclusions and monetary interpretation.
8. KPI formulas, denominators, null/zero handling, segmentation, and reconciliation.
9. Required reporting dimensions and management outputs.
10. Data-quality exceptions and validation expectations.

All proposed definitions remain proposed until the Product Owner explicitly approves or revises them. D-007 remains PROPOSED.

## 6. FNEOS operating workflow

1. **ChatGPT — Architecture & Documentation:** requirements, architecture, specifications, documentation, assignments, change control, main governance.
2. **Claude — Specialist Engineering & Code:** independent review by default; assigned code implementation only; returns complete files and exact paths in chat. No GitHub writes, branches, commits, or documentation edits.
3. **User + VS Code + ChatGPT — Assembly & Integration:** user assembles and tests; ChatGPT performs return/alignment checkpoint, resolves issues, integrates approved code into main, and records evidence.

Zero-overlap applies. ChatGPT owns documentation; Claude owns only assigned code files during an active implementation assignment. No branch-based work unless the Product Owner explicitly authorises an exception.

## 7. Specialist review assignment queue

### FEA-REV-001 — Independent review of proposed payment requirements and KPI definitions

- **Assignment mode:** REVIEW ONLY.
- **Assigned AI:** Claude (Specialist AI).
- **Status:** NOT STARTED — assignment prepared; not yet issued.
- **Base repository state:** Latest main commit must be re-inspected immediately before issuing the assignment.
- **Files to inspect:** `docs/business/ANALYTICAL-REQUIREMENTS.md`, `docs/business/KPI-DICTIONARY.md`, `docs/business/PAYMENTS-PERFORMANCE-CASE.md`, `docs/DECISIONS.md`, and `docs/PROJECT-ARCHITECTURE.md`.
- **Files authorised for modification:** NONE.
- **Files excluded from modification:** ALL repository files.
- **Owner:** ChatGPT retains documentation modification ownership; Claude is review-only.
- **Objective:** Independently assess measurement grain, retries, duplicate identifiers, outcome taxonomy, resolved denominators, pending/cancelled treatment, time attribution, SAST boundaries, ZAR scope, gross successful value, reversals/refunds, data-quality edge cases, KPI completeness, and executive interpretability.
- **Required output:** Findings classified as ACCEPTABLE, ACCEPTABLE WITH CONDITIONS, CHANGE RECOMMENDED, or PRODUCT OWNER DECISION REQUIRED. Explain the issue, example/impact, recommended treatment, and whether Product Owner approval is required.
- **Restrictions:** Do not approve D-007, alter business meaning, edit files, design a physical schema, generate data, or implement code.
- **Deliverable:** Review report in Claude's chat response only. No branch, commit, or PR.

## 8. Return/alignment checkpoint status

No Claude review response or local code assembly has been supplied for this reset. Therefore, no specialist findings, local test results, or implementation changes are claimed.

When the user returns with Claude's review or assembled code, ChatGPT must first inspect the latest main and compare the supplied work against its assignment before issuing any subsequent task.

## 9. Next authorised action

Issue FEA-REV-001 to Claude as a REVIEW ONLY assignment after confirming the latest main commit. ChatGPT will then evaluate the review and present any material business-rule/KPI choices to the Product Owner.

**No synthetic data model, database schema, seed data, SQL analysis implementation, or Power BI implementation is authorised until Phase 1 requirements and KPI definitions are explicitly approved.**
