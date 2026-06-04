# COM-EP2-US1: View Commission List and Filters
## Detailed User Story

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `COM` - University Commission Tracking |
| EPIC | [COM-EP2: Commission Reporting](../epics/COM-EP2_commission_reporting.md) |

## Story Statement

As an Owner, I want to filter commission records so that I can review received revenue.

## Business Expectation

This story must convert the business expectation into a working system behavior that staff can use without relying on manual spreadsheets, side notes, or hidden process knowledge. The implementation must preserve the role boundaries, lifecycle rules, and data ownership described in the source business flow.

## Primary Actors

- Owner
- University

## Source Documents

- [University Commission Tracking Flow](../../../../business/flows/07_university_commission_tracking_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [Commission Tracking Design](../../../../design-guide/12-commission-tracking.html)

## Acceptance Criteria

- [ ] Owner can filter by date range, university, country, file, and consultant.
- [ ] List shows amount, received date, student file, university, and notes.
- [ ] Non-owner users cannot access the list.

## Business Rules

- Commission is Owner-only.
- Commission records link to file and university.
- Non-owner responses must exclude commission data.

## Dependencies and Preconditions

- Depends on VIS completion/enrollment and ACL Owner-only access.

## Frontend Tasks

- [ ] [COM-EP2-US1-FE1](../tasks/COM-EP2-US1-FE1.md): Build owner commission list with filters and summary count.
- [ ] [COM-EP2-US1-FE2](../tasks/COM-EP2-US1-FE2.md): Add loading, empty, and filtered result states.
- [ ] [COM-EP2-US1-FE3](../tasks/COM-EP2-US1-FE3.md): Add tests for filtering and owner-only route access.

## Backend Tasks

- [ ] [COM-EP2-US1-BE1](../tasks/COM-EP2-US1-BE1.md): Implement commission list API with filter DTOs and pagination.
- [ ] [COM-EP2-US1-BE2](../tasks/COM-EP2-US1-BE2.md): Add owner-only authorization and efficient joins to file/university data.
- [ ] [COM-EP2-US1-BE3](../tasks/COM-EP2-US1-BE3.md): Add tests for filters, pagination, and role blocking.

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
