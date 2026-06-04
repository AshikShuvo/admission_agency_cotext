# Counselling and Program Selection
## Independent Requirement Module Folder

Module ID: `CNS`

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Module Goal

Help consultants search programs, compare package costs, check student fit, and start file opening only when a selected program has an active package.

## Primary Actors

- Consultant
- Student
- Owner, oversight

## Source Documents

- [Counselling and Program Selection Flow](../../../business/flows/02_counselling_and_program_selection_flow.md)
- [Module Boundaries](../../../architecture/module_boundaries.md)
- [Counselling Program Selection Design](../../../design-guide/06-counselling-program-selection.html)

## Architecture Routing

| Area | Owner |
|---|---|
| Frontend workspace | Consultant File Workspace |
| Backend module boundary | Catalog, Students, Files / Cases |
| Design reference | ../../../design-guide/06-counselling-program-selection.html |

## Business Rules

- Consultants cannot edit catalog records.
- File opening requires active package.
- Counselling can exist before formal file creation.

## Dependencies

- Depends on CAT active catalog and active package lookup.

## EPIC Files

- [ ] [CNS-EP1: Program Discovery for Counselling](epics/CNS-EP1_program_discovery_for_counselling.md)
- [ ] [CNS-EP2: Student Fit and Proceed Decision](epics/CNS-EP2_student_fit_and_proceed_decision.md)

## User Story Files

- [ ] [CNS-EP1-US1: Search Active Programs](stories/CNS-EP1-US1_search_active_programs.md)
- [ ] [CNS-EP1-US2: View Program and Package Details](stories/CNS-EP1-US2_view_program_and_package_details.md)
- [ ] [CNS-EP2-US1: Capture Counselling Inputs](stories/CNS-EP2-US1_capture_counselling_inputs.md)
- [ ] [CNS-EP2-US2: Start File Opening from Selected Program](stories/CNS-EP2-US2_start_file_opening_from_selected_program.md)

## Task Implementation Plans

- [ ] [CNS-EP1-US1-FE1](tasks/CNS-EP1-US1-FE1.md): Build searchable program browser with filters and result list.
- [ ] [CNS-EP1-US1-FE2](tasks/CNS-EP1-US1-FE2.md): Add empty, loading, no-package, and read-only states.
- [ ] [CNS-EP1-US1-FE3](tasks/CNS-EP1-US1-FE3.md): Add frontend tests for filtering and read-only catalog behavior.
- [ ] [CNS-EP1-US1-BE1](tasks/CNS-EP1-US1-BE1.md): Add program search API with filters and active-package indicator.
- [ ] [CNS-EP1-US1-BE2](tasks/CNS-EP1-US1-BE2.md): Enforce consultant read-only access and active catalog visibility rules.
- [ ] [CNS-EP1-US1-BE3](tasks/CNS-EP1-US1-BE3.md): Add tests for search filters, role access, and no-package indicators.
- [ ] [CNS-EP1-US2-FE1](tasks/CNS-EP1-US2-FE1.md): Build program detail panel with package cost summary.
- [ ] [CNS-EP1-US2-FE2](tasks/CNS-EP1-US2-FE2.md): Add stage-wise fee display for File Opening, Admission, and Visa.
- [ ] [CNS-EP1-US2-FE3](tasks/CNS-EP1-US2-FE3.md): Add tests that consultant package details exclude commission fields.
- [ ] [CNS-EP1-US2-BE1](tasks/CNS-EP1-US2-BE1.md): Add program detail API with active package summary for counselling.
- [ ] [CNS-EP1-US2-BE2](tasks/CNS-EP1-US2-BE2.md): Remove owner-only commission data from consultant responses.
- [ ] [CNS-EP1-US2-BE3](tasks/CNS-EP1-US2-BE3.md): Add tests for package summary calculation and commission hiding.
- [ ] [CNS-EP2-US1-FE1](tasks/CNS-EP2-US1-FE1.md): Build counselling input form beside program search results.
- [ ] [CNS-EP2-US1-FE2](tasks/CNS-EP2-US1-FE2.md): Add validation and save-draft behavior for undecided students.
- [ ] [CNS-EP2-US1-FE3](tasks/CNS-EP2-US1-FE3.md): Add tests for saving inputs without creating a file.
- [ ] [CNS-EP2-US1-BE1](tasks/CNS-EP2-US1-BE1.md): Define counselling lead or draft model for pre-file student inputs.
- [ ] [CNS-EP2-US1-BE2](tasks/CNS-EP2-US1-BE2.md): Implement draft create/update APIs scoped to the consultant.
- [ ] [CNS-EP2-US1-BE3](tasks/CNS-EP2-US1-BE3.md): Add tests for consultant ownership and no-file-created behavior.
- [ ] [CNS-EP2-US2-FE1](tasks/CNS-EP2-US2-FE1.md): Add proceed-to-file-opening action from program detail.
- [ ] [CNS-EP2-US2-FE2](tasks/CNS-EP2-US2-FE2.md): Pre-fill file opening context with selected country, university, program, and package.
- [ ] [CNS-EP2-US2-FE3](tasks/CNS-EP2-US2-FE3.md): Add tests for enabled and blocked proceed states.
- [ ] [CNS-EP2-US2-BE1](tasks/CNS-EP2-US2-BE1.md): Add selected-program validation endpoint for file-opening eligibility.
- [ ] [CNS-EP2-US2-BE2](tasks/CNS-EP2-US2-BE2.md): Return active package snapshot preview for the file opening flow.
- [ ] [CNS-EP2-US2-BE3](tasks/CNS-EP2-US2-BE3.md): Add tests for missing active package and inactive program blocking.

## Folder Completion Rules

- [ ] Every EPIC file is complete.
- [ ] Every story file is accepted.
- [ ] Every task implementation plan is completed or explicitly deferred with an approved blocker.
- [ ] Module row is updated in [Progress Tracker](../../progress_tracker.md).
- [ ] Completion log records meaningful milestone completion.
