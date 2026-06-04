# CNS-EP1-US1-BE1: Add program search API with filters and active-package indicator.
## Detailed Backend Task Plan

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `CNS` - Counselling and Program Selection |
| EPIC | [CNS-EP1: Program Discovery for Counselling](../epics/CNS-EP1_program_discovery_for_counselling.md) |
| User Story | [CNS-EP1-US1: Search Active Programs](../stories/CNS-EP1-US1_search_active_programs.md) |
| Task Type | `BE` |

## Business Context

As a Consultant, I want to search active programs by counselling criteria so that I can find suitable options for a student.

This task supports the module goal: Help consultants search programs, compare package costs, check student fit, and start file opening only when a selected program has an active package.

## Source Documents

- [Counselling and Program Selection Flow](../../../../business/flows/02_counselling_and_program_selection_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [Counselling Program Selection Design](../../../../design-guide/06-counselling-program-selection.html)

## Acceptance Criteria Impact

- [ ] Consultant can filter by country, university, level, field, intake, and active status.
- [ ] Results clearly show whether a program has an active package.
- [ ] Consultant cannot edit catalog data from counselling screens.

## Business Rules To Preserve

- Consultants cannot edit catalog records.
- File opening requires active package.
- Counselling can exist before formal file creation.

## Dependencies To Check First

- Depends on CAT active catalog and active package lookup.

## Implementation Plan

1. Implement inside the NestJS Catalog, Students, Files / Cases ownership boundary unless an explicit dependency requires another module.
2. Define or update Prisma/NestJS entities, DTOs, enums, and validation rules needed by the task.
3. Implement service-layer business logic first; controllers should stay thin and call typed service methods.
4. Apply authorization guards and query-level scope filters before reading or mutating protected records.
5. Persist audit log or notification events when the task changes sensitive business state.
6. Return role-appropriate response shapes and exclude sensitive fields for restricted roles.
7. Add unit tests for business rules and integration tests for API behavior, persistence, and authorization.
8. Document expected REST route, method, request body, response body, errors, and pagination/filter behavior if the endpoint lists records.

## Backend Contract Expectations

- Backend module ownership: `Catalog, Students, Files / Cases`.
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
Module: CNS
Story: CNS-EP1-US1
Completed task: CNS-EP1-US1-BE1
Files changed:
Tests run:
Tracker updated:
Open blockers:
Next recommended task:
```
