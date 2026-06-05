# USR-EP1-US0-BE2: Implement login, JWT issuance, and `/auth/me` from token.
## Detailed Backend Task Plan

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-05`

## Traceability

| Level | Reference |
|---|---|
| Module | `USR` - User Management |
| EPIC | [USR-EP1: Staff Account Lifecycle](../epics/USR-EP1_staff_account_lifecycle.md) |
| User Story | [USR-EP1-US0: Bootstrap Owner Login](../stories/USR-EP1-US0_bootstrap_owner_login.md) |
| Task Type | `BE` |

## Business Context

As an Owner, I want a bootstrapped account and secure login so that I can access the system and create staff users.

This task replaces browser-facing mock auth with token-backed current-user context while keeping development compatibility where explicitly allowed.

## Source Documents

- [User Management Flow](../../../../business/flows/12_user_management_flow.md)
- [Users and Roles](../../../../business/users_and_roles.md)
- [User Management Design](../../../../design-guide/16-staff-user-management.html)

## Acceptance Criteria Impact

- [ ] Owner can log in with email and password and receive a protected session token.
- [ ] `/auth/me` returns the authenticated Owner from the token.
- [ ] Missing, invalid, suspended, or inactive sessions are blocked with stable auth errors.

## Business Rules To Preserve

- Suspended or inactive users cannot authenticate or continue protected sessions.
- Dev/test header auth may remain only outside production for compatibility.
- Backend remains the source of truth for authorization.

## Dependencies To Check First

- Depends on the persisted User model and Owner bootstrap seed from `USR-EP1-US0-BE1`.

## Implementation Plan

1. Add `POST /auth/login` with email/password DTO validation.
2. Verify credentials against the stored password hash.
3. Return `401` for bad credentials and `403` for inactive or suspended users.
4. Issue a signed JWT containing stable subject and role context.
5. Update `/auth/me` to read Bearer JWT, verify it, load the current user, and return the existing permission/workspace contract.
6. Keep development header auth only in non-production environments for tests and local compatibility.
7. Ensure protected guards block inactive or suspended users before controller logic runs.

## Backend Contract Expectations

`POST /auth/login` request:

```json
{
  "email": "owner@example.com",
  "password": "secure-password"
}
```

Success response:

```json
{
  "accessToken": "jwt",
  "user": {
    "id": "uuid",
    "email": "owner@example.com",
    "fullName": "Owner Name",
    "role": "OWNER",
    "status": "ACTIVE"
  }
}
```

Errors:

- `400` invalid payload.
- `401` bad credentials or missing/invalid token.
- `403` suspended or inactive user.

## Test Plan

- [ ] Add or update tests for successful login.
- [ ] Add or update tests for wrong password.
- [ ] Add or update tests for `/auth/me` from Bearer JWT.
- [ ] Add or update tests for missing or invalid token.
- [ ] Add or update tests for suspended or inactive user blocking.
- [ ] Record the test command in the agent handoff note.

## Definition of Done

- [ ] Implementation matches this task plan and the linked story acceptance criteria.
- [ ] Required API/service behavior is implemented in the correct module boundary.
- [ ] Authorization and active-user checks are enforced.
- [ ] Tests are added or an explicit test gap is recorded as a blocker.
- [ ] This task checkbox is marked complete in the story file and source module summary.
- [ ] [Progress Tracker](../../../progress_tracker.md) is updated with the completed task count.

## Handoff Note Template

```text
Module: USR
Story: USR-EP1-US0
Completed task: USR-EP1-US0-BE2
Files changed:
Tests run:
Tracker updated:
Open blockers:
Next recommended task:
```
