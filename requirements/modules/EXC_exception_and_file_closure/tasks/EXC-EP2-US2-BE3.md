# EXC-EP2-US2-BE3: Add tests for completed lock, owner exception, and commission eligibility flag.
## Detailed Backend Task Plan

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `EXC` - Exception and File Closure |
| EPIC | [EXC-EP2: Rejection and Final Closure](../epics/EXC-EP2_rejection_and_final_closure.md) |
| User Story | [EXC-EP2-US2: Lock Completed Files](../stories/EXC-EP2-US2_lock_completed_files.md) |
| Task Type | `BE` |

## Business Context

As the agency, I want completed files locked from normal edits so that final records remain stable.

This task supports the module goal: Handle files that pause, cancel, complete, or receive visa rejection without deleting business history, payments, documents, or audit records.

## Source Documents

- [Exception and File Closure Flow](../../../../business/flows/11_exception_and_file_closure_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [Exception Closure Workbench Design](../../../../design-guide/18-exception-closure-workbench.html)
- [Locked File State Design](../../../../design-guide/20-locked-file-state.html)

## Acceptance Criteria Impact

- [ ] Completed file cannot be edited by normal role actions.
- [ ] Owner can authorize exceptional correction with reason.
- [ ] Completed file is eligible for commission tracking.

## Business Rules To Preserve

- Files are not deleted.
- Cancelled and completed files are locked from normal edits.
- Visa reapplication preserves previous history.

## Dependencies To Check First

- Depends on FIL status model, VIS rejection, and COM completion eligibility.

## Implementation Plan

1. Implement inside the NestJS Files / Cases ownership boundary unless an explicit dependency requires another module.
2. Define or update Prisma/NestJS entities, DTOs, enums, and validation rules needed by the task.
3. Implement service-layer business logic first; controllers should stay thin and call typed service methods.
4. Apply authorization guards and query-level scope filters before reading or mutating protected records.
5. Persist audit log or notification events when the task changes sensitive business state.
6. Return role-appropriate response shapes and exclude sensitive fields for restricted roles.
7. Add unit tests for business rules and integration tests for API behavior, persistence, and authorization.
8. Include fixtures for allowed and blocked roles, valid and invalid inputs, and important workflow states.

## Backend Contract Expectations

- Backend module ownership: `Files / Cases`.
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
Module: EXC
Story: EXC-EP2-US2
Completed task: EXC-EP2-US2-BE3
Files changed:
Tests run:
Tracker updated:
Open blockers:
Next recommended task:
```
