# Exception and File Closure Flow

## Purpose

Handle files that cannot follow the happy path because they are paused, cancelled, completed, or affected by visa rejection.

## Primary Actors

- Owner
- Consultant
- Admission Department
- Visa Department
- Accounts Department, financial context only

## Trigger

A file reaches an exceptional status or final status:

- `On Hold`
- `Cancelled`
- `Visa Rejected`
- `Completed`

## Preconditions

- File exists.
- Reason for the exception or closure is known.
- User has authority to update the status.

## On Hold Flow

1. Authorized user identifies that the file should pause.
2. User records the hold reason.
3. System sets status to `On Hold`.
4. System keeps existing payments, documents, and activity history unchanged.
5. File can resume when the reason is resolved.

## Cancellation Flow

1. Student withdraws or agency decides to stop processing.
2. Authorized user records cancellation reason.
3. System sets status to `Cancelled`.
4. System prevents normal edits unless Owner authorizes reopening or correction.
5. Financial records and audit trail remain preserved.

## Visa Rejection Flow

1. Visa Department records rejection outcome.
2. System sets status to `Visa Rejected`.
3. Rejection reason is recorded.
4. Owner reviews whether to reapply or close.
5. If reapplication is approved, the visa stage restarts without losing old records.
6. If no reapplication is approved, file remains rejected or is closed according to final business decision.

## Completion Flow

1. Visa is approved and student departs or enrollment is confirmed.
2. Visa Department or Owner records completion details.
3. System sets status to `Completed`.
4. File becomes immutable unless Owner explicitly authorizes changes.
5. File becomes eligible for commission tracking if commission is expected.

## Business Rules

- File deletion is not permitted; cancellation is used instead.
- Completed and cancelled files cannot be edited without Owner authorization.
- Visa rejection must preserve records.
- Reapplication restarts the visa stage without deleting previous visa history.
- All status changes must be logged.

## Outputs

- Exception status
- Reason note
- Preserved file history
- Optional reapplication decision
- Final completed or cancelled record

## Related Data

- File
- Document
- Payment
- File Activity Log
- Commission, after completion

## Source Sections

- Section 8: File Lifecycle and Status Model
- Section 11: Business Rules BR-009 and BR-010
- Section 14: Assumptions and Open Questions
