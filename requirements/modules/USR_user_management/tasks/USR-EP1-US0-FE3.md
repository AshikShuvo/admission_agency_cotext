# USR-EP1-US0-FE3: Add frontend tests for login states and authenticated route access.
## Detailed Frontend Task Plan

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-05`

## Traceability

| Level | Reference |
|---|---|
| Module | `USR` - User Management |
| EPIC | [USR-EP1: Staff Account Lifecycle](../epics/USR-EP1_staff_account_lifecycle.md) |
| User Story | [USR-EP1-US0: Bootstrap Owner Login](../stories/USR-EP1-US0_bootstrap_owner_login.md) |
| Task Type | `FE` |

## Business Context

As an Owner, I want a bootstrapped account and secure login so that I can access the system and create staff users.

This task proves the login UI and route protection before staff creation is implemented.

## Source Documents

- [User Management Flow](../../../../business/flows/12_user_management_flow.md)
- [Users and Roles](../../../../business/users_and_roles.md)
- [Login Design](../../../../design-guide/01-login.html)

## Acceptance Criteria Impact

- [ ] Frontend login stores the session securely and redirects authenticated Owner into an allowed workspace.
- [ ] Missing, invalid, suspended, or inactive sessions are blocked with stable auth errors.

## Business Rules To Preserve

- Unauthenticated users are redirected to `/login` or shown a login-required state.
- Authenticated users without workspace permission still see the restricted-access behavior from ACL.

## Dependencies To Check First

- Depends on `USR-EP1-US0-FE1` and `USR-EP1-US0-FE2`.

## Implementation Plan

1. Add frontend tests for login form required-field validation.
2. Add frontend tests for backend credential error rendering.
3. Add current-user mapping tests for a valid authenticated session.
4. Add unauthenticated route tests for redirect or login-required behavior.
5. Add restricted-workspace test proving ACL behavior remains after login.
6. Record whether Playwright is deferred or included for this story.

## UI and Contract Expectations

- Prefer focused unit or route-handler tests for login helpers.
- Use Playwright once login is merged and real browser role flows become useful.
- Keep test fixtures free of production credentials or live secrets.

## Test Plan

- [ ] `pnpm --filter @admission-agency/web lint`
- [ ] `pnpm --filter @admission-agency/web typecheck`
- [ ] `pnpm --filter @admission-agency/web test`

## Definition of Done

- [ ] Implementation matches this task plan and the linked story acceptance criteria.
- [ ] Required UI/session behavior is covered by automated tests.
- [ ] Route protection and restricted-access behavior are tested or a blocker is recorded.
- [ ] This task checkbox is marked complete in the story file and source module summary.
- [ ] [Progress Tracker](../../../progress_tracker.md) is updated with the completed task count.

## Handoff Note Template

```text
Module: USR
Story: USR-EP1-US0
Completed task: USR-EP1-US0-FE3
Files changed:
Tests run:
Tracker updated:
Open blockers:
Next recommended task:
```
