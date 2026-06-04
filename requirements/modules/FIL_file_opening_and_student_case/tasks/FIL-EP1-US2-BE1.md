# FIL-EP1-US2-BE1: Create file/case entity with status, assignment, program links, and file number.
## Detailed Backend Task Plan

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `FIL` - File Opening and Student Case |
| EPIC | [FIL-EP1: Student Profile and File Creation](../epics/FIL-EP1_student_profile_and_file_creation.md) |
| User Story | [FIL-EP1-US2: Create Student File](../stories/FIL-EP1-US2_create_student_file.md) |
| Task Type | `BE` |

## Business Context

As a Consultant, I want to create a student file from the selected program so that the agency can start the official workflow.

This task supports the module goal: Create the central student file, copy the selected package fees into immutable file fee records, assign the consultant, and prepare the file for payment confirmation and admission processing.

## Source Documents

- [File Opening Flow](../../../../business/flows/03_file_opening_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [File Opening Design](../../../../design-guide/07-file-opening.html)
- [Student File Detail Design](../../../../design-guide/08-student-file-detail.html)

## Acceptance Criteria Impact

- [ ] File links student, consultant, country, university, and program.
- [ ] System generates a unique file number.
- [ ] Initial status is `File Opened` or `Pending Payment - File Opening`.

## Business Rules To Preserve

- Consultants only manage assigned files.
- File numbers are unique.
- Package fees are copied at creation time.
- File history is preserved.

## Dependencies To Check First

- Depends on CAT active package and CNS selected program context.

## Implementation Plan

1. Implement inside the NestJS Students, Files / Cases, File Fees ownership boundary unless an explicit dependency requires another module.
2. Define or update Prisma/NestJS entities, DTOs, enums, and validation rules needed by the task.
3. Implement service-layer business logic first; controllers should stay thin and call typed service methods.
4. Apply authorization guards and query-level scope filters before reading or mutating protected records.
5. Persist audit log or notification events when the task changes sensitive business state.
6. Return role-appropriate response shapes and exclude sensitive fields for restricted roles.
7. Add unit tests for business rules and integration tests for API behavior, persistence, and authorization.
8. Add database constraints for required relationships, uniqueness, active/inactive state, and immutable historical records where applicable.

## Backend Contract Expectations

- Backend module ownership: `Students, Files / Cases, File Fees`.
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
Module: FIL
Story: FIL-EP1-US2
Completed task: FIL-EP1-US2-BE1
Files changed:
Tests run:
Tracker updated:
Open blockers:
Next recommended task:
```
