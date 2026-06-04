# Payments and Financial Clearance
## Independent Requirement Module Folder

Module ID: `PAY`

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Module Goal

Record student payments, confirm deposits, calculate dues, and expose financial clearance so file stages cannot advance before required payment confirmation.

## Primary Actors

- Accounts
- Consultant, status visibility
- Admission, clearance visibility
- Visa, clearance visibility
- Owner

## Source Documents

- [Payment and Deposit Confirmation Flow](../../../business/flows/04_payment_and_deposit_confirmation_flow.md)
- [Module Boundaries](../../../architecture/module_boundaries.md)
- [Payment Deposit Workbench Design](../../../design-guide/09-payment-deposit-workbench.html)

## Architecture Routing

| Area | Owner |
|---|---|
| Frontend workspace | Accounts Payment Workspace |
| Backend module boundary | Payments, File Fees |
| Design reference | ../../../design-guide/09-payment-deposit-workbench.html |

## Business Rules

- Only Accounts or Owner can record/confirm payments.
- Unconfirmed payments do not reduce dues.
- Payment gates block stage advancement.

## Dependencies

- Depends on FIL file fee snapshot.

## EPIC Files

- [ ] [PAY-EP1: Payment Recording and Confirmation](epics/PAY-EP1_payment_recording_and_confirmation.md)
- [ ] [PAY-EP2: Due Calculation and Stage Gates](epics/PAY-EP2_due_calculation_and_stage_gates.md)

## User Story Files

- [ ] [PAY-EP1-US1: Record Student Payment](stories/PAY-EP1-US1_record_student_payment.md)
- [ ] [PAY-EP1-US2: Confirm Verified Deposit](stories/PAY-EP1-US2_confirm_verified_deposit.md)
- [ ] [PAY-EP2-US1: Calculate Stage Dues](stories/PAY-EP2-US1_calculate_stage_dues.md)
- [ ] [PAY-EP2-US2: Enforce Financial Clearance Gates](stories/PAY-EP2-US2_enforce_financial_clearance_gates.md)

## Task Implementation Plans

- [ ] [PAY-EP1-US1-FE1](tasks/PAY-EP1-US1-FE1.md): Build payment entry form with file lookup and stage selection.
- [ ] [PAY-EP1-US1-FE2](tasks/PAY-EP1-US1-FE2.md): Add validation for amount, date, method, and duplicate reference warning.
- [ ] [PAY-EP1-US1-FE3](tasks/PAY-EP1-US1-FE3.md): Add tests for payment creation and partial payment entry.
- [ ] [PAY-EP1-US1-BE1](tasks/PAY-EP1-US1-BE1.md): Create payment entity with stage enum, amount, method, reference, and confirmation status.
- [ ] [PAY-EP1-US1-BE2](tasks/PAY-EP1-US1-BE2.md): Implement accounts-only payment create API.
- [ ] [PAY-EP1-US1-BE3](tasks/PAY-EP1-US1-BE3.md): Add tests for partial payments, invalid amounts, and role restrictions.
- [ ] [PAY-EP1-US2-FE1](tasks/PAY-EP1-US2-FE1.md): Build pending deposit confirmation queue.
- [ ] [PAY-EP1-US2-FE2](tasks/PAY-EP1-US2-FE2.md): Add confirm action with verification reference and confirmation summary.
- [ ] [PAY-EP1-US2-FE3](tasks/PAY-EP1-US2-FE3.md): Add tests for confirm flow and non-accounts blocked UI states.
- [ ] [PAY-EP1-US2-BE1](tasks/PAY-EP1-US2-BE1.md): Implement payment confirmation API with immutable confirmation metadata.
- [ ] [PAY-EP1-US2-BE2](tasks/PAY-EP1-US2-BE2.md): Add audit log and notification events for confirmed payments.
- [ ] [PAY-EP1-US2-BE3](tasks/PAY-EP1-US2-BE3.md): Add tests for accounts-only confirmation and pending-payment due exclusion.
- [ ] [PAY-EP2-US1-FE1](tasks/PAY-EP2-US1-FE1.md): Build stage-wise payment and due summary component.
- [ ] [PAY-EP2-US1-FE2](tasks/PAY-EP2-US1-FE2.md): Show confirmed, pending, total fee, and due amounts separately.
- [ ] [PAY-EP2-US1-FE3](tasks/PAY-EP2-US1-FE3.md): Add tests for partial, cleared, and pending payment display.
- [ ] [PAY-EP2-US1-BE1](tasks/PAY-EP2-US1-BE1.md): Implement due calculation service using file fee snapshots and confirmed payments.
- [ ] [PAY-EP2-US1-BE2](tasks/PAY-EP2-US1-BE2.md): Add payment summary API scoped by role.
- [ ] [PAY-EP2-US1-BE3](tasks/PAY-EP2-US1-BE3.md): Add tests for due formula, multi-payment totals, and pending exclusion.
- [ ] [PAY-EP2-US2-FE1](tasks/PAY-EP2-US2-FE1.md): Add blocked-stage indicators and next payment requirement messages.
- [ ] [PAY-EP2-US2-FE2](tasks/PAY-EP2-US2-FE2.md): Disable stage actions when backend clearance says the gate is blocked.
- [ ] [PAY-EP2-US2-FE3](tasks/PAY-EP2-US2-FE3.md): Add tests for blocked and cleared stage action states.
- [ ] [PAY-EP2-US2-BE1](tasks/PAY-EP2-US2-BE1.md): Expose financial clearance service for Files, Admission, and Visa modules.
- [ ] [PAY-EP2-US2-BE2](tasks/PAY-EP2-US2-BE2.md): Enforce clearance checks before stage transition or approval mutations.
- [ ] [PAY-EP2-US2-BE3](tasks/PAY-EP2-US2-BE3.md): Add integration tests for each stage gate.

## Folder Completion Rules

- [ ] Every EPIC file is complete.
- [ ] Every story file is accepted.
- [ ] Every task implementation plan is completed or explicitly deferred with an approved blocker.
- [ ] Module row is updated in [Progress Tracker](../../progress_tracker.md).
- [ ] Completion log records meaningful milestone completion.
