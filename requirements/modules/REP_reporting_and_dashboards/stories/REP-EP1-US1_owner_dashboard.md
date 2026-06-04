# REP-EP1-US1: Owner Dashboard
## Detailed User Story

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `REP` - Reporting and Dashboards |
| EPIC | [REP-EP1: Role-Based Dashboards](../epics/REP-EP1_role_based_dashboards.md) |

## Story Statement

As an Owner, I want a full business dashboard so that I can monitor files, revenue, dues, activity, and commissions.

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

- [ ] Owner dashboard shows files by status, revenue, dues, consultant performance, recent activity, and commission summary.
- [ ] Metrics support date range filters.
- [ ] Owner can drill into filtered file lists.

## Business Rules

- Reports must use query-layer role scopes.
- Owner sees all reports.
- Commission appears only in Owner reports.

## Dependencies and Preconditions

- Depends on FIL, PAY, ADM, VIS, COM, and ACL query scopes.

## Frontend Tasks

- [ ] [REP-EP1-US1-FE1](../tasks/REP-EP1-US1-FE1.md): Build owner dashboard metric cards, status breakdowns, and recent activity sections.
- [ ] [REP-EP1-US1-FE2](../tasks/REP-EP1-US1-FE2.md): Add date range and drill-down interactions.
- [ ] [REP-EP1-US1-FE3](../tasks/REP-EP1-US1-FE3.md): Add tests for owner dashboard rendering and filter state.

## Backend Tasks

- [ ] [REP-EP1-US1-BE1](../tasks/REP-EP1-US1-BE1.md): Implement owner dashboard summary API with file, payment, due, activity, and commission aggregates.
- [ ] [REP-EP1-US1-BE2](../tasks/REP-EP1-US1-BE2.md): Add date range filters and drill-down query parameters.
- [ ] [REP-EP1-US1-BE3](../tasks/REP-EP1-US1-BE3.md): Add tests for aggregate accuracy and owner-only commission inclusion.

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
