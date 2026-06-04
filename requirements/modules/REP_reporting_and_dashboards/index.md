# Reporting and Dashboards
## Independent Requirement Module Folder

Module ID: `REP`

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Module Goal

Give each role the operational and financial visibility needed for daily work while enforcing query-layer data boundaries.

## Primary Actors

- Owner
- Accounts
- Consultant
- Admission
- Visa

## Source Documents

- [Reporting and Dashboard Flow](../../../business/flows/08_reporting_and_dashboard_flow.md)
- [Module Boundaries](../../../architecture/module_boundaries.md)
- [Reports and Dashboards Design](../../../design-guide/13-reports-and-dashboards.html)

## Architecture Routing

| Area | Owner |
|---|---|
| Frontend workspace | Role-Based Dashboard |
| Backend module boundary | Reporting |
| Design reference | ../../../design-guide/13-reports-and-dashboards.html |

## Business Rules

- Reports must use query-layer role scopes.
- Owner sees all reports.
- Commission appears only in Owner reports.

## Dependencies

- Depends on FIL, PAY, ADM, VIS, COM, and ACL query scopes.

## EPIC Files

- [ ] [REP-EP1: Role-Based Dashboards](epics/REP-EP1_role_based_dashboards.md)
- [ ] [REP-EP2: Operational Reports](epics/REP-EP2_operational_reports.md)

## User Story Files

- [ ] [REP-EP1-US1: Owner Dashboard](stories/REP-EP1-US1_owner_dashboard.md)
- [ ] [REP-EP1-US2: Staff Dashboards](stories/REP-EP1-US2_staff_dashboards.md)
- [ ] [REP-EP2-US1: Filter File and Stage Reports](stories/REP-EP2-US1_filter_file_and_stage_reports.md)
- [ ] [REP-EP2-US2: View Financial and Due Reports](stories/REP-EP2-US2_view_financial_and_due_reports.md)

## Task Implementation Plans

- [ ] [REP-EP1-US1-FE1](tasks/REP-EP1-US1-FE1.md): Build owner dashboard metric cards, status breakdowns, and recent activity sections.
- [ ] [REP-EP1-US1-FE2](tasks/REP-EP1-US1-FE2.md): Add date range and drill-down interactions.
- [ ] [REP-EP1-US1-FE3](tasks/REP-EP1-US1-FE3.md): Add tests for owner dashboard rendering and filter state.
- [ ] [REP-EP1-US1-BE1](tasks/REP-EP1-US1-BE1.md): Implement owner dashboard summary API with file, payment, due, activity, and commission aggregates.
- [ ] [REP-EP1-US1-BE2](tasks/REP-EP1-US1-BE2.md): Add date range filters and drill-down query parameters.
- [ ] [REP-EP1-US1-BE3](tasks/REP-EP1-US1-BE3.md): Add tests for aggregate accuracy and owner-only commission inclusion.
- [ ] [REP-EP1-US2-FE1](tasks/REP-EP1-US2-FE1.md): Build role-specific dashboard layouts for Consultant, Accounts, Admission, and Visa.
- [ ] [REP-EP1-US2-FE2](tasks/REP-EP1-US2-FE2.md): Add role-aware empty states and quick links to relevant workspaces.
- [ ] [REP-EP1-US2-FE3](tasks/REP-EP1-US2-FE3.md): Add tests for dashboard selection by role.
- [ ] [REP-EP1-US2-BE1](tasks/REP-EP1-US2-BE1.md): Implement staff dashboard APIs with role-specific aggregate shapes.
- [ ] [REP-EP1-US2-BE2](tasks/REP-EP1-US2-BE2.md): Enforce query-layer scopes for assigned files and department-stage data.
- [ ] [REP-EP1-US2-BE3](tasks/REP-EP1-US2-BE3.md): Add tests for consultant scope, accounts finance scope, and department queue accuracy.
- [ ] [REP-EP2-US1-FE1](tasks/REP-EP2-US1-FE1.md): Build report filter panel and results table.
- [ ] [REP-EP2-US1-FE2](tasks/REP-EP2-US1-FE2.md): Add role-aware filter availability and result columns.
- [ ] [REP-EP2-US1-FE3](tasks/REP-EP2-US1-FE3.md): Add tests for filters and consultant assigned-file restriction.
- [ ] [REP-EP2-US1-BE1](tasks/REP-EP2-US1-BE1.md): Implement file report API with filters and pagination.
- [ ] [REP-EP2-US1-BE2](tasks/REP-EP2-US1-BE2.md): Apply role-based query scopes before aggregation.
- [ ] [REP-EP2-US1-BE3](tasks/REP-EP2-US1-BE3.md): Add tests for filters, scopes, and pagination.
- [ ] [REP-EP2-US2-FE1](tasks/REP-EP2-US2-FE1.md): Build financial report views for payments, dues, and pending confirmations.
- [ ] [REP-EP2-US2-FE2](tasks/REP-EP2-US2-FE2.md): Add owner-only commission summary section.
- [ ] [REP-EP2-US2-FE3](tasks/REP-EP2-US2-FE3.md): Add tests for Accounts vs Owner financial report visibility.
- [ ] [REP-EP2-US2-BE1](tasks/REP-EP2-US2-BE1.md): Implement financial report APIs with payment, due, and pending confirmation aggregates.
- [ ] [REP-EP2-US2-BE2](tasks/REP-EP2-US2-BE2.md): Add owner-only commission aggregation and accounts-safe response shaping.
- [ ] [REP-EP2-US2-BE3](tasks/REP-EP2-US2-BE3.md): Add tests for financial aggregate accuracy and commission exclusion.

## Folder Completion Rules

- [ ] Every EPIC file is complete.
- [ ] Every story file is accepted.
- [ ] Every task implementation plan is completed or explicitly deferred with an approved blocker.
- [ ] Module row is updated in [Progress Tracker](../../progress_tracker.md).
- [ ] Completion log records meaningful milestone completion.
