# PAY-EP1-US1: Record Student Payment
## Detailed User Story

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `PAY` - Payments and Financial Clearance |
| EPIC | [PAY-EP1: Payment Recording and Confirmation](../epics/PAY-EP1_payment_recording_and_confirmation.md) |

## Story Statement

As an Accounts user, I want to record a payment against a file and stage so that the agency can track received money.

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

- [ ] Payment records include file, stage, amount, method, date, and reference.
- [ ] Payments can be marked pending until verification.
- [ ] Partial payments are allowed.

## Business Rules

- Only Accounts or Owner can record/confirm payments.
- Unconfirmed payments do not reduce dues.
- Payment gates block stage advancement.

## Dependencies and Preconditions

- Depends on FIL file fee snapshot.

## Frontend Tasks

- [ ] [PAY-EP1-US1-FE1](../tasks/PAY-EP1-US1-FE1.md): Build payment entry form with file lookup and stage selection.
- [ ] [PAY-EP1-US1-FE2](../tasks/PAY-EP1-US1-FE2.md): Add validation for amount, date, method, and duplicate reference warning.
- [ ] [PAY-EP1-US1-FE3](../tasks/PAY-EP1-US1-FE3.md): Add tests for payment creation and partial payment entry.

## Backend Tasks

- [ ] [PAY-EP1-US1-BE1](../tasks/PAY-EP1-US1-BE1.md): Create payment entity with stage enum, amount, method, reference, and confirmation status.
- [ ] [PAY-EP1-US1-BE2](../tasks/PAY-EP1-US1-BE2.md): Implement accounts-only payment create API.
- [ ] [PAY-EP1-US1-BE3](../tasks/PAY-EP1-US1-BE3.md): Add tests for partial payments, invalid amounts, and role restrictions.

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
