# Admission Processing Flow

## Purpose

Collect and verify admission documents, confirm admission-stage fees, submit the university application, and approve the file for visa processing after offer letter receipt.

## Primary Actors

- Admission Department
- Consultant
- Student
- Accounts Department
- University
- Owner, oversight only

## Trigger

File-opening payment is confirmed and the file is ready for admission processing.

## Preconditions

- File exists and is assigned to a consultant.
- Selected university and program are recorded.
- File-opening stage payment gate is cleared.

## Main Flow

1. Admission Department reviews the file and selected program.
2. Admission Department generates the required admission document checklist.
3. Admission Department sends document request to the assigned consultant.
4. Consultant collects documents from the student.
5. Consultant uploads or submits documents through the system.
6. Admission Department verifies document completeness and validity.
7. If documents are missing or incorrect, Admission sends a correction request to the consultant.
8. Student pays admission-stage charges.
9. Accounts records and confirms admission-stage payments.
10. System calculates admission-stage due amount.
11. Once documents are complete and payment is cleared, Admission submits the application to the university.
12. System records application submission date and expected response timeline.
13. University issues offer letter or acceptance letter.
14. Admission uploads the offer letter to the file.
15. Admission marks the admission stage approved.
16. File moves to Visa Processing.

## Required Documents

Typical admission documents include:

- Academic certificates
- Transcripts
- English language score, if required
- NID or birth certificate
- Photographs
- Passport, if available or required

## Payment Gate

The admission stage cannot be approved until admission-stage fees are confirmed by Accounts and due amount is cleared.

## Checklist

- Document checklist generated
- Documents requested from consultant
- Documents submitted
- Documents verified
- Admission payment confirmed
- University application submitted
- Offer letter received
- Admission approved

## Business Rules

- Admission users see only admission-relevant file details.
- Admission cannot access commission data.
- All document uploads and status changes must be logged.
- Payment confirmation must come from Accounts.

## Outputs

- Admission document checklist
- Verified admission documents
- Admission-stage payment clearance
- University application submission record
- Offer letter
- Admission approval

## Related Data

- File
- Student
- Program
- Document
- Payment
- File Activity Log

## Source Sections

- Section 6.2: Admission Process
- Section 8: File Lifecycle and Status Model
- Section 10: Access Control and Permissions
- Section 11: Business Rules
