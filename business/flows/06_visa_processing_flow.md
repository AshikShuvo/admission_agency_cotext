# Visa Processing Flow

## Purpose

Collect and verify visa documents, confirm visa-stage fees, submit the visa application, record the outcome, and close or complete the file.

## Primary Actors

- Visa Department
- Consultant
- Student
- Accounts Department
- Embassy / Immigration Authority
- Owner

## Trigger

Admission is approved and the student has received a university offer or acceptance letter.

## Preconditions

- Admission stage is approved.
- Offer letter is uploaded to the file.
- File has moved to `Visa In Progress`.

## Main Flow

1. Visa Department reviews the file and offer letter.
2. Visa Department generates the visa document checklist.
3. Visa Department requests required documents from the consultant and student.
4. Visa documents are collected and uploaded.
5. Visa Department verifies document completeness and validity.
6. Student pays visa-stage charges.
7. Accounts records and confirms visa-stage payments.
8. System calculates visa-stage due amount.
9. Once documents are complete and payment is cleared, Visa submits the application to the embassy or immigration authority.
10. System records visa submission date.
11. Visa Department records the visa outcome.
12. If approved, visa issue date and expiry date are recorded.
13. Pre-departure details may be recorded.
14. Visa Department marks the visa stage approved or completed.
15. File status moves to `Completed` after student departure or enrollment confirmation.

## Required Documents

Typical visa documents include:

- Passport
- University acceptance letter
- Financial statements
- Medical certificate
- Police clearance
- Photographs
- Visa application form

## Payment Gate

The visa stage cannot be approved until visa-stage fees are confirmed by Accounts and due amount is cleared.

## Alternate Paths

- Visa approved: File continues to pre-departure and completion.
- Visa rejected: File is marked `Visa Rejected`, rejection reason is recorded, and Owner decides whether to reapply or close.

## Checklist

- Visa document checklist generated
- Visa documents collected
- Visa documents verified
- Visa payment confirmed
- Visa application submitted
- Visa outcome recorded
- File completed or rejected

## Business Rules

- Visa users see only visa-relevant file details.
- Visa users cannot view commission data.
- Payment confirmation must come from Accounts.
- Visa rejection must keep existing records and support possible reapplication.

## Outputs

- Visa document checklist
- Verified visa documents
- Visa-stage payment clearance
- Visa application submission record
- Visa outcome
- Completed or rejected file status

## Related Data

- File
- Document
- Payment
- File Activity Log

## Source Sections

- Section 6.3: Visa Processing
- Section 8: File Lifecycle and Status Model
- Section 10: Access Control and Permissions
- Section 11: Business Rules
