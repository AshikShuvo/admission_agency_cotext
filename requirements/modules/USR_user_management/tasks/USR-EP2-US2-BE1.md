# USR-EP2-US2-BE1: Implement user audit history API with action filters.
## Detailed Backend Task Plan

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `USR` - User Management |
| EPIC | [USR-EP2: Suspension and User Audit](../epics/USR-EP2_suspension_and_user_audit.md) |
| User Story | [USR-EP2-US2: Audit User Management Actions](../stories/USR-EP2-US2_audit_user_management_actions.md) |
| Task Type | `BE` |

## Business Context

As an Owner, I want to review user management audit history so that sensitive access changes are traceable.

This task supports the module goal: Allow Owner to create, update, suspend, and audit internal staff accounts so every user has the correct role before accessing files, payments, documents, reports, catalog records, or commissions.

## Source Documents

- [User Management Flow](../../../../business/flows/12_user_management_flow.md)
- [Users and Roles](../../../../business/users_and_roles.md)
- [User Management Design](../../../../design-guide/16-staff-user-management.html)

## Acceptance Criteria Impact

- [ ] Audit history shows who changed what, when, and why.
- [ ] Audit records include create, role change, status change, and suspension events.
- [ ] Non-owner users cannot view user management audit history.

## Business Rules To Preserve

- Only Owner manages staff users.
- Each user has one primary role unless explicitly approved.
- Suspension blocks access without deleting history.

## Dependencies To Check First

- Depends on ACL role model and audit logging.

## Implementation Plan

1. Implement inside the NestJS Auth and Users ownership boundary unless an explicit dependency requires another module.
2. Define or update Prisma/NestJS entities, DTOs, enums, and validation rules needed by the task.
3. Implement service-layer business logic first; controllers should stay thin and call typed service methods.
4. Apply authorization guards and query-level scope filters before reading or mutating protected records.
5. Persist audit log or notification events when the task changes sensitive business state.
6. Return role-appropriate response shapes and exclude sensitive fields for restricted roles.
7. Add unit tests for business rules and integration tests for API behavior, persistence, and authorization.
8. Document expected REST route, method, request body, response body, errors, and pagination/filter behavior if the endpoint lists records.

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

- [ ] Add or update automated tests for the normal successful path.
- [ ] Add or update tests for at least one blocked or invalid path.
- [ ] Add role/access tests when task touches restricted data or actions.
- [ ] Confirm test data includes the minimum business objects needed for this story.
- [ ] Record the test command in the agent handoff note.

## Definition of Done

- [ ] Implementation matches this task plan and the linked story acceptance criteria.
- [ ] Required UI/API/service behavior is implemented in the correct module boundary.
- [ ] Authorization and data visibility are enforced where applicable.
- [ ] Tests are added or an explicit test gap is recorded as a blocker.
- [ ] This task checkbox is marked complete in the story file and source module summary.
- [ ] [Progress Tracker](../../../progress_tracker.md) is updated with the completed task count.

## Handoff Note Template

```text
Module: USR
Story: USR-EP2-US2
Completed task: USR-EP2-US2-BE1
Files changed:
Tests run:
Tracker updated:
Open blockers:
Next recommended task:
```
