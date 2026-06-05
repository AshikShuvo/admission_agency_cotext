# ACL-EP1-US2: Block Unauthorized Direct Access
## Detailed User Story

Status: `Accepted`
Owner: `Turing / Hegel / Zeno`
Last updated: `2026-06-05`

## Traceability

| Level | Reference |
|---|---|
| Module | `ACL` - Access Control and Role Visibility |
| EPIC | [ACL-EP1: Role Permissions](../epics/ACL-EP1_role_permissions.md) |

## Story Statement

As the agency, I want direct route or API access blocked so that users cannot bypass UI restrictions.

## Business Expectation

This story must convert the business expectation into a working system behavior that staff can use without relying on manual spreadsheets, side notes, or hidden process knowledge. The implementation must preserve the role boundaries, lifecycle rules, and data ownership described in the source business flow.

## Primary Actors

- System
- Owner
- Consultant
- Accounts
- Admission
- Visa

## Source Documents

- [Access Control and Role Visibility Flow](../../../../business/flows/10_access_control_and_role_visibility_flow.md)
- [Users and Roles](../../../../business/users_and_roles.md)
- [Access Control Architecture](../../../../architecture/access_control.md)

## Acceptance Criteria

- [x] Unauthorized API calls return a clear forbidden response.
- [x] Unauthorized frontend routes show restricted access or redirect to allowed dashboard.
- [x] Unauthorized attempts can be audited for sensitive resources.

## Business Rules

- Backend authorization is mandatory.
- UI hiding is not enough.
- Sensitive fields are filtered by role.

## Dependencies and Preconditions

- Depends on role model from business/users_and_roles.md and applies to all modules.

## Frontend Tasks

- [x] [ACL-EP1-US2-FE1](../tasks/ACL-EP1-US2-FE1.md): Add protected route wrapper using current user permission data.
- [x] [ACL-EP1-US2-FE2](../tasks/ACL-EP1-US2-FE2.md): Build restricted access state for blocked routes.
- [x] [ACL-EP1-US2-FE3](../tasks/ACL-EP1-US2-FE3.md): Add tests for direct navigation to unauthorized screens.

## Backend Tasks

- [x] [ACL-EP1-US2-BE1](../tasks/ACL-EP1-US2-BE1.md): Standardize forbidden responses and authorization error handling.
- [x] [ACL-EP1-US2-BE2](../tasks/ACL-EP1-US2-BE2.md): Add optional access audit log for sensitive blocked attempts.
- [x] [ACL-EP1-US2-BE3](../tasks/ACL-EP1-US2-BE3.md): Add tests for direct forbidden API access.

## Cross-Agent Contract

- Backend owns persistence, authorization, workflow gates, audit events, and role-scoped API responses.
- Frontend owns the staff-facing workflow, visible states, validation feedback, and clear blocked-state messaging.
- QA/review owns acceptance verification across frontend, backend, and access-control behavior.
- If the frontend and backend agents disagree on API shape, pause the story and add a blocker to [Progress Tracker](../../../progress_tracker.md).

## Detailed Acceptance Review Checklist

- [x] User can complete the happy path described by the story statement.
- [x] User sees clear feedback when required data is missing or a workflow gate blocks progress.
- [x] Unauthorized roles cannot perform the action through UI or API.
- [x] Restricted data is not returned from the backend and is not rendered by the frontend.
- [x] Important state changes create audit log or notification events where required by the business rules.
- [x] Automated tests cover the success path and at least one failure or restricted path.

## Completion Rules

- [x] All linked frontend tasks are complete.
- [x] All linked backend tasks are complete.
- [x] Acceptance criteria are verified by QA/review.
- [x] Story count is updated in [Progress Tracker](../../../progress_tracker.md).
- [x] EPIC progress is recalculated after this story is accepted.
