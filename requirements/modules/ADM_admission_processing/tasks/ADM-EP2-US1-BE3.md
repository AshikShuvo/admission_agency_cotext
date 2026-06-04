# ADM-EP2-US1-BE3: Add integration tests for admission submission gates.
## Detailed Backend Task Plan

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `ADM` - Admission Processing |
| EPIC | [ADM-EP2: University Application and Admission Approval](../epics/ADM-EP2_university_application_and_admission_approval.md) |
| User Story | [ADM-EP2-US1: Submit University Application](../stories/ADM-EP2-US1_submit_university_application.md) |
| Task Type | `BE` |

## Business Context

As an Admission user, I want to record university application submission so that the agency can track when the application was sent.

This task supports the module goal: Manage admission document requests, document verification, university application submission, offer letter upload, and admission approval while enforcing document completeness and admission-stage payment clearance.

## Source Documents

- [Admission Processing Flow](../../../../business/flows/05_admission_processing_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [Admission Workbench Design](../../../../design-guide/10-admission-workbench.html)

## Acceptance Criteria Impact

- [ ] Application submission requires complete admission documents.
- [ ] Application submission requires admission-stage financial clearance.
- [ ] Submission date and expected response timeline are recorded.

## Business Rules To Preserve

- Admission approval requires documents and payment clearance.
- Admission users cannot see commission data.
- All document status changes are logged.

## Dependencies To Check First

- Depends on FIL file status and PAY clearance.

## Implementation Plan

1. Implement inside the NestJS Admission, Documents ownership boundary unless an explicit dependency requires another module.
2. Define or update Prisma/NestJS entities, DTOs, enums, and validation rules needed by the task.
3. Implement service-layer business logic first; controllers should stay thin and call typed service methods.
4. Apply authorization guards and query-level scope filters before reading or mutating protected records.
5. Persist audit log or notification events when the task changes sensitive business state.
6. Return role-appropriate response shapes and exclude sensitive fields for restricted roles.
7. Add unit tests for business rules and integration tests for API behavior, persistence, and authorization.
8. Include fixtures for allowed and blocked roles, valid and invalid inputs, and important workflow states.
9. Add transaction-safe checks so the workflow cannot advance when required payment, document, or status prerequisites fail.

## Backend Contract Expectations

- Backend module ownership: `Admission, Documents`.
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
Module: ADM
Story: ADM-EP2-US1
Completed task: ADM-EP2-US1-BE3
Files changed:
Tests run:
Tracker updated:
Open blockers:
Next recommended task:
```
