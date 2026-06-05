# Access Control and Role Visibility
## Independent Requirement Module Folder

Module ID: `ACL`

Status: `In Progress`
Owner: `Hegel / Lorentz / Gibbs`
Last updated: `2026-06-05`

## Module Goal

Ensure every screen, API, query, and action respects the user's role and data scope. UI hiding is not enough; access must be enforced by backend authorization and query-level filters.

## Primary Actors

- System
- Owner
- Consultant
- Accounts
- Admission
- Visa

## Source Documents

- [Access Control and Role Visibility Flow](../../../business/flows/10_access_control_and_role_visibility_flow.md)
- [Users and Roles](../../../business/users_and_roles.md)
- [Access Control Architecture](../../../architecture/access_control.md)

## Architecture Routing

| Area | Owner |
|---|---|
| Frontend workspace | All Workspaces |
| Backend module boundary | Auth and Users |
| Design reference | ../../../design-guide/14-notifications-access-exceptions.html |

## Business Rules

- Backend authorization is mandatory.
- UI hiding is not enough.
- Sensitive fields are filtered by role.

## Dependencies

- Depends on role model from business/users_and_roles.md and applies to all modules.

## EPIC Files

- [ ] [ACL-EP1: Role Permissions](epics/ACL-EP1_role_permissions.md)
- [ ] [ACL-EP2: Data Scope and Sensitive Field Filtering](epics/ACL-EP2_data_scope_and_sensitive_field_filtering.md)

## User Story Files

- [x] [ACL-EP1-US1: Enforce Role Permissions](stories/ACL-EP1-US1_enforce_role_permissions.md)
- [ ] [ACL-EP1-US2: Block Unauthorized Direct Access](stories/ACL-EP1-US2_block_unauthorized_direct_access.md)
- [ ] [ACL-EP2-US1: Apply Query-Level Data Scope](stories/ACL-EP2-US1_apply_query_level_data_scope.md)
- [ ] [ACL-EP2-US2: Filter Sensitive Fields](stories/ACL-EP2-US2_filter_sensitive_fields.md)

## Task Implementation Plans

- [x] [ACL-EP1-US1-FE1](tasks/ACL-EP1-US1-FE1.md): Build role-based navigation configuration for allowed workspaces.
- [x] [ACL-EP1-US1-FE2](tasks/ACL-EP1-US1-FE2.md): Add disabled or hidden action states based on backend permission data.
- [x] [ACL-EP1-US1-FE3](tasks/ACL-EP1-US1-FE3.md): Add tests for role-specific navigation and blocked actions.
- [x] [ACL-EP1-US1-BE1](tasks/ACL-EP1-US1-BE1.md): Implement role permission map for core modules and actions.
- [x] [ACL-EP1-US1-BE2](tasks/ACL-EP1-US1-BE2.md): Add NestJS guards or policy checks for protected routes and service actions.
- [x] [ACL-EP1-US1-BE3](tasks/ACL-EP1-US1-BE3.md): Add tests for allowed and blocked role actions across key modules.
- [ ] [ACL-EP1-US2-FE1](tasks/ACL-EP1-US2-FE1.md): Add protected route wrapper using current user permission data.
- [ ] [ACL-EP1-US2-FE2](tasks/ACL-EP1-US2-FE2.md): Build restricted access state for blocked routes.
- [ ] [ACL-EP1-US2-FE3](tasks/ACL-EP1-US2-FE3.md): Add tests for direct navigation to unauthorized screens.
- [ ] [ACL-EP1-US2-BE1](tasks/ACL-EP1-US2-BE1.md): Standardize forbidden responses and authorization error handling.
- [ ] [ACL-EP1-US2-BE2](tasks/ACL-EP1-US2-BE2.md): Add optional access audit log for sensitive blocked attempts.
- [ ] [ACL-EP1-US2-BE3](tasks/ACL-EP1-US2-BE3.md): Add tests for direct forbidden API access.
- [ ] [ACL-EP2-US1-FE1](tasks/ACL-EP2-US1-FE1.md): Consume scoped API responses without assuming hidden data exists.
- [ ] [ACL-EP2-US1-FE2](tasks/ACL-EP2-US1-FE2.md): Show role-appropriate filter options for file lists and reports.
- [ ] [ACL-EP2-US1-FE3](tasks/ACL-EP2-US1-FE3.md): Add tests for consultant and department scoped list behavior.
- [ ] [ACL-EP2-US1-BE1](tasks/ACL-EP2-US1-BE1.md): Implement reusable query scope helpers for file, payment, document, and report queries.
- [ ] [ACL-EP2-US1-BE2](tasks/ACL-EP2-US1-BE2.md): Apply scopes in Files, Payments, Admission, Visa, Documents, and Reporting services.
- [ ] [ACL-EP2-US1-BE3](tasks/ACL-EP2-US1-BE3.md): Add tests proving scopes are enforced in list, detail, and report APIs.
- [ ] [ACL-EP2-US2-FE1](tasks/ACL-EP2-US2-FE1.md): Render file detail sections only from fields returned by the backend.
- [ ] [ACL-EP2-US2-FE2](tasks/ACL-EP2-US2-FE2.md): Add fallback states when a section is not available for the role.
- [ ] [ACL-EP2-US2-FE3](tasks/ACL-EP2-US2-FE3.md): Add tests proving sensitive sections do not appear for restricted roles.
- [ ] [ACL-EP2-US2-BE1](tasks/ACL-EP2-US2-BE1.md): Implement response serializers or projection builders by role.
- [ ] [ACL-EP2-US2-BE2](tasks/ACL-EP2-US2-BE2.md): Apply sensitive field filtering to file detail, reports, payments, documents, and commissions.
- [ ] [ACL-EP2-US2-BE3](tasks/ACL-EP2-US2-BE3.md): Add tests for commission, document, visa, and financial field filtering.

## Folder Completion Rules

- [ ] Every EPIC file is complete.
- [ ] Every story file is accepted.
- [ ] Every task implementation plan is completed or explicitly deferred with an approved blocker.
- [ ] Module row is updated in [Progress Tracker](../../progress_tracker.md).
- [ ] Completion log records meaningful milestone completion.
