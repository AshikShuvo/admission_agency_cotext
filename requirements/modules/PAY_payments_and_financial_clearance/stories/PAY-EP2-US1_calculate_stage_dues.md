# PAY-EP2-US1: Calculate Stage Dues
## Detailed User Story

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `PAY` - Payments and Financial Clearance |
| EPIC | [PAY-EP2: Due Calculation and Stage Gates](../epics/PAY-EP2_due_calculation_and_stage_gates.md) |

## Story Statement

As a staff user, I want to see accurate stage dues so that I know whether the student has remaining payment obligations.

## Business Expectation

This story must convert the business expectation into a working system behavior that staff can use without relying on manual spreadsheets, side notes, or hidden process knowledge. The implementation must preserve the role boundaries, lifecycle rules, and data ownership described in the source business flow.

## Primary Actors

- Accounts
- Consultant, status visibility
- Admission, clearance visibility
- Visa, clearance visibility
- Owner

## Source Documents

- [Payment and Deposit Confirmation Flow](../../../../business/flows/04_payment_and_deposit_confirmation_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [Payment Deposit Workbench Design](../../../../design-guide/09-payment-deposit-workbench.html)

## Acceptance Criteria

- [ ] Due amount equals total stage fee minus confirmed payments for the stage.
- [ ] Pending payments are visible but do not reduce due.
- [ ] Due summary is available in file detail and accounts workspace.

## Business Rules

- Only Accounts or Owner can record/confirm payments.
- Unconfirmed payments do not reduce dues.
- Payment gates block stage advancement.

## Dependencies and Preconditions

- Depends on FIL file fee snapshot.

## Frontend Tasks

- [ ] [PAY-EP2-US1-FE1](../tasks/PAY-EP2-US1-FE1.md): Build stage-wise payment and due summary component.
- [ ] [PAY-EP2-US1-FE2](../tasks/PAY-EP2-US1-FE2.md): Show confirmed, pending, total fee, and due amounts separately.
- [ ] [PAY-EP2-US1-FE3](../tasks/PAY-EP2-US1-FE3.md): Add tests for partial, cleared, and pending payment display.

## Backend Tasks

- [ ] [PAY-EP2-US1-BE1](../tasks/PAY-EP2-US1-BE1.md): Implement due calculation service using file fee snapshots and confirmed payments.
- [ ] [PAY-EP2-US1-BE2](../tasks/PAY-EP2-US1-BE2.md): Add payment summary API scoped by role.
- [ ] [PAY-EP2-US1-BE3](../tasks/PAY-EP2-US1-BE3.md): Add tests for due formula, multi-payment totals, and pending exclusion.

## Cross-Agent Contract

- Backend owns persistence, authorization, workflow gates, audit events, and role-scoped API responses.
- Frontend owns the staff-facing workflow, visible states, validation feedback, and clear blocked-state messaging.
- QA/review owns acceptance verification across frontend, backend, and access-control behavior.
- If the frontend and backend agents disagree on API shape, pause the story and add a blocker to [Progress Tracker](../../../progress_tracker.md).

## Detailed Acceptance Review Checklist

- [ ] User can complete the happy path described by the story statement.
- [ ] User sees clear feedback when required data is missing or a workflow gate blocks progress.
- [ ] Unauthorized roles cannot perform the action through UI or API.
- [ ] Restricted data is not returned from the backend and is not rendered by the frontend.
- [ ] Important state changes create audit log or notification events where required by the business rules.
- [ ] Automated tests cover the success path and at least one failure or restricted path.

## Completion Rules

- [ ] All linked frontend tasks are complete.
- [ ] All linked backend tasks are complete.
- [ ] Acceptance criteria are verified by QA/review.
- [ ] Story count is updated in [Progress Tracker](../../../progress_tracker.md).
- [ ] EPIC progress is recalculated after this story is accepted.
