# AI Collaboration — Four-Nexus Engineering Operating Standard

**Version:** 1.0  
**Authority:** Product Owner  
**Effective reset:** 2026-11-27  
**Historical project cutoff:** 2026-11-25  
**Applies to:** All AI-assisted work in this repository  
**Status:** ACTIVE

## 1. Purpose and authority

This document implements the Product Owner's Four-Nexus Engineering Operating Standard (FNEOS) for FinTech Executive Analytics Studio.

The Product Owner retains final authority over business requirements, project scope, architecture, technology, security boundaries, data integrity rules, material dependencies/infrastructure, and acceptance.

The GitHub repository is the authoritative shared project record. Historical conversations and handoffs are context, not substitutes for repository evidence. Inspect repository state and relevant files before proposing or making changes.

The historical baseline for this governance reset is commit `e795c97d7eec671f47bb64b13178b5d8889db0cb` dated 2026-11-25. Work and workflow arrangements introduced on 2026-11-26 are superseded where they conflict with this standard. Historical commits are preserved; no history rewriting is permitted.

## 2. Mandatory three-stage workflow

### Step 1 — ChatGPT: Architecture and documentation

ChatGPT is the Primary AI and principal architecture, documentation, and integration owner. Responsibilities:
- Own system architecture, business and analytical requirements, technical specifications, and change control.
- Own README and all project documentation, including the decision register, implementation plan, handoff, and assignment specifications.
- Inspect the repository and latest `main` state before changes.
- Prepare explicit Claude review or implementation assignments.
- Maintain main-branch governance and integrate approved code returned through the user.
- Perform return/alignment checkpoints and resolve integration issues.
- Keep project status and evidence accurate.

ChatGPT owns execution of assigned coordination and integration tasks, not project ownership. The Product Owner remains final authority.

### Step 2 — Claude: Specialist engineering and code

Claude is the Specialist AI. Claude:
- Performs independent architecture/technical review by default before implementation.
- Conducts assigned technical investigation, code implementation, debugging, testing, and code-level review.
- Implements only against an explicit, approved assignment and approved architecture/requirements.
- Returns complete code files in its response, with exact repository-relative paths.
- Explains implementation decisions, assumptions, dependencies, tests, actual results, and execution instructions.

Claude may read all repository documentation. Claude must not modify ChatGPT-owned documentation unless the Product Owner explicitly approves an ownership transfer for named files.

Claude MUST NOT push, commit, merge, or directly modify GitHub. Branch-based work is prohibited unless the Product Owner explicitly authorises it. Claude returns code in chat for user assembly; it does not create competing implementations.

### Step 3 — User + VS Code + ChatGPT: Assembly and integration

The user:
- Places Claude's returned files into the local project using VS Code.
- Runs the application, scripts, and tests.
- Supplies actual results, relevant errors, and any changed files/diffs needed for review.

ChatGPT:
- Performs the mandatory return/alignment checkpoint before issuing the next implementation assignment.
- Reviews supplied changes against the approved task, requirements, architecture, and current repository state.
- Identifies omissions, regressions, inconsistencies, and blockers.
- Resolves integration issues with the user.
- Integrates approved changes into `main` and updates project documentation.
- Records actual verification evidence; it never invents local test results.

## 3. Zero-overlap file ownership

ChatGPT owns project documentation. Claude owns only explicitly assigned code files during an engineering assignment.

Neither AI may simultaneously modify the same file. Assignment records must list files authorised for modification and files excluded from modification.

Claude may inspect documentation but cannot change it without explicit Product Owner approval transferring ownership of the named file(s). ChatGPT must not edit code files while Claude has active modification ownership of those files. Ownership returns to ChatGPT/user integration only when Claude has returned the complete files and the assignment is closed or explicitly cancelled.

No assignment implicitly grants permission to modify files outside its stated scope.

## 4. Main-branch governance and assembly

- `main` is the authoritative shared branch.
- ChatGPT maintains repository documentation and integrates approved changes into `main`.
- Claude does not access GitHub for write operations and does not create branches, commits, or pull requests.
- The user assembles Claude's returned code locally and provides actual test evidence.
- ChatGPT must inspect current `main` before integration and use normal, non-destructive commits.
- Never force-push, rewrite history, or discard historical work.
- Do not claim access to uncommitted local files or a local working tree unless the user supplies them or a tool actually exposes them.

Branch-based work is prohibited unless the Product Owner explicitly authorises an exception. Any such exception must be recorded before it is used.

## 5. Change control

Obtain Product Owner approval before materially changing:
- Business requirements or project scope.
- Architecture or technology stack.
- Security boundaries.
- Data integrity and governance rules.
- Major dependencies or infrastructure commitments.
- Approved KPI definitions or business interpretations.

Routine implementation decisions may be made within approved boundaries. Explain alternatives and trade-offs for material changes. Record material decisions in `docs/DECISIONS.md`.

A proposed rule, AI recommendation, draft, or implemented calculation is not approved merely because it appears in the repository. Preserve explicit PROPOSED, APPROVED, VERIFIED, and ACCEPTED distinctions.

## 6. Return/alignment checkpoint

Whenever the user returns after Claude work or local code assembly, ChatGPT must first:
1. Establish and inspect the latest `main` commit.
2. Inspect repository state and relevant changes.
3. Compare supplied implementation against the approved assignment.
4. Review actual test results supplied by the user.
5. Identify inconsistencies, omissions, regressions, and blockers.
6. Confirm alignment or explain what remains unresolved.

Do not issue the next implementation assignment until this checkpoint is completed. Do not claim visibility into uncommitted local changes that the user has not supplied.

## 7. Engineering lifecycle and implementation discipline

Follow **DISCOVER → DESIGN → BUILD → VERIFY → REVIEW → RECORD**. Scale the process to task complexity.

Prioritise correctness, simplicity, maintainability, security, reliability, testability, explainability, and practical business value. Avoid speculative features and unnecessary frameworks, services, brokers, cloud infrastructure, or dependencies.

Inspect before modifying. Preserve verified functionality. Work in manageable increments. Do not begin substantial implementation before the relevant business requirements, architecture, and approval gates are satisfied.

## 8. Status and verification vocabulary

Use these states precisely:
- **NOT STARTED**
- **IN PROGRESS**
- **BLOCKED**
- **IMPLEMENTED**
- **VERIFIED**
- **ACCEPTED**

Implemented does not mean verified. Verification requires actual evidence. Verified does not mean accepted; Product Owner acceptance remains separate. Report failures and limitations honestly. Never invent test results, analytical findings, deployment status, or business impact.

## 9. Assignment and completion reporting

Every meaningful Claude assignment must identify objective, approved scope, base repository state, assigned files, excluded files, ownership, deliverables, acceptance criteria, and required tests.

At completion, report:
1. Accomplishments.
2. Files created or modified.
3. Important technical decisions.
4. Tests executed and actual results.
5. Outstanding issues.
6. Documentation status.
7. Git status/commit information where applicable.
8. Recommended next action.

## 10. Conflict resolution

If repository state, instructions, or project documents conflict:
1. Stop the conflicting change.
2. Inspect the relevant history and current repository state.
3. Identify the exact discrepancy and affected files/decisions.
4. Preserve existing work; do not overwrite blindly.
5. Present material choices to the Product Owner.
6. Record the approved resolution in the appropriate authoritative document.

Do not create duplicate AI agreements, parallel handoffs, or competing project implementations without a demonstrated need.
