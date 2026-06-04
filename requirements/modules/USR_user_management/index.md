# User Management
## Independent Requirement Module Folder

Module ID: `USR`

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Module Goal

Allow Owner to create, update, suspend, and audit internal staff accounts so every user has the correct role before accessing files, payments, documents, reports, catalog records, or commissions.

## Primary Actors

- Owner / Admin
- System
- Managed Consultant
- Managed Accounts user
- Managed Admission user
- Managed Visa user

## Source Documents

- [User Management Flow](../../../business/flows/12_user_management_flow.md)
- [Users and Roles](../../../business/users_and_roles.md)
- [User Management Design](../../../design-guide/16-staff-user-management.html)

## Architecture Routing

| Area | Owner |
|---|---|
| Frontend workspace | Owner Reports and Settings |
| Backend module boundary | Auth and Users |
| Design reference | ../../../design-guide/16-staff-user-management.html |

## Business Rules

- Only Owner manages staff users.
- Each user has one primary role unless explicitly approved.
- Suspension blocks access without deleting history.

## Dependencies

- Depends on ACL role model and audit logging.

## EPIC Files

- [ ] [USR-EP1: Staff Account Lifecycle](epics/USR-EP1_staff_account_lifecycle.md)
- [ ] [USR-EP2: Suspension and User Audit](epics/USR-EP2_suspension_and_user_audit.md)

## User Story Files

- [ ] [USR-EP1-US1: Create Staff User](stories/USR-EP1-US1_create_staff_user.md)
- [ ] [USR-EP1-US2: Update Staff Details and Role](stories/USR-EP1-US2_update_staff_details_and_role.md)
- [ ] [USR-EP2-US1: Suspend Staff Access](stories/USR-EP2-US1_suspend_staff_access.md)
- [ ] [USR-EP2-US2: Audit User Management Actions](stories/USR-EP2-US2_audit_user_management_actions.md)

## Task Implementation Plans

- [ ] [USR-EP1-US1-FE1](tasks/USR-EP1-US1-FE1.md): Build staff user creation form with role and department fields.
- [ ] [USR-EP1-US1-FE2](tasks/USR-EP1-US1-FE2.md): Show role scope and restricted areas before save.
- [ ] [USR-EP1-US1-FE3](tasks/USR-EP1-US1-FE3.md): Add tests for required fields, duplicate email error, and role scope preview.
- [ ] [USR-EP1-US1-BE1](tasks/USR-EP1-US1-BE1.md): Create user entity fields for profile, role, department, status, and login email.
- [ ] [USR-EP1-US1-BE2](tasks/USR-EP1-US1-BE2.md): Implement owner-only user creation API with unique email validation.
- [ ] [USR-EP1-US1-BE3](tasks/USR-EP1-US1-BE3.md): Add tests for owner-only creation, duplicate email, and created status.
- [ ] [USR-EP1-US2-FE1](tasks/USR-EP1-US2-FE1.md): Build staff detail/edit screen with current role and status.
- [ ] [USR-EP1-US2-FE2](tasks/USR-EP1-US2-FE2.md): Require reason when role or access status changes.
- [ ] [USR-EP1-US2-FE3](tasks/USR-EP1-US2-FE3.md): Add tests for role change reason and preserved user identity display.
- [ ] [USR-EP1-US2-BE1](tasks/USR-EP1-US2-BE1.md): Implement staff update API with role/status change reason validation.
- [ ] [USR-EP1-US2-BE2](tasks/USR-EP1-US2-BE2.md): Record audit entries for changed fields, actor, timestamp, and reason.
- [ ] [USR-EP1-US2-BE3](tasks/USR-EP1-US2-BE3.md): Add tests for role changes, audit log, and activity identity preservation.
- [ ] [USR-EP2-US1-FE1](tasks/USR-EP2-US1-FE1.md): Build suspend action with warning and required reason.
- [ ] [USR-EP2-US1-FE2](tasks/USR-EP2-US1-FE2.md): Show suspended status in user lists and detail pages.
- [ ] [USR-EP2-US1-FE3](tasks/USR-EP2-US1-FE3.md): Add tests for suspension confirmation and suspended status display.
- [ ] [USR-EP2-US1-BE1](tasks/USR-EP2-US1-BE1.md): Implement suspension API with reason, actor, timestamp, and status update.
- [ ] [USR-EP2-US1-BE2](tasks/USR-EP2-US1-BE2.md): Block login/session access for suspended users.
- [ ] [USR-EP2-US1-BE3](tasks/USR-EP2-US1-BE3.md): Add tests for suspension, login blocking, and historical activity preservation.
- [ ] [USR-EP2-US2-FE1](tasks/USR-EP2-US2-FE1.md): Build user audit history panel on staff detail page.
- [ ] [USR-EP2-US2-FE2](tasks/USR-EP2-US2-FE2.md): Add filters for action type and date range.
- [ ] [USR-EP2-US2-FE3](tasks/USR-EP2-US2-FE3.md): Add tests for audit rendering and owner-only visibility.
- [ ] [USR-EP2-US2-BE1](tasks/USR-EP2-US2-BE1.md): Implement user audit history API with action filters.
- [ ] [USR-EP2-US2-BE2](tasks/USR-EP2-US2-BE2.md): Enforce owner-only access to user audit records.
- [ ] [USR-EP2-US2-BE3](tasks/USR-EP2-US2-BE3.md): Add tests for audit filtering, owner-only access, and event completeness.

## Folder Completion Rules

- [ ] Every EPIC file is complete.
- [ ] Every story file is accepted.
- [ ] Every task implementation plan is completed or explicitly deferred with an approved blocker.
- [ ] Module row is updated in [Progress Tracker](../../progress_tracker.md).
- [ ] Completion log records meaningful milestone completion.
