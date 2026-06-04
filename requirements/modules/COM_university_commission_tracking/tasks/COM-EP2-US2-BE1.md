# COM-EP2-US2-BE1: Add owner revenue summary query with separate commission aggregation.
## Detailed Backend Task Plan

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `COM` - University Commission Tracking |
| EPIC | [COM-EP2: Commission Reporting](../epics/COM-EP2_commission_reporting.md) |
| User Story | [COM-EP2-US2: Include Commission in Owner Revenue Summary](../stories/COM-EP2-US2_include_commission_in_owner_revenue_summary.md) |
| Task Type | `BE` |

## Business Context

As an Owner, I want commission included in owner-only revenue summaries so that I can see total business income.

This task supports the module goal: Allow the Owner to record confidential university commission revenue for completed or enrolled student files and include it only in Owner-visible reports.

## Source Documents

- [University Commission Tracking Flow](../../../../business/flows/07_university_commission_tracking_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [Commission Tracking Design](../../../../design-guide/12-commission-tracking.html)

## Acceptance Criteria Impact

- [ ] Owner revenue summary includes commission total separately from student payments.
- [ ] Commission totals can be filtered by date range and university.
- [ ] Accounts reports do not include commission totals.

## Business Rules To Preserve

- Commission is Owner-only.
- Commission records link to file and university.
- Non-owner responses must exclude commission data.

## Dependencies To Check First

- Depends on VIS completion/enrollment and ACL Owner-only access.

## Implementation Plan

1. Implement inside the NestJS Commissions ownership boundary unless an explicit dependency requires another module.
2. Define or update Prisma/NestJS entities, DTOs, enums, and validation rules needed by the task.
3. Implement service-layer business logic first; controllers should stay thin and call typed service methods.
4. Apply authorization guards and query-level scope filters before reading or mutating protected records.
5. Persist audit log or notification events when the task changes sensitive business state.
6. Return role-appropriate response shapes and exclude sensitive fields for restricted roles.
7. Add unit tests for business rules and integration tests for API behavior, persistence, and authorization.

## Backend Contract Expectations

- Backend module ownership: `Commissions`.
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
Module: COM
Story: COM-EP2-US2
Completed task: COM-EP2-US2-BE1
Files changed:
Tests run:
Tracker updated:
Open blockers:
Next recommended task:
```
