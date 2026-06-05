# ACL-EP1-US2-BE1: Standardize forbidden responses and authorization error handling.
## Detailed Backend Task Plan

Status: `Completed`
Owner: `Hegel`
Last updated: `2026-06-05`

## Traceability

| Level | Reference |
|---|---|
| Module | `ACL` - Access Control and Role Visibility |
| EPIC | [ACL-EP1: Role Permissions](../epics/ACL-EP1_role_permissions.md) |
| User Story | [ACL-EP1-US2: Block Unauthorized Direct Access](../stories/ACL-EP1-US2_block_unauthorized_direct_access.md) |
| Task Type | `BE` |

## Business Context

As the agency, I want direct route or API access blocked so that users cannot bypass UI restrictions.

This task supports the module goal: Ensure every screen, API, query, and action respects the user's role and data scope. UI hiding is not enough; access must be enforced by backend authorization and query-level filters.

## Source Documents

- [Access Control and Role Visibility Flow](../../../../business/flows/10_access_control_and_role_visibility_flow.md)
- [Users and Roles](../../../../business/users_and_roles.md)
- [Access Control Architecture](../../../../architecture/access_control.md)

## Acceptance Criteria Impact

- [x] Unauthorized API calls return a clear forbidden response.
- [x] Unauthorized frontend routes show restricted access or redirect to allowed dashboard.
- [x] Unauthorized attempts can be audited for sensitive resources.

## Business Rules To Preserve

- Backend authorization is mandatory.
- UI hiding is not enough.
- Sensitive fields are filtered by role.

## Dependencies To Check First

- Depends on role model from business/users_and_roles.md and applies to all modules.

## Implementation Plan

1. Implement inside the NestJS Auth and Users ownership boundary unless an explicit dependency requires another module.
2. Define or update Prisma/NestJS entities, DTOs, enums, and validation rules needed by the task.
3. Implement service-layer business logic first; controllers should stay thin and call typed service methods.
4. Apply authorization guards and query-level scope filters before reading or mutating protected records.
5. Persist audit log or notification events when the task changes sensitive business state.
6. Return role-appropriate response shapes and exclude sensitive fields for restricted roles.
7. Add unit tests for business rules and integration tests for API behavior, persistence, and authorization.

## Backend Contract Expectations

- Backend module ownership: `Auth and Users`.
- Use NestJS services/controllers, TypeScript DTOs, Prisma/PostgreSQL persistence, and JWT role context when implementation begins.
- Required enforcement: authentication, role permission, query-level data scope, input validation, and business-rule validation.
- REST/API reference: `../../../../architecture/api_design.md` from repository root.
- Access-control reference: `../../../../architecture/access_control.md` from repository root.

## Data, State, and Error Handling

- Identify all required fields from the story acceptance criteria before implementation.
- Keep IDs stable and use backend-generated identifiers for persisted records.
- Handle not found, forbidden, validation error, duplicate/conflict, and workflow-blocked responses.
- Preserve historical records when the business flow says data must not be deleted or overwritten.
- Do not expose restricted fields in UI state, API responses, logs, or test fixtures.

## Test Plan

- [x] Add or update automated tests for the normal successful path.
- [x] Add or update tests for at least one blocked or invalid path.
- [x] Add role/access tests when task touches restricted data or actions.
- [x] Confirm test data includes the minimum business objects needed for this story.
- [x] Record the test command in the agent handoff note.

## Definition of Done

- [x] Implementation matches this task plan and the linked story acceptance criteria.
- [x] Required UI/API/service behavior is implemented in the correct module boundary.
- [x] Authorization and data visibility are enforced where applicable.
- [x] Tests are added or an explicit test gap is recorded as a blocker.
- [x] This task checkbox is marked complete in the story file and source module summary.
- [x] [Progress Tracker](../../../progress_tracker.md) is updated with the completed task count.

## Handoff Note Template

```text
Module: ACL
Story: ACL-EP1-US2
Completed task: ACL-EP1-US2-BE1
Files changed:
Tests run:
Tracker updated:
Open blockers:
Next recommended task:
```
