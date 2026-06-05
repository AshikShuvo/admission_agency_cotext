# USR-EP1-US0-FE1: Build login page from design guide.
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

This task creates the first real browser entry point for authenticated Owner work.

## Source Documents

- [User Management Flow](../../../../business/flows/12_user_management_flow.md)
- [Users and Roles](../../../../business/users_and_roles.md)
- [Login Design](../../../../design-guide/01-login.html)

## Acceptance Criteria Impact

- [ ] Frontend login stores the session securely and redirects authenticated Owner into an allowed workspace.

## Business Rules To Preserve

- Staff creation does not start until Owner login is accepted.
- Login UI must not expose secrets, token values, or backend implementation details.

## Dependencies To Check First

- Depends on backend `POST /auth/login` contract or a documented temporary blocker.

## Implementation Plan

1. Create `/login` using the visual structure and fields from `design-guide/01-login.html`.
2. Add email and password fields with accessible labels, validation, and disabled submit states.
3. Add loading, success redirect, validation error, credential error, inactive-user error, and backend error states.
4. Post credentials to the Next.js auth route handler instead of calling the backend directly from browser code.
5. Redirect an authenticated Owner into the default allowed dashboard or workspace.
6. Keep unauthenticated users on `/login` without rendering protected workspace data.

## UI and Contract Expectations

- Use Next.js, TypeScript, Tailwind CSS, and the existing design system.
- Keep the login page focused on the login workflow, not a marketing landing page.
- Preserve ACL restricted-route behavior after successful login.

## Test Plan

- [ ] Add or update automated tests for login form validation.
- [ ] Add or update tests for login error rendering.
- [ ] Record the test command in the agent handoff note.

## Definition of Done

- [ ] Implementation matches this task plan and the linked story acceptance criteria.
- [ ] Required UI behavior is implemented in the correct route boundary.
- [ ] Tests are added or an explicit test gap is recorded as a blocker.
- [ ] This task checkbox is marked complete in the story file and source module summary.
- [ ] [Progress Tracker](../../../progress_tracker.md) is updated with the completed task count.

## Handoff Note Template

```text
Module: USR
Story: USR-EP1-US0
Completed task: USR-EP1-US0-FE1
Files changed:
Tests run:
Tracker updated:
Open blockers:
Next recommended task:
```
