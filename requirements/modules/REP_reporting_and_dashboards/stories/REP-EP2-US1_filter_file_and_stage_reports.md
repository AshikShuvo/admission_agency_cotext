# REP-EP2-US1: Filter File and Stage Reports
## Detailed User Story

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `REP` - Reporting and Dashboards |
| EPIC | [REP-EP2: Operational Reports](../epics/REP-EP2_operational_reports.md) |

## Story Statement

As an authorized user, I want to filter file reports so that I can inspect the work relevant to my role.

## Business Expectation

This story must convert the business expectation into a working system behavior that staff can use without relying on manual spreadsheets, side notes, or hidden process knowledge. The implementation must preserve the role boundaries, lifecycle rules, and data ownership described in the source business flow.

## Primary Actors

- Owner
- Accounts
- Consultant
- Admission
- Visa

## Source Documents

- [Reporting and Dashboard Flow](../../../../business/flows/08_reporting_and_dashboard_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [Reports and Dashboards Design](../../../../design-guide/13-reports-and-dashboards.html)

## Acceptance Criteria

- [ ] Filters include date range, file status, consultant, stage, and university where allowed.
- [ ] Consultant results include only assigned files.
- [ ] Owner results include all files.

## Business Rules

- Reports must use query-layer role scopes.
- Owner sees all reports.
- Commission appears only in Owner reports.

## Dependencies and Preconditions

- Depends on FIL, PAY, ADM, VIS, COM, and ACL query scopes.

## Frontend Tasks

- [ ] [REP-EP2-US1-FE1](../tasks/REP-EP2-US1-FE1.md): Build report filter panel and results table.
- [ ] [REP-EP2-US1-FE2](../tasks/REP-EP2-US1-FE2.md): Add role-aware filter availability and result columns.
- [ ] [REP-EP2-US1-FE3](../tasks/REP-EP2-US1-FE3.md): Add tests for filters and consultant assigned-file restriction.

## Backend Tasks

- [ ] [REP-EP2-US1-BE1](../tasks/REP-EP2-US1-BE1.md): Implement file report API with filters and pagination.
- [ ] [REP-EP2-US1-BE2](../tasks/REP-EP2-US1-BE2.md): Apply role-based query scopes before aggregation.
- [ ] [REP-EP2-US1-BE3](../tasks/REP-EP2-US1-BE3.md): Add tests for filters, scopes, and pagination.

## Cross-Agent Contract

- Backend owns persistence, authorization, workflow gates, audit events, and role-scoped API responses.
- Frontend owns the staff-facing workflow, visible states, validation feedback, and clear blocked-state messaging.
- QA/review owns acceptance verification across frontend, backend, and access-control behavior.
- If the frontend and backend agents disagree on API shape, pause the story and add a blocker to [Progress Tracker](../../../progress_tracker.md).

## Detailed Acceptance Review Checklist

- [ ] User can complete the happy path described by the story statement.
- [ ] User sees clear feedback when required data is missing or a workflow gate blocks progress.
- [ ] Unauthorized roles cannot perform the action through UI or API.
- [ ] Restricted data is not returned from the backend and is not rendered by the frontend.
- [ ] Important state changes create audit log or notification events where required by the business rules.
- [ ] Automated tests cover the success path and at least one failure or restricted path.

## Completion Rules

- [ ] All linked frontend tasks are complete.
- [ ] All linked backend tasks are complete.
- [ ] Acceptance criteria are verified by QA/review.
- [ ] Story count is updated in [Progress Tracker](../../../progress_tracker.md).
- [ ] EPIC progress is recalculated after this story is accepted.
