# Counselling and Program Selection Flow

## Purpose

Help a prospective student choose a suitable university program and understand the full stage-wise cost before opening a file.

## Primary Actors

- Student
- Consultant
- Owner, oversight only

## Trigger

A student walks into the agency or contacts the agency seeking abroad admission guidance.

## Preconditions

- Active catalog exists.
- Selected programs have active packages.
- Consultant has access to browse the catalog.

## Main Flow

1. Student shares academic background, preferences, target country, budget, and intake interest.
2. Consultant searches and filters programs by:
   - Country
   - University
   - Program level
   - Field of study
   - Intake month
   - Entry requirement suitability
3. Consultant reviews program options with the student.
4. Consultant opens the package summary for shortlisted programs.
5. System displays:
   - Program details
   - University details
   - Duration and intake
   - Stage-wise fee breakdown
   - Total package cost
6. Consultant explains the cost and process stages to the student.
7. Student selects a program.
8. If the student decides to proceed, the consultant starts the File Opening Flow.

## Alternate Paths

- Student is undecided: Consultant may continue counselling without creating a file, subject to open business question OQ-01.
- Program has no active package: Consultant cannot create a file and must request Owner configuration.
- Student does not meet entry requirements: Consultant suggests another program or university.

## Business Rules

- Consultants can browse but cannot edit catalog data.
- File creation requires a selected program with an active package.
- Package fees shown during counselling should match the package snapshot applied during file creation.

## Outputs

- Selected country, university, and program
- Student-facing package summary
- Decision to proceed or pause

## Related Data

- Student profile information
- Country
- University
- Program
- Package
- Package Fee Line Item

## Source Sections

- Section 5.4: Program Management
- Section 5.5: Program Package
- Section 5.6: Package Use in Counselling and Marketing
- Section 6.1: File Opening Process
