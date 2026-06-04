# CAT-EP1-US1-BE1: Create country and university entities with status fields, ownership timestamps, and unique constraints.
## Detailed Backend Task Plan

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `CAT` - Catalog and Packages |
| EPIC | [CAT-EP1: Master Catalog Management](../epics/CAT-EP1_master_catalog_management.md) |
| User Story | [CAT-EP1-US1: Manage Countries and Universities](../stories/CAT-EP1-US1_manage_countries_and_universities.md) |
| Task Type | `BE` |

## Business Context

As an Owner, I want to manage destination countries and universities so that the agency can keep the counselling catalog accurate.

This task supports the module goal: Allow the Owner to maintain countries, universities, programs, and active stage-wise packages so consultants can counsel students using accurate program and fee data.

## Source Documents

- [Catalog and Package Setup Flow](../../../../business/flows/01_catalog_and_package_setup_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [Catalog Package Management Design](../../../../design-guide/05-catalog-package-management.html)

## Acceptance Criteria Impact

- [ ] Owner can create and edit country records with active/inactive status.
- [ ] Owner can create and edit universities under a selected country.
- [ ] Non-owner users cannot create, edit, or deactivate catalog records.

## Business Rules To Preserve

- Only Owner can mutate catalog records.
- Consultants browse active records only.
- Only one active package is allowed per program.
- File creation must snapshot active package fees.

## Dependencies To Check First

- None for core catalog setup. It is an upstream dependency for counselling and file opening.

## Implementation Plan

1. Implement inside the NestJS Catalog ownership boundary unless an explicit dependency requires another module.
2. Define or update Prisma/NestJS entities, DTOs, enums, and validation rules needed by the task.
3. Implement service-layer business logic first; controllers should stay thin and call typed service methods.
4. Apply authorization guards and query-level scope filters before reading or mutating protected records.
5. Persist audit log or notification events when the task changes sensitive business state.
6. Return role-appropriate response shapes and exclude sensitive fields for restricted roles.
7. Add unit tests for business rules and integration tests for API behavior, persistence, and authorization.

## Backend Contract Expectations

- Backend module ownership: `Catalog`.
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
Module: CAT
Story: CAT-EP1-US1
Completed task: CAT-EP1-US1-BE1
Files changed:
Tests run:
Tracker updated:
Open blockers:
Next recommended task:
```
