# Visa Processing
## Independent Requirement Module Folder

Module ID: `VIS`

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Module Goal

Manage visa document collection, visa application submission, payment clearance, outcome recording, rejection handling, and completion of the student file.

## Primary Actors

- Visa Department
- Consultant
- Student
- Accounts
- Embassy / Immigration Authority
- Owner

## Source Documents

- [Visa Processing Flow](../../../business/flows/06_visa_processing_flow.md)
- [Module Boundaries](../../../architecture/module_boundaries.md)
- [Visa Workbench Design](../../../design-guide/11-visa-workbench.html)

## Architecture Routing

| Area | Owner |
|---|---|
| Frontend workspace | Visa Workspace |
| Backend module boundary | Visa, Documents |
| Design reference | ../../../design-guide/11-visa-workbench.html |

## Business Rules

- Visa approval/completion requires documents and payment clearance.
- Visa rejection preserves history.
- Visa users cannot see commission data.

## Dependencies

- Depends on ADM approval, offer letter, and PAY clearance.

## EPIC Files

- [ ] [VIS-EP1: Visa Documents and Submission](epics/VIS-EP1_visa_documents_and_submission.md)
- [ ] [VIS-EP2: Visa Outcome and File Completion](epics/VIS-EP2_visa_outcome_and_file_completion.md)

## User Story Files

- [ ] [VIS-EP1-US1: Generate Visa Checklist](stories/VIS-EP1-US1_generate_visa_checklist.md)
- [ ] [VIS-EP1-US2: Submit Visa Application](stories/VIS-EP1-US2_submit_visa_application.md)
- [ ] [VIS-EP2-US1: Record Visa Outcome](stories/VIS-EP2-US1_record_visa_outcome.md)
- [ ] [VIS-EP2-US2: Complete Student File](stories/VIS-EP2-US2_complete_student_file.md)

## Task Implementation Plans

- [ ] [VIS-EP1-US1-FE1](tasks/VIS-EP1-US1-FE1.md): Build visa checklist view with required and optional visa document items.
- [ ] [VIS-EP1-US1-FE2](tasks/VIS-EP1-US1-FE2.md): Add missing-document request and consultant follow-up state.
- [ ] [VIS-EP1-US1-FE3](tasks/VIS-EP1-US1-FE3.md): Add tests for checklist generation after admission approval.
- [ ] [VIS-EP1-US1-BE1](tasks/VIS-EP1-US1-BE1.md): Create visa checklist and item models linked to file and visa stage.
- [ ] [VIS-EP1-US1-BE2](tasks/VIS-EP1-US1-BE2.md): Implement visa checklist generation API gated by admission approval.
- [ ] [VIS-EP1-US1-BE3](tasks/VIS-EP1-US1-BE3.md): Add tests for status gating, role access, and task notification events.
- [ ] [VIS-EP1-US2-FE1](tasks/VIS-EP1-US2-FE1.md): Build visa submission panel with submission date and reference fields.
- [ ] [VIS-EP1-US2-FE2](tasks/VIS-EP1-US2-FE2.md): Show document and payment blockers before submission.
- [ ] [VIS-EP1-US2-FE3](tasks/VIS-EP1-US2-FE3.md): Add tests for blocked and successful visa submission states.
- [ ] [VIS-EP1-US2-BE1](tasks/VIS-EP1-US2-BE1.md): Create visa application record with submission date and reference fields.
- [ ] [VIS-EP1-US2-BE2](tasks/VIS-EP1-US2-BE2.md): Enforce document completeness and visa payment clearance before submission.
- [ ] [VIS-EP1-US2-BE3](tasks/VIS-EP1-US2-BE3.md): Add integration tests for visa submission gates.
- [ ] [VIS-EP2-US1-FE1](tasks/VIS-EP2-US1-FE1.md): Build visa outcome form with approved and rejected branches.
- [ ] [VIS-EP2-US1-FE2](tasks/VIS-EP2-US1-FE2.md): Show rejection reason and reapplication decision placeholder for Owner review.
- [ ] [VIS-EP2-US1-FE3](tasks/VIS-EP2-US1-FE3.md): Add tests for approved and rejected outcome states.
- [ ] [VIS-EP2-US1-BE1](tasks/VIS-EP2-US1-BE1.md): Implement visa outcome API with approved/rejected fields and validation.
- [ ] [VIS-EP2-US1-BE2](tasks/VIS-EP2-US1-BE2.md): Add status transition to `Visa Approved` or `Visa Rejected` with audit log and notification.
- [ ] [VIS-EP2-US1-BE3](tasks/VIS-EP2-US1-BE3.md): Add tests for outcome validation, rejection history, and notification creation.
- [ ] [VIS-EP2-US2-FE1](tasks/VIS-EP2-US2-FE1.md): Build completion action with departure/enrollment confirmation fields.
- [ ] [VIS-EP2-US2-FE2](tasks/VIS-EP2-US2-FE2.md): Show completed locked-file state across file detail screens.
- [ ] [VIS-EP2-US2-FE3](tasks/VIS-EP2-US2-FE3.md): Add tests for completion action and locked state.
- [ ] [VIS-EP2-US2-BE1](tasks/VIS-EP2-US2-BE1.md): Implement file completion API with completion details and allowed roles.
- [ ] [VIS-EP2-US2-BE2](tasks/VIS-EP2-US2-BE2.md): Enforce immutable completed-file behavior except Owner-authorized changes.
- [ ] [VIS-EP2-US2-BE3](tasks/VIS-EP2-US2-BE3.md): Add integration tests for completion, locking, and owner exception behavior.

## Folder Completion Rules

- [ ] Every EPIC file is complete.
- [ ] Every story file is accepted.
- [ ] Every task implementation plan is completed or explicitly deferred with an approved blocker.
- [ ] Module row is updated in [Progress Tracker](../../progress_tracker.md).
- [ ] Completion log records meaningful milestone completion.
