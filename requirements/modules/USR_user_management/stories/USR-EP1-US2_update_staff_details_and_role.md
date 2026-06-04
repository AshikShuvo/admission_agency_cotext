# USR-EP1-US2: Update Staff Details and Role
## Detailed User Story

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `USR` - User Management |
| EPIC | [USR-EP1: Staff Account Lifecycle](../epics/USR-EP1_staff_account_lifecycle.md) |

## Story Statement

As an Owner, I want to update staff details or role so that access stays aligned with current business responsibility.

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

- [ ] Owner can update contact details, department, role, and account status.
- [ ] Role changes require a business reason.
- [ ] Past activity remains linked to the same user and is not rewritten.

## Business Rules

- Only Owner manages staff users.
- Each user has one primary role unless explicitly approved.
- Suspension blocks access without deleting history.

## Dependencies and Preconditions

- Depends on ACL role model and audit logging.

## Frontend Tasks

- [ ] [USR-EP1-US2-FE1](../tasks/USR-EP1-US2-FE1.md): Build staff detail/edit screen with current role and status.
- [ ] [USR-EP1-US2-FE2](../tasks/USR-EP1-US2-FE2.md): Require reason when role or access status changes.
- [ ] [USR-EP1-US2-FE3](../tasks/USR-EP1-US2-FE3.md): Add tests for role change reason and preserved user identity display.

## Backend Tasks

- [ ] [USR-EP1-US2-BE1](../tasks/USR-EP1-US2-BE1.md): Implement staff update API with role/status change reason validation.
- [ ] [USR-EP1-US2-BE2](../tasks/USR-EP1-US2-BE2.md): Record audit entries for changed fields, actor, timestamp, and reason.
- [ ] [USR-EP1-US2-BE3](../tasks/USR-EP1-US2-BE3.md): Add tests for role changes, audit log, and activity identity preservation.

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
