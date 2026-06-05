# USR-EP1-US0-FE2: Store session securely and load current user from real token.
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

This task connects the browser session to backend token auth without exposing the JWT to application JavaScript.

## Source Documents

- [User Management Flow](../../../../business/flows/12_user_management_flow.md)
- [Users and Roles](../../../../business/users_and_roles.md)
- [Login Design](../../../../design-guide/01-login.html)

## Acceptance Criteria Impact

- [ ] `/auth/me` returns the authenticated Owner from the token.
- [ ] Frontend login stores the session securely and redirects authenticated Owner into an allowed workspace.

## Business Rules To Preserve

- Backend remains the source of truth for authorization.
- Token values are stored in an HttpOnly same-site cookie through a Next.js route handler.
- Unauthenticated users cannot render protected workspace data.

## Dependencies To Check First

- Depends on backend login and `/auth/me` token contract.

## Implementation Plan

1. Add Next.js route handler for `/api/auth/login` that calls backend `POST /auth/login`.
2. Store the returned JWT in an HttpOnly, same-site cookie with production-safe flags.
3. Add current-user loading through the real session token by proxying to backend `/auth/me`.
4. Update route protection helpers to redirect unauthenticated users to `/login`.
5. Preserve restricted-access UI for authenticated users who lack a workspace permission.
6. Add logout or cookie-clearing helper if required to keep tests and browser flows deterministic.

## UI and Contract Expectations

- Browser submits credentials to the Next.js route handler.
- Server-side current-user reads the cookie and calls backend `/auth/me`.
- Client-side current-user checks should use the same session-backed contract.

## Test Plan

- [ ] Add or update tests for authenticated current-user mapping.
- [ ] Add or update tests for unauthenticated route handling.
- [ ] Record the test command in the agent handoff note.

## Definition of Done

- [ ] Implementation matches this task plan and the linked story acceptance criteria.
- [ ] Required session behavior is implemented in the correct route/helper boundary.
- [ ] Tests are added or an explicit test gap is recorded as a blocker.
- [ ] This task checkbox is marked complete in the story file and source module summary.
- [ ] [Progress Tracker](../../../progress_tracker.md) is updated with the completed task count.

## Handoff Note Template

```text
Module: USR
Story: USR-EP1-US0
Completed task: USR-EP1-US0-FE2
Files changed:
Tests run:
Tracker updated:
Open blockers:
Next recommended task:
```
