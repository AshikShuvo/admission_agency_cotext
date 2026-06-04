# File Opening and Student Case
## Independent Requirement Module Folder

Module ID: `FIL`

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Module Goal

Create the central student file, copy the selected package fees into immutable file fee records, assign the consultant, and prepare the file for payment confirmation and admission processing.

## Primary Actors

- Consultant
- Student
- Accounts
- Owner, oversight

## Source Documents

- [File Opening Flow](../../../business/flows/03_file_opening_flow.md)
- [Module Boundaries](../../../architecture/module_boundaries.md)
- [File Opening Design](../../../design-guide/07-file-opening.html)
- [Student File Detail Design](../../../design-guide/08-student-file-detail.html)

## Architecture Routing

| Area | Owner |
|---|---|
| Frontend workspace | Consultant File Workspace |
| Backend module boundary | Students, Files / Cases, File Fees |
| Design reference | ../../../design-guide/07-file-opening.html and ../../../design-guide/08-student-file-detail.html |

## Business Rules

- Consultants only manage assigned files.
- File numbers are unique.
- Package fees are copied at creation time.
- File history is preserved.

## Dependencies

- Depends on CAT active package and CNS selected program context.

## EPIC Files

- [ ] [FIL-EP1: Student Profile and File Creation](epics/FIL-EP1_student_profile_and_file_creation.md)
- [ ] [FIL-EP2: Package Snapshot and File Detail](epics/FIL-EP2_package_snapshot_and_file_detail.md)

## User Story Files

- [ ] [FIL-EP1-US1: Register Student Profile](stories/FIL-EP1-US1_register_student_profile.md)
- [ ] [FIL-EP1-US2: Create Student File](stories/FIL-EP1-US2_create_student_file.md)
- [ ] [FIL-EP2-US1: Snapshot Package Fees](stories/FIL-EP2-US1_snapshot_package_fees.md)
- [ ] [FIL-EP2-US2: View Student File Detail](stories/FIL-EP2-US2_view_student_file_detail.md)

## Task Implementation Plans

- [ ] [FIL-EP1-US1-FE1](tasks/FIL-EP1-US1-FE1.md): Build student profile form with personal, guardian, academic, and passport sections.
- [ ] [FIL-EP1-US1-FE2](tasks/FIL-EP1-US1-FE2.md): Add validation, draft saving, and missing-optional-field indicators.
- [ ] [FIL-EP1-US1-FE3](tasks/FIL-EP1-US1-FE3.md): Add tests for required fields and consultant-scoped student creation.
- [ ] [FIL-EP1-US1-BE1](tasks/FIL-EP1-US1-BE1.md): Create student entity and DTOs for profile, guardian, academic, and passport metadata.
- [ ] [FIL-EP1-US1-BE2](tasks/FIL-EP1-US1-BE2.md): Implement student create/update APIs with consultant scope enforcement.
- [ ] [FIL-EP1-US1-BE3](tasks/FIL-EP1-US1-BE3.md): Add tests for validation, ownership scope, and profile persistence.
- [ ] [FIL-EP1-US2-FE1](tasks/FIL-EP1-US2-FE1.md): Build file creation confirmation screen using selected program context.
- [ ] [FIL-EP1-US2-FE2](tasks/FIL-EP1-US2-FE2.md): Show generated file number and initial lifecycle status after creation.
- [ ] [FIL-EP1-US2-FE3](tasks/FIL-EP1-US2-FE3.md): Add tests for file creation confirmation and navigation to file detail.
- [ ] [FIL-EP1-US2-BE1](tasks/FIL-EP1-US2-BE1.md): Create file/case entity with status, assignment, program links, and file number.
- [ ] [FIL-EP1-US2-BE2](tasks/FIL-EP1-US2-BE2.md): Implement transaction-safe file creation API.
- [ ] [FIL-EP1-US2-BE3](tasks/FIL-EP1-US2-BE3.md): Add tests for unique file number generation and required relationships.
- [ ] [FIL-EP2-US1-FE1](tasks/FIL-EP2-US1-FE1.md): Show package snapshot preview before final file creation.
- [ ] [FIL-EP2-US1-FE2](tasks/FIL-EP2-US1-FE2.md): Show file-specific stage fee totals in file detail.
- [ ] [FIL-EP2-US1-FE3](tasks/FIL-EP2-US1-FE3.md): Add tests for package preview and snapshot display.
- [ ] [FIL-EP2-US1-BE1](tasks/FIL-EP2-US1-BE1.md): Create file fee snapshot records during file creation transaction.
- [ ] [FIL-EP2-US1-BE2](tasks/FIL-EP2-US1-BE2.md): Add file fee summary API with stage totals and due inputs.
- [ ] [FIL-EP2-US1-BE3](tasks/FIL-EP2-US1-BE3.md): Add tests proving catalog package changes do not mutate file fees.
- [ ] [FIL-EP2-US2-FE1](tasks/FIL-EP2-US2-FE1.md): Build role-aware file detail layout with status, tabs, and next action summary.
- [ ] [FIL-EP2-US2-FE2](tasks/FIL-EP2-US2-FE2.md): Add empty, locked, loading, and restricted-section states.
- [ ] [FIL-EP2-US2-FE3](tasks/FIL-EP2-US2-FE3.md): Add tests for role-specific file detail visibility.
- [ ] [FIL-EP2-US2-BE1](tasks/FIL-EP2-US2-BE1.md): Implement file detail API with role-based data shape.
- [ ] [FIL-EP2-US2-BE2](tasks/FIL-EP2-US2-BE2.md): Add query-layer scope filters for Owner, Consultant, Accounts, Admission, and Visa.
- [ ] [FIL-EP2-US2-BE3](tasks/FIL-EP2-US2-BE3.md): Add tests for assigned-file restriction and sensitive field hiding.

## Folder Completion Rules

- [ ] Every EPIC file is complete.
- [ ] Every story file is accepted.
- [ ] Every task implementation plan is completed or explicitly deferred with an approved blocker.
- [ ] Module row is updated in [Progress Tracker](../../progress_tracker.md).
- [ ] Completion log records meaningful milestone completion.
