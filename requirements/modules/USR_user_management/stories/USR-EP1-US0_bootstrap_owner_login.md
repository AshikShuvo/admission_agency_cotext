# USR-EP1-US0: Bootstrap Owner Login
## Detailed User Story

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-05`

## Traceability

| Level | Reference |
|---|---|
| Module | `USR` - User Management |
| EPIC | [USR-EP1: Staff Account Lifecycle](../epics/USR-EP1_staff_account_lifecycle.md) |

## Story Statement

As an Owner, I want a bootstrapped account and secure login so that I can access the system and create staff users.

## Business Expectation

This story unlocks browser-usable user management. Staff creation, suspension, and audit workflows cannot be accepted until a real Owner can authenticate, hold a protected session, and load current user context from that session.

## Primary Actors

- Owner / Admin
- System

## Source Documents

- [User Management Flow](../../../../business/flows/12_user_management_flow.md)
- [Users and Roles](../../../../business/users_and_roles.md)
- [User Management Design](../../../../design-guide/16-staff-user-management.html)

## Acceptance Criteria

- [ ] Owner account is seeded idempotently from environment-provided bootstrap values.
- [ ] Owner can log in with email and password and receive a protected session token.
- [ ] `/auth/me` returns the authenticated Owner from the token.
- [ ] Missing, invalid, suspended, or inactive sessions are blocked with stable auth errors.
- [ ] Frontend login stores the session securely and redirects authenticated Owner into an allowed workspace.

## Business Rules

- First Owner bootstrap is environment-controlled and idempotent.
- Password hashes are never exposed in API responses, logs, UI state, or tests.
- Staff creation does not start until Owner login is accepted.
- Dev/test header auth may remain only outside production for compatibility.
- Suspended or inactive users cannot authenticate or continue protected sessions.

## Dependencies and Preconditions

- Depends on ACL role model and direct-access enforcement.
- Depends on Auth and Users module boundaries being available in the application scaffold.

## Frontend Tasks

- [ ] [USR-EP1-US0-FE1](../tasks/USR-EP1-US0-FE1.md): Build login page from design guide.
- [ ] [USR-EP1-US0-FE2](../tasks/USR-EP1-US0-FE2.md): Store session securely and load current user from real token.
- [ ] [USR-EP1-US0-FE3](../tasks/USR-EP1-US0-FE3.md): Add frontend tests for login states and authenticated route access.

## Backend Tasks

- [ ] [USR-EP1-US0-BE1](../tasks/USR-EP1-US0-BE1.md): Add persisted user auth fields and bootstrap Owner seed.
- [ ] [USR-EP1-US0-BE2](../tasks/USR-EP1-US0-BE2.md): Implement login, JWT issuance, and `/auth/me` from token.
- [ ] [USR-EP1-US0-BE3](../tasks/USR-EP1-US0-BE3.md): Add auth tests for login, active status, bad password, suspended/blocking behavior.

## Cross-Agent Contract

- Backend owns user persistence, password verification, token issuance, `/auth/me`, and inactive-user blocking.
- Frontend owns login UI, secure cookie session handoff, current-user loading, unauthenticated redirects, and login error states.
- QA/review owns acceptance verification across frontend, backend, and protected-route behavior.
- If the frontend and backend agents disagree on API shape, pause the story and add a blocker to [Progress Tracker](../../../progress_tracker.md).

## Detailed Acceptance Review Checklist

- [ ] Owner bootstrap creates exactly one usable Owner account for the configured email.
- [ ] Owner can complete the login happy path.
- [ ] Bad credentials and inactive/suspended users are blocked.
- [ ] `/auth/me` is backed by the real token, not only development headers.
- [ ] Frontend route protection uses the authenticated session and preserves ACL restricted-route behavior.
- [ ] Automated tests cover the success path and at least one failure or restricted path.

## Completion Rules

- [ ] All linked frontend tasks are complete.
- [ ] All linked backend tasks are complete.
- [ ] Acceptance criteria are verified by QA/review.
- [ ] Story count is updated in [Progress Tracker](../../../progress_tracker.md).
- [ ] EPIC progress is recalculated after this story is accepted.
