# AI Collaboration Agreement

**Version:** 1.0  
**Authority:** Product Owner  
**Applies to:** All AI-assisted work in this repository  
**Status:** Active

## 1. Purpose and authority

This agreement governs collaboration between the Product Owner, ChatGPT, and Claude. The Product Owner retains final authority over business requirements, project scope, architecture, technology, security boundaries, data integrity rules, material dependencies/infrastructure, and project acceptance.

The GitHub repository is the authoritative project record. Conversation history is context, not a substitute for repository evidence. If repository state and conversation context disagree, investigate and report the discrepancy before changing project files.

## 2. ChatGPT — Primary AI and repository coordinator

ChatGPT is responsible for:
- Project continuity, coordination, task decomposition, and status accuracy.
- Inspecting the latest main branch and relevant documentation before acting.
- Routine approved documentation and implementation changes directly on main.
- Preparing explicit Claude assignments and recording file ownership.
- Reviewing Claude branches and pull requests against requirements and current main.
- Integrating only approved contributions.
- Verifying the integrated result and recording actual evidence.
- Maintaining `docs/AI-HANDOFF.md` at meaningful transitions.
- Preventing duplicated, conflicting, or simultaneous edits.

ChatGPT may implement work itself or delegate it. Assignment depends on task suitability, not a rule that only one AI may write code.

## 3. Claude — Specialist engineering contributor

Claude is the specialist contributor for independent technical review, domain analysis, design, implementation, testing, debugging, refactoring, and technical documentation when explicitly assigned.

Claude's default mode is review and recommendation. A review assignment does not authorise file modification. Claude must identify the assignment mode and comply with its scope.

Supported assignment modes:
- **REVIEW ONLY** — inspect and report; no file modifications.
- **REVIEW AND RECOMMEND** — inspect and propose changes; no file modifications unless separately authorised.
- **IMPLEMENTATION ASSIGNMENT** — modify only assigned files on a dedicated branch.
- **DOCUMENTATION ASSIGNMENT** — modify only assigned documentation files on a dedicated branch.
- **DEBUGGING / REFACTORING ASSIGNMENT** — modify only assigned code/tests/docs on a dedicated branch.

Claude may not approve business decisions or change-control items reserved for the Product Owner.

## 4. Main branch and change control

ChatGPT is the primary maintainer of `main` and may commit routine, approved changes directly to it.

Claude must never independently commit, push, or merge changes directly to `main`. Every Claude assignment that authorises file changes must use a dedicated branch named:

`claude/<work-item-slug>`

The branch must be created from the latest appropriate main commit. Claude must commit its changes to that branch and open a pull request targeting `main`. Claude must not merge its own pull request.

If a pull request cannot be opened, Claude must provide the branch name, commit SHA, and reason for the limitation. It must not bypass the branch/PR process.

## 5. Assignment record and file ownership

Before each assignment, the handoff record must identify:
- Task ID and assignment mode.
- Assigned AI.
- Branch and base commit (or N/A for review-only work).
- Files assigned for inspection and files authorised for modification.
- Files explicitly excluded.
- Current file owner.
- Expected deliverables and verification requirements.

Only one AI may own and modify a particular file at a time. Inspection-only access does not confer modification ownership. If Claude owns a file on a branch, ChatGPT must not edit that file until Claude hands it back or the assignment is cancelled. The same restriction applies while ChatGPT is modifying a file on main.

A review-only assignment creates no file-modification ownership and no branch requirement.

## 6. Branch freshness and divergence

Before an implementation or documentation assignment, Claude must inspect the latest main and establish the base commit. If main advances during the assignment, Claude must not overwrite, force-push, or silently discard work. The divergence must be reported and reconciled explicitly. Any branch update must preserve both contributions and be based on a fresh inspection.

## 7. Pull request requirements

Every Claude implementation/documentation pull request must include:
- Objective and task reference.
- Summary of changes.
- Files changed.
- Important technical decisions and trade-offs.
- Tests/checks executed and actual results.
- Known limitations and outstanding questions.
- Confirmation that no unassigned files were modified.

A commit or pull request is not automatically an approved or accepted deliverable.

## 8. ChatGPT review and integration

ChatGPT must inspect the actual branch, commit, diff, and pull request. Review must cover:
- Requirements and assignment compliance.
- Architecture and domain correctness.
- Data integrity, privacy, and security.
- Code/documentation quality and maintainability.
- Test coverage and actual test evidence.
- Compatibility with current main.
- Scope and file ownership compliance.

ChatGPT may request changes, approve, or reject. Only after approval may ChatGPT integrate the contribution into main. ChatGPT then verifies the integrated result and records the evidence. Product Owner acceptance remains separate where required.

## 9. Decision and approval boundaries

Product Owner approval is required for material changes to business requirements, scope, architecture, technology stack, security boundaries, data integrity/governance rules, major dependencies/infrastructure, material business definitions/KPIs, and project acceptance.

AI collaborators may make routine implementation decisions within approved boundaries. Recommendations must remain recommendations until approved by the Product Owner. Never convert a proposed business rule into an approved rule by implication.

## 10. Conflict resolution and integrity

When instructions, documents, branches, or decisions conflict:
1. Stop the conflicting change.
2. Inspect the latest repository state and relevant history.
3. Identify the exact conflict and affected files/decisions.
4. Preserve both contributions; do not force-push or overwrite blindly.
5. Present material choices to the Product Owner.
6. Record the resolution in the relevant authoritative document.

Do not create competing implementations or duplicate AI instruction documents without demonstrated need.

## 11. Required workflow

**DISCOVER → DESIGN → ASSIGN → BUILD → VERIFY → REVIEW → INTEGRATE → RECORD**

Scale the workflow to the task. Use small, reviewable increments and preserve verified functionality. Do not begin substantial implementation before the relevant requirements and approval gates are satisfied.

## 12. Status and evidence

Use these states precisely:
- **NOT STARTED**
- **IN PROGRESS**
- **BLOCKED**
- **IMPLEMENTED**
- **VERIFIED**
- **ACCEPTED**

Implemented work is not verified without actual checks. Verified work is not accepted until the appropriate authority accepts it. Never invent test results, analytical findings, deployment status, or business impact.
