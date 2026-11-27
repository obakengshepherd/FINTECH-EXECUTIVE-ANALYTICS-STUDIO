# AI Collaboration — Four-Nexus Engineering Operating Standard

**Version:** 1.1  
**Authority:** Product Owner  
**Effective:** 2026-11-27  
**Historical project cutoff:** 2026-11-25  
**Applies to:** All AI-assisted work in this repository  
**Status:** ACTIVE

## 1. Purpose and authority

This document implements the Product Owner's Four-Nexus Engineering Operating Standard (FNEOS) for FinTech Executive Analytics Studio.

The Product Owner retains final authority over business requirements, project scope, architecture, technology, security boundaries, data integrity rules, material dependencies/infrastructure, and acceptance.

The GitHub repository is the authoritative shared project record. Historical conversations and handoffs are context, not substitutes for repository evidence. Inspect repository state and relevant files before proposing or making changes.

The historical baseline is commit `e795c97d7eec671f47bb64b13178b5d8889db0cb` dated 2026-11-25. Work and workflow arrangements introduced on 2026-11-26 are superseded where they conflict with this standard. Historical commits are preserved; no history rewriting is permitted.

## 2. Authority and responsibilities

### ChatGPT — Primary AI

ChatGPT owns architecture, requirements, technical specifications, all project documentation, implementation planning, task decomposition, Claude handoffs, change control, main-branch governance, integration review, and evidence-based project status.

### Claude — Specialist AI

Claude independently reviews relevant Primary AI design and implementation work, identifies material risks, and implements only explicitly assigned code files under the approved handoff. Claude returns complete files in chat with exact repository-relative paths, implementation explanations, dependencies, assembly instructions, commands, tests, expected outcomes, limitations, and known issues.

Claude never pushes, commits, merges, or modifies ChatGPT-owned documentation. Claude does not change approved requirements or architecture unilaterally.

### Product Owner + VS Code + ChatGPT

The Product Owner assembles Claude's files locally and runs the application/tests. ChatGPT reviews supplied files, diffs, and actual execution evidence, then controls approved integration into `main` and records verified results.

## 3. Streamlined implementation workflow — no review loop

Every bounded implementation increment follows this sequence:

1. ChatGPT finalises the design and bounded implementation handoff.
2. Claude performs **one independent review of the relevant Primary AI work within that same handoff**.
3. If no blocking issue exists, Claude proceeds with implementation under the same handoff. A separate general review assignment is not required.
4. Claude returns complete assigned files and assembly/testing instructions.
5. The Product Owner assembles and tests in VS Code.
6. ChatGPT performs one return/alignment checkpoint and reviews the completed increment.
7. ChatGPT integrates approved changes and records the outcome.
8. The next increment begins.

Claude classifies findings as:
- **NON-BLOCKING:** document the concern and proceed within the approved design.
- **BLOCKING:** stop only the affected work; state the precise issue, impact, and recommended resolution.
- **PRODUCT OWNER DECISION:** request a decision only where a material approval is genuinely necessary.

Do not reopen settled decisions, repeat general reviews, or request approval for routine implementation choices within approved boundaries. If material issues arise, provide one consolidated report with issue, impact, proposed resolution, and exact decision required. Wait only for that decision.

## 4. Zero-overlap file ownership

ChatGPT owns all project documentation. Claude owns only explicitly assigned code files during an active implementation assignment. The Product Owner owns local assembly and execution.

Neither AI may simultaneously modify the same file. Every handoff lists exact files authorised for modification and files excluded from modification. Claude may read documentation but cannot modify it without explicit Product Owner-approved ownership transfer. ChatGPT must not edit code files while Claude has active modification ownership. Ownership returns to the user/ChatGPT integration process when Claude returns the complete files or the assignment is closed/cancelled.

No assignment implicitly grants permission to modify files outside its scope.

## 5. Main-branch governance and assembly

- `main` is the authoritative shared branch.
- ChatGPT maintains repository documentation and integrates approved changes into `main`.
- Claude does not perform GitHub write operations and does not create branches, commits, or pull requests.
- The user assembles Claude's returned code locally and provides actual test evidence.
- ChatGPT inspects current `main` before integration and uses normal, non-destructive commits.
- Never force-push, rewrite history, or discard historical work.
- Do not claim access to uncommitted local files or a local working tree unless the user supplies them or a tool exposes them.

Branch-based work is prohibited unless the Product Owner explicitly authorises an exception.

## 6. Change control

Obtain Product Owner approval before materially changing business requirements/scope, architecture/technology, security boundaries, data integrity/governance rules, major dependencies/infrastructure, or approved KPI definitions/business interpretations.

Routine implementation decisions may be made within approved boundaries. Explain alternatives and trade-offs for material changes. Record material decisions in `docs/DECISIONS.md`.

A proposal, AI recommendation, or implemented calculation is not approved merely because it appears in the repository. Preserve explicit PROPOSED, APPROVED, IMPLEMENTED, VERIFIED, and ACCEPTED distinctions.

## 7. Return/alignment checkpoint

When the user returns after Claude work or local assembly, ChatGPT must:
1. Establish and inspect latest `main`.
2. Inspect relevant repository changes.
3. Compare supplied files against the approved handoff.
4. Review actual test results supplied by the user.
5. Identify defects, omissions, regressions, and blockers.
6. Confirm alignment or explain what remains unresolved.

Do not issue the next implementation increment until this checkpoint is complete. Do not claim visibility into uncommitted local changes the user has not supplied.

## 8. Engineering discipline and status vocabulary

Follow **DISCOVER → DESIGN → BUILD → VERIFY → REVIEW → RECORD**. Prioritise correctness, simplicity, maintainability, security, reliability, testability, explainability, and practical business value. Avoid speculative features and unnecessary frameworks, services, brokers, cloud infrastructure, or dependencies.

Use these states precisely: NOT STARTED, IN PROGRESS, BLOCKED, IMPLEMENTED, VERIFIED, ACCEPTED. Implemented does not mean verified; verification requires actual evidence; verified does not mean Product Owner accepted.

## 9. Handoff and completion reporting

Every implementation handoff includes task ID and phase/increment; latest verified main SHA; approved architecture and requirements references; objective and scope; exact assigned and excluded files; dependencies/environment assumptions; expected behaviour and acceptance criteria; required commands/tests and expected outcomes; complete-file return format; VS Code assembly and local verification instructions; risks and stop conditions.

At completion, report accomplishments, files, technical decisions, tests and actual results, outstanding issues, documentation status, Git status where applicable, and recommended next action.

## 10. Conflict resolution

If repository state, instructions, or documents conflict, stop only the affected work, inspect the exact discrepancy, preserve existing work, and present material choices to the Product Owner. Do not create duplicate AI agreements, parallel handoffs, or competing implementations without a demonstrated need.
