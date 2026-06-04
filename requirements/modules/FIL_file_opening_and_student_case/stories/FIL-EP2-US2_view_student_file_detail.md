# FIL-EP2-US2: View Student File Detail
## Detailed User Story

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `FIL` - File Opening and Student Case |
| EPIC | [FIL-EP2: Package Snapshot and File Detail](../epics/FIL-EP2_package_snapshot_and_file_detail.md) |

## Story Statement

As a staff user, I want to view the file detail allowed for my role so that I can understand current status and next actions.

## Business Expectation

This story must convert the business expectation into a working system behavior that staff can use without relying on manual spreadsheets, side notes, or hidden process knowledge. The implementation must preserve the role boundaries, lifecycle rules, and data ownership described in the source business flow.

## Primary Actors

- Consultant
- Student
- Accounts
- Owner, oversight

## Source Documents

- [File Opening Flow](../../../../business/flows/03_file_opening_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [File Opening Design](../../../../design-guide/07-file-opening.html)
- [Student File Detail Design](../../../../design-guide/08-student-file-detail.html)

## Acceptance Criteria

- [ ] File detail shows student, selected program, status, payments, documents, and activity according to role scope.
- [ ] Consultant sees only assigned files.
- [ ] Owner sees full file detail.

## Business Rules

- Consultants only manage assigned files.
- File numbers are unique.
- Package fees are copied at creation time.
- File history is preserved.

## Dependencies and Preconditions

- Depends on CAT active package and CNS selected program context.

## Frontend Tasks

- [ ] [FIL-EP2-US2-FE1](../tasks/FIL-EP2-US2-FE1.md): Build role-aware file detail layout with status, tabs, and next action summary.
- [ ] [FIL-EP2-US2-FE2](../tasks/FIL-EP2-US2-FE2.md): Add empty, locked, loading, and restricted-section states.
- [ ] [FIL-EP2-US2-FE3](../tasks/FIL-EP2-US2-FE3.md): Add tests for role-specific file detail visibility.

## Backend Tasks

- [ ] [FIL-EP2-US2-BE1](../tasks/FIL-EP2-US2-BE1.md): Implement file detail API with role-based data shape.
- [ ] [FIL-EP2-US2-BE2](../tasks/FIL-EP2-US2-BE2.md): Add query-layer scope filters for Owner, Consultant, Accounts, Admission, and Visa.
- [ ] [FIL-EP2-US2-BE3](../tasks/FIL-EP2-US2-BE3.md): Add tests for assigned-file restriction and sensitive field hiding.

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
