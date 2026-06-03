# Catalog and Package Setup Flow

## Purpose

Prepare the master catalog that consultants use during counselling and file creation. A student file cannot be created for a program unless that program has one active package.

## Primary Actors

- Owner / Admin
- Consultant, read-only browser
- Accounts, limited package view when linked to a file

## Trigger

The agency starts operating in a new country, partners with a university, adds a program, or updates program fees.

## Preconditions

- Owner has system access.
- The country, university, program, and package details are known.
- Fee amounts are confirmed by agency management.

## Main Flow

1. Owner creates or activates a destination country.
2. Owner creates or updates partner university details under that country.
3. Owner creates or updates programs under the university.
4. Owner creates a program package for each active program.
5. Owner adds package fee line items by stage:
   - File Opening
   - Admission
   - Visa
6. System calculates stage totals and total package cost.
7. Owner marks the package active.
8. System ensures only one active package exists for the program.
9. Consultant can browse the active catalog during counselling.

## Business Rules

- Only the Owner can manage countries, universities, programs, and packages.
- Consultants can browse the catalog but cannot edit it.
- Only one package can be active per program at a time.
- A program must have an active package before a student file can be created.
- When a file is created, the active package is copied as a snapshot onto the file.
- Future package changes must not alter existing file fee records.
- University commission defaults are visible only to the Owner.

## Outputs

- Active country records
- Active university records
- Active program records
- Active program package with stage-wise fee line items
- Consultant-browsable catalog

## Related Data

- Country
- University
- Program
- Package
- Package Fee Line Item

## Source Sections

- Section 5: Country, University and Program Catalog
- Section 9: Data Entities and Relationships
- Section 11: Business Rules BR-012 to BR-015
