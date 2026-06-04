# ACL-EP1-US1: Enforce Role Permissions
## Detailed User Story

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `ACL` - Access Control and Role Visibility |
| EPIC | [ACL-EP1: Role Permissions](../epics/ACL-EP1_role_permissions.md) |

## Story Statement

As the system, I want to enforce role permissions so that users cannot perform actions outside their business responsibility.

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

- [ ] Each protected API checks authenticated role before executing mutations.
- [ ] Non-owner users cannot manage catalog, users, or commissions.
- [ ] Accounts cannot approve admission or visa stages.

## Business Rules

- Backend authorization is mandatory.
- UI hiding is not enough.
- Sensitive fields are filtered by role.

## Dependencies and Preconditions

- Depends on role model from business/users_and_roles.md and applies to all modules.

## Frontend Tasks

- [ ] [ACL-EP1-US1-FE1](../tasks/ACL-EP1-US1-FE1.md): Build role-based navigation configuration for allowed workspaces.
- [ ] [ACL-EP1-US1-FE2](../tasks/ACL-EP1-US1-FE2.md): Add disabled or hidden action states based on backend permission data.
- [ ] [ACL-EP1-US1-FE3](../tasks/ACL-EP1-US1-FE3.md): Add tests for role-specific navigation and blocked actions.

## Backend Tasks

- [ ] [ACL-EP1-US1-BE1](../tasks/ACL-EP1-US1-BE1.md): Implement role permission map for core modules and actions.
- [ ] [ACL-EP1-US1-BE2](../tasks/ACL-EP1-US1-BE2.md): Add NestJS guards or policy checks for protected routes and service actions.
- [ ] [ACL-EP1-US1-BE3](../tasks/ACL-EP1-US1-BE3.md): Add tests for allowed and blocked role actions across key modules.

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
