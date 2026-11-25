# Decision Register

Record material business, analytical, and technical decisions here. Newest decisions appear first. Proposed decisions must not be represented as approved.

## D-001 — Project foundation approval

- **Date:** 2026-11-25
- **Status:** APPROVED
- **Decision:** Establish FinTech Executive Analytics Studio as a synthetic financial-services Data Analysis portfolio project.
- **Authority:** Product Owner
- **Rationale:** Demonstrate the conversion of business questions and raw data into validated, actionable insights and executive communication.
- **Consequences:** Repository documentation and subsequent work must preserve synthetic-data boundaries and analytical discipline.

## D-002 — First analytical scenario

- **Date:** 2026-11-25
- **Status:** APPROVED
- **Decision:** Begin with Payments Performance Analytics.
- **Business question:** How is payment performance changing over time, and where should management investigate potential operational issues?
- **Rationale:** A bounded operational scenario provides a practical foundation for requirements, KPI governance, SQL analysis, validation, and executive reporting.

## D-003 — Initial toolkit

- **Date:** 2026-11-25
- **Status:** APPROVED
- **Decision:** Use SQL Server 2022/T-SQL as the primary analytical engine, Excel for supporting inspection and reconciliation, Power BI for visualisation and reporting, and Python/pandas where justified.
- **Rationale:** Prioritise practical analytical capability over unnecessary technology.

## D-004 — Clean-slate repository

- **Date:** 2026-11-25
- **Status:** CONFIRMED
- **Decision:** Use the supplied GitHub repository as a new project baseline.
- **Evidence:** Repository metadata showed public visibility, default branch `main`, size 0 KB; contents endpoint reported that the repository was empty and branch listing returned no branches.
- **Consequence:** No prior project implementation or documentation was inherited.

## D-005 — Initial architecture direction

- **Date:** 2026-11-25
- **Status:** PROPOSED BASELINE
- **Decision:** Use a single analytical project with synthetic source data, SQL Server, T-SQL analysis and validation, optional Excel/Python support, Power BI reporting, and executive outputs.
- **Rationale:** This is the simplest structure that satisfies the approved first scenario.
- **Constraint:** Material architecture changes require Product Owner approval.
