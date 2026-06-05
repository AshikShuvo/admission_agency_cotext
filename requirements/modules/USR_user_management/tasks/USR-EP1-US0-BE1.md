# USR-EP1-US0-BE1: Add persisted user auth fields and bootstrap Owner seed.
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

This task establishes the persisted user record needed before any staff lifecycle workflow can be usable.

## Source Documents

- [User Management Flow](../../../../business/flows/12_user_management_flow.md)
- [Users and Roles](../../../../business/users_and_roles.md)
- [User Management Design](../../../../design-guide/16-staff-user-management.html)

## Acceptance Criteria Impact

- [ ] Owner account is seeded idempotently from environment-provided bootstrap values.
- [ ] Password hashes are never exposed.

## Business Rules To Preserve

- First Owner bootstrap is environment-controlled and idempotent.
- Only active users can hold a valid session.
- Staff creation waits until Owner login is accepted.

## Dependencies To Check First

- Depends on ACL role model and direct-access enforcement.

## Implementation Plan

1. Add a persisted `User` model with `id`, `fullName`, `email`, `passwordHash`, `role`, `status`, `department`, `phone`, `createdAt`, and `updatedAt`.
2. Add enums or typed constants for supported roles, user status, and department values.
3. Add unique email constraint and required indexes for login lookup.
4. Add password hashing helper with deterministic verification and no plaintext storage.
5. Add bootstrap Owner seed using `OWNER_EMAIL`, `OWNER_PASSWORD`, and `OWNER_FULL_NAME`.
6. Make Owner bootstrap idempotent by updating or skipping the configured Owner instead of creating duplicates.
7. Keep bootstrap behavior explicit and testable from the API startup or seed pathway.

## Backend Contract Expectations

- Backend module ownership: `Auth and Users`.
- Use Prisma/PostgreSQL persistence and NestJS services.
- Do not return `passwordHash` in any API response.
- Use environment validation for required bootstrap values where appropriate.

## Test Plan

- [ ] Add or update automated tests for Owner seed creation.
- [ ] Add or update tests proving repeated bootstrap does not duplicate Owner.
- [ ] Add tests proving password hashes are stored and plaintext is not exposed.
- [ ] Record the test command in the agent handoff note.

## Definition of Done

- [ ] Implementation matches this task plan and the linked story acceptance criteria.
- [ ] Required service behavior is implemented in the correct module boundary.
- [ ] Tests are added or an explicit test gap is recorded as a blocker.
- [ ] This task checkbox is marked complete in the story file and source module summary.
- [ ] [Progress Tracker](../../../progress_tracker.md) is updated with the completed task count.

## Handoff Note Template

```text
Module: USR
Story: USR-EP1-US0
Completed task: USR-EP1-US0-BE1
Files changed:
Tests run:
Tracker updated:
Open blockers:
Next recommended task:
```
