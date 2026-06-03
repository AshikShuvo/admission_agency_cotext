# File Opening Flow

## Purpose

Register the student, create the central student file, apply the selected package fees, and start the agency workflow.

## Primary Actors

- Student
- Consultant
- Accounts Department
- Owner, oversight only

## Trigger

The student chooses a program and decides to proceed with the agency.

## Preconditions

- Student has selected a program and university.
- The selected program has one active package.
- Consultant is authorized to create files.

## Main Flow

1. Consultant records student personal and academic details.
2. Consultant selects the chosen country, university, and program.
3. System validates that the program has an active package.
4. Consultant creates the file.
5. System generates a unique human-readable file number.
6. System links the file to:
   - Student
   - Consultant
   - University
   - Program
7. System snapshot-copies the active package fee line items onto the file.
8. System sets the file status to `File Opened` or `Pending Payment - File Opening`.
9. Consultant gives the student the fee quotation or package summary.
10. Student makes full or partial payment for the file-opening stage.
11. Payment is sent to Accounts for confirmation.
12. Once Accounts confirms the required file-opening payment, the file becomes eligible for Admission Processing.

## Payment Gate

The file cannot move to the Admission stage until the file-opening payment requirement is confirmed by Accounts.

## Checklist

- Student registered
- Program and university selected
- File created and assigned to consultant
- File number generated
- Package fees copied to file
- Fee quotation generated
- File-opening payment recorded
- Deposit confirmed by Accounts

## Business Rules

- Consultants can create files only for students assigned to them.
- Each file number must be unique.
- Package fees are snapshot-copied at creation time.
- Partial payments are allowed, but dues must be tracked.
- Accounts must confirm deposits.

## Outputs

- Student record
- File record
- File fee records
- Initial payment record
- File opening payment confirmation status

## Related Data

- Student
- File
- Package Snapshot / Fee Structure
- Payment
- File Activity Log

## Source Sections

- Section 6.1: File Opening Process
- Section 7: Financial Domain
- Section 8: File Lifecycle and Status Model
- Section 11: Business Rules
