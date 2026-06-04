# VIS-EP2-US2-BE2: Enforce immutable completed-file behavior except Owner-authorized changes.
## Detailed Backend Task Plan

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `VIS` - Visa Processing |
| EPIC | [VIS-EP2: Visa Outcome and File Completion](../epics/VIS-EP2_visa_outcome_and_file_completion.md) |
| User Story | [VIS-EP2-US2: Complete Student File](../stories/VIS-EP2-US2_complete_student_file.md) |
| Task Type | `BE` |

## Business Context

As a Visa user or Owner, I want to mark the file complete after student departure or enrollment confirmation so that the case lifecycle is closed.

This task supports the module goal: Manage visa document collection, visa application submission, payment clearance, outcome recording, rejection handling, and completion of the student file.

## Source Documents

- [Visa Processing Flow](../../../../business/flows/06_visa_processing_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [Visa Workbench Design](../../../../design-guide/11-visa-workbench.html)

## Acceptance Criteria Impact

- [ ] Completion requires approved visa or Owner-approved closure rule.
- [ ] Completion details include departure or enrollment confirmation notes.
- [ ] Completed file is locked from normal edits.

## Business Rules To Preserve

- Visa approval/completion requires documents and payment clearance.
- Visa rejection preserves history.
- Visa users cannot see commission data.

## Dependencies To Check First

- Depends on ADM approval, offer letter, and PAY clearance.

## Implementation Plan

1. Implement inside the NestJS Visa, Documents ownership boundary unless an explicit dependency requires another module.
2. Define or update Prisma/NestJS entities, DTOs, enums, and validation rules needed by the task.
3. Implement service-layer business logic first; controllers should stay thin and call typed service methods.
4. Apply authorization guards and query-level scope filters before reading or mutating protected records.
5. Persist audit log or notification events when the task changes sensitive business state.
6. Return role-appropriate response shapes and exclude sensitive fields for restricted roles.
7. Add unit tests for business rules and integration tests for API behavior, persistence, and authorization.

## Backend Contract Expectations

- Backend module ownership: `Visa, Documents`.
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
Module: VIS
Story: VIS-EP2-US2
Completed task: VIS-EP2-US2-BE2
Files changed:
Tests run:
Tracker updated:
Open blockers:
Next recommended task:
```
