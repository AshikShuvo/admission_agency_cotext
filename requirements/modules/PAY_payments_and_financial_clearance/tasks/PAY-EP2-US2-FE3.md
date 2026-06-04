# PAY-EP2-US2-FE3: Add tests for blocked and cleared stage action states.
## Detailed Frontend Task Plan

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `PAY` - Payments and Financial Clearance |
| EPIC | [PAY-EP2: Due Calculation and Stage Gates](../epics/PAY-EP2_due_calculation_and_stage_gates.md) |
| User Story | [PAY-EP2-US2: Enforce Financial Clearance Gates](../stories/PAY-EP2-US2_enforce_financial_clearance_gates.md) |
| Task Type | `FE` |

## Business Context

As the agency, I want stages blocked until required payment is cleared so that processing does not advance without payment control.

This task supports the module goal: Record student payments, confirm deposits, calculate dues, and expose financial clearance so file stages cannot advance before required payment confirmation.

## Source Documents

- [Payment and Deposit Confirmation Flow](../../../../business/flows/04_payment_and_deposit_confirmation_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [Payment Deposit Workbench Design](../../../../design-guide/09-payment-deposit-workbench.html)

## Acceptance Criteria Impact

- [ ] Admission cannot start until File Opening is financially cleared.
- [ ] Admission approval cannot happen until Admission payment is cleared.
- [ ] Visa approval cannot happen until Visa payment is cleared.

## Business Rules To Preserve

- Only Accounts or Owner can record/confirm payments.
- Unconfirmed payments do not reduce dues.
- Payment gates block stage advancement.

## Dependencies To Check First

- Depends on FIL file fee snapshot.

## Implementation Plan

1. Locate or create the Accounts Payment Workspace route or workspace section that owns this behavior.
2. Create typed UI models for the data needed by the story; keep field names aligned with the backend DTO/API contract.
3. Build the screen, panel, form, table, queue, or state component described by the task with loading, empty, success, and error states.
4. Apply role-aware behavior using authenticated user role and backend permission response; do not rely on visual hiding for security decisions.
5. Connect mutation actions to API calls only after backend contract exists; otherwise document the missing contract as a blocker.
6. Add user-visible validation for required fields, invalid transitions, duplicate warnings, and blocked workflow states mentioned by acceptance criteria.
7. Add frontend coverage for the happy path and at least one blocked/error path. Prefer Playwright for full role flows and component tests only for risky reusable pieces.
8. Write tests that assert the visible business outcome, not only that components render.
9. Test at least two roles: one allowed role and one restricted role.

## UI and Contract Expectations

- Frontend workspace: `Accounts Payment Workspace`.
- Use Next.js, TypeScript, Tailwind CSS, and React Query patterns when implementation begins.
- Prefer API-driven permissions and response fields over hardcoded role assumptions.
- Required states: loading, empty, successful data, validation error, authorization-restricted, and server error.
- Design reference: `../../../../design-guide/09-payment-deposit-workbench.html`.

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
Story: PAY-EP2-US2
Completed task: PAY-EP2-US2-FE3
Files changed:
Tests run:
Tracker updated:
Open blockers:
Next recommended task:
```
