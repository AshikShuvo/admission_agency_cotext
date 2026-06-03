# Payment and Deposit Confirmation Flow

## Purpose

Record student payments, verify deposits, calculate dues, and enforce payment gates before each processing stage can advance.

## Primary Actors

- Student
- Accounts Department
- Consultant, status visibility for own files
- Admission Department, stage clearance visibility
- Visa Department, stage clearance visibility
- Owner

## Trigger

A student pays any amount for file opening, admission, visa, or another tracked charge.

## Preconditions

- A student file exists.
- The file has configured fee records for the relevant stage.
- Payment method and amount are known.

## Main Flow

1. Student pays by cash, bank transfer, bKash, Nagad, or another accepted method.
2. Accounts records the payment with:
   - File number
   - Stage
   - Amount
   - Payment date
   - Payment method
   - Reference or receipt number
3. System stores the payment as pending confirmation if verification is not complete.
4. Accounts verifies the deposit against bank, cash, or mobile banking records.
5. Accounts confirms the payment in the system.
6. System updates confirmed payment totals for that stage.
7. System calculates due amount:

```text
Due Amount = Total Stage Fee - Sum of Confirmed Payments for Stage
```

8. If due amount is zero, the stage is financially cleared.
9. System notifies the relevant role that the file can proceed.

## Stage Gates

| Stage | Gate |
|---|---|
| File Opening | Must be financially cleared before Admission starts |
| Admission | Must be financially cleared before university application or admission approval |
| Visa | Must be financially cleared before visa application or visa approval |

## Alternate Paths

- Partial payment: System records payment and keeps due amount visible.
- Payment not verified: Payment remains unconfirmed and does not reduce due.
- Owner override: Possible only if approved as a future business rule decision.

## Business Rules

- Only Accounts can confirm deposits.
- Consultants cannot self-confirm student payments.
- Partial payments are accepted at every stage.
- Due calculation is automatic.
- A stage cannot be approved while required dues remain unpaid unless owner override is allowed.

## Outputs

- Payment record
- Confirmation record
- Updated due amount
- Financial clearance status
- Activity log entry

## Related Data

- Payment
- Fee Structure
- File
- User
- File Activity Log

## Source Sections

- Section 7: Financial Domain
- Section 8: File Lifecycle and Status Model
- Section 11: Business Rules BR-001 to BR-003 and BR-011
