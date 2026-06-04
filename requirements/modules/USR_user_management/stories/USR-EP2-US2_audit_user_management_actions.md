# USR-EP2-US2: Audit User Management Actions
## Detailed User Story

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `USR` - User Management |
| EPIC | [USR-EP2: Suspension and User Audit](../epics/USR-EP2_suspension_and_user_audit.md) |

## Story Statement

As an Owner, I want to review user management audit history so that sensitive access changes are traceable.

## Business Expectation

This story must convert the business expectation into a working system behavior that staff can use without relying on manual spreadsheets, side notes, or hidden process knowledge. The implementation must preserve the role boundaries, lifecycle rules, and data ownership described in the source business flow.

## Primary Actors

- Owner / Admin
- System
- Managed Consultant
- Managed Accounts user
- Managed Admission user
- Managed Visa user

## Source Documents

- [User Management Flow](../../../../business/flows/12_user_management_flow.md)
- [Users and Roles](../../../../business/users_and_roles.md)
- [User Management Design](../../../../design-guide/16-staff-user-management.html)

## Acceptance Criteria

- [ ] Audit history shows who changed what, when, and why.
- [ ] Audit records include create, role change, status change, and suspension events.
- [ ] Non-owner users cannot view user management audit history.

## Business Rules

- Only Owner manages staff users.
- Each user has one primary role unless explicitly approved.
- Suspension blocks access without deleting history.

## Dependencies and Preconditions

- Depends on ACL role model and audit logging.

## Frontend Tasks

- [ ] [USR-EP2-US2-FE1](../tasks/USR-EP2-US2-FE1.md): Build user audit history panel on staff detail page.
- [ ] [USR-EP2-US2-FE2](../tasks/USR-EP2-US2-FE2.md): Add filters for action type and date range.
- [ ] [USR-EP2-US2-FE3](../tasks/USR-EP2-US2-FE3.md): Add tests for audit rendering and owner-only visibility.

## Backend Tasks

- [ ] [USR-EP2-US2-BE1](../tasks/USR-EP2-US2-BE1.md): Implement user audit history API with action filters.
- [ ] [USR-EP2-US2-BE2](../tasks/USR-EP2-US2-BE2.md): Enforce owner-only access to user audit records.
- [ ] [USR-EP2-US2-BE3](../tasks/USR-EP2-US2-BE3.md): Add tests for audit filtering, owner-only access, and event completeness.

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
