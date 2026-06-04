# PAY-EP2-US1-BE3: Add tests for due formula, multi-payment totals, and pending exclusion.
## Detailed Backend Task Plan

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `PAY` - Payments and Financial Clearance |
| EPIC | [PAY-EP2: Due Calculation and Stage Gates](../epics/PAY-EP2_due_calculation_and_stage_gates.md) |
| User Story | [PAY-EP2-US1: Calculate Stage Dues](../stories/PAY-EP2-US1_calculate_stage_dues.md) |
| Task Type | `BE` |

## Business Context

As a staff user, I want to see accurate stage dues so that I know whether the student has remaining payment obligations.

This task supports the module goal: Record student payments, confirm deposits, calculate dues, and expose financial clearance so file stages cannot advance before required payment confirmation.

## Source Documents

- [Payment and Deposit Confirmation Flow](../../../../business/flows/04_payment_and_deposit_confirmation_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [Payment Deposit Workbench Design](../../../../design-guide/09-payment-deposit-workbench.html)

## Acceptance Criteria Impact

- [ ] Due amount equals total stage fee minus confirmed payments for the stage.
- [ ] Pending payments are visible but do not reduce due.
- [ ] Due summary is available in file detail and accounts workspace.

## Business Rules To Preserve

- Only Accounts or Owner can record/confirm payments.
- Unconfirmed payments do not reduce dues.
- Payment gates block stage advancement.

## Dependencies To Check First

- Depends on FIL file fee snapshot.

## Implementation Plan

1. Implement inside the NestJS Payments, File Fees ownership boundary unless an explicit dependency requires another module.
2. Define or update Prisma/NestJS entities, DTOs, enums, and validation rules needed by the task.
3. Implement service-layer business logic first; controllers should stay thin and call typed service methods.
4. Apply authorization guards and query-level scope filters before reading or mutating protected records.
5. Persist audit log or notification events when the task changes sensitive business state.
6. Return role-appropriate response shapes and exclude sensitive fields for restricted roles.
7. Add unit tests for business rules and integration tests for API behavior, persistence, and authorization.
8. Include fixtures for allowed and blocked roles, valid and invalid inputs, and important workflow states.

## Backend Contract Expectations

- Backend module ownership: `Payments, File Fees`.
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
Module: PAY
Story: PAY-EP2-US1
Completed task: PAY-EP2-US1-BE3
Files changed:
Tests run:
Tracker updated:
Open blockers:
Next recommended task:
```
