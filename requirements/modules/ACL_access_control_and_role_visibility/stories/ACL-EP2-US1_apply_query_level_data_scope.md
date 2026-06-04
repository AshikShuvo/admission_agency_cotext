# ACL-EP2-US1: Apply Query-Level Data Scope
## Detailed User Story

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `ACL` - Access Control and Role Visibility |
| EPIC | [ACL-EP2: Data Scope and Sensitive Field Filtering](../epics/ACL-EP2_data_scope_and_sensitive_field_filtering.md) |

## Story Statement

As the system, I want query-level data scopes so that users only receive records they are allowed to see.

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

- [ ] Consultant file lists include only assigned files.
- [ ] Department users see only stage-relevant files.
- [ ] Owner can filter across all files.

## Business Rules

- Backend authorization is mandatory.
- UI hiding is not enough.
- Sensitive fields are filtered by role.

## Dependencies and Preconditions

- Depends on role model from business/users_and_roles.md and applies to all modules.

## Frontend Tasks

- [ ] [ACL-EP2-US1-FE1](../tasks/ACL-EP2-US1-FE1.md): Consume scoped API responses without assuming hidden data exists.
- [ ] [ACL-EP2-US1-FE2](../tasks/ACL-EP2-US1-FE2.md): Show role-appropriate filter options for file lists and reports.
- [ ] [ACL-EP2-US1-FE3](../tasks/ACL-EP2-US1-FE3.md): Add tests for consultant and department scoped list behavior.

## Backend Tasks

- [ ] [ACL-EP2-US1-BE1](../tasks/ACL-EP2-US1-BE1.md): Implement reusable query scope helpers for file, payment, document, and report queries.
- [ ] [ACL-EP2-US1-BE2](../tasks/ACL-EP2-US1-BE2.md): Apply scopes in Files, Payments, Admission, Visa, Documents, and Reporting services.
- [ ] [ACL-EP2-US1-BE3](../tasks/ACL-EP2-US1-BE3.md): Add tests proving scopes are enforced in list, detail, and report APIs.

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
