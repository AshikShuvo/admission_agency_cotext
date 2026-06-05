# USR-EP1-US0-BE3: Add auth tests for login, active status, bad password, suspended/blocking behavior.
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

This task proves the login and current-user behavior before staff creation work begins.

## Source Documents

- [User Management Flow](../../../../business/flows/12_user_management_flow.md)
- [Users and Roles](../../../../business/users_and_roles.md)
- [User Management Design](../../../../design-guide/16-staff-user-management.html)

## Acceptance Criteria Impact

- [ ] Owner account is seeded idempotently from environment-provided bootstrap values.
- [ ] Owner can log in with email and password and receive a protected session token.
- [ ] Missing, invalid, suspended, or inactive sessions are blocked with stable auth errors.

## Business Rules To Preserve

- Only active users can authenticate or load current user context.
- Bad credentials must not disclose whether the email exists.
- Tests must not expose real secrets or plaintext passwords outside test fixtures.

## Dependencies To Check First

- Depends on `USR-EP1-US0-BE1` and `USR-EP1-US0-BE2`.

## Implementation Plan

1. Add backend tests for Owner bootstrap seed creation and idempotency.
2. Add login success test using the configured Owner credentials.
3. Add bad password test returning `401`.
4. Add `/auth/me` test using a valid Bearer token.
5. Add missing and invalid token tests returning `401`.
6. Add inactive or suspended user tests returning `403`.
7. Confirm dev/test header auth remains limited to non-production if retained.

## Backend Contract Expectations

- Test the public API contract and service boundaries, not private implementation details only.
- Keep test fixtures deterministic and isolated.
- Record the exact validation commands in the handoff note.

## Test Plan

- [ ] `pnpm --filter @admission-agency/api lint`
- [ ] `pnpm --filter @admission-agency/api typecheck`
- [ ] `pnpm --filter @admission-agency/api test`

## Definition of Done

- [ ] Implementation matches this task plan and the linked story acceptance criteria.
- [ ] Required API/service behavior is covered by automated tests.
- [ ] Authorization and active-user blocking are tested.
- [ ] This task checkbox is marked complete in the story file and source module summary.
- [ ] [Progress Tracker](../../../progress_tracker.md) is updated with the completed task count.

## Handoff Note Template

```text
Module: USR
Story: USR-EP1-US0
Completed task: USR-EP1-US0-BE3
Files changed:
Tests run:
Tracker updated:
Open blockers:
Next recommended task:
```
