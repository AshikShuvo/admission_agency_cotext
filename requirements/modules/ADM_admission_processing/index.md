# Admission Processing
## Independent Requirement Module Folder

Module ID: `ADM`

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Module Goal

Manage admission document requests, document verification, university application submission, offer letter upload, and admission approval while enforcing document completeness and admission-stage payment clearance.

## Primary Actors

- Admission Department
- Consultant
- Student
- Accounts
- University
- Owner, oversight

## Source Documents

- [Admission Processing Flow](../../../business/flows/05_admission_processing_flow.md)
- [Module Boundaries](../../../architecture/module_boundaries.md)
- [Admission Workbench Design](../../../design-guide/10-admission-workbench.html)

## Architecture Routing

| Area | Owner |
|---|---|
| Frontend workspace | Admission Workspace |
| Backend module boundary | Admission, Documents |
| Design reference | ../../../design-guide/10-admission-workbench.html |

## Business Rules

- Admission approval requires documents and payment clearance.
- Admission users cannot see commission data.
- All document status changes are logged.

## Dependencies

- Depends on FIL file status and PAY clearance.

## EPIC Files

- [ ] [ADM-EP1: Admission Document Checklist](epics/ADM-EP1_admission_document_checklist.md)
- [ ] [ADM-EP2: University Application and Admission Approval](epics/ADM-EP2_university_application_and_admission_approval.md)

## User Story Files

- [ ] [ADM-EP1-US1: Generate Admission Checklist](stories/ADM-EP1-US1_generate_admission_checklist.md)
- [ ] [ADM-EP1-US2: Submit and Verify Admission Documents](stories/ADM-EP1-US2_submit_and_verify_admission_documents.md)
- [ ] [ADM-EP2-US1: Submit University Application](stories/ADM-EP2-US1_submit_university_application.md)
- [ ] [ADM-EP2-US2: Upload Offer Letter and Approve Admission](stories/ADM-EP2-US2_upload_offer_letter_and_approve_admission.md)

## Task Implementation Plans

- [ ] [ADM-EP1-US1-FE1](tasks/ADM-EP1-US1-FE1.md): Build admission checklist view with required and optional items.
- [ ] [ADM-EP1-US1-FE2](tasks/ADM-EP1-US1-FE2.md): Add document request action with consultant notification preview.
- [ ] [ADM-EP1-US1-FE3](tasks/ADM-EP1-US1-FE3.md): Add tests for checklist creation and consultant request visibility.
- [ ] [ADM-EP1-US1-BE1](tasks/ADM-EP1-US1-BE1.md): Create admission checklist and checklist item models linked to file.
- [ ] [ADM-EP1-US1-BE2](tasks/ADM-EP1-US1-BE2.md): Implement checklist generation and document request APIs.
- [ ] [ADM-EP1-US1-BE3](tasks/ADM-EP1-US1-BE3.md): Add tests for checklist persistence, role access, and notification event creation.
- [ ] [ADM-EP1-US2-FE1](tasks/ADM-EP1-US2-FE1.md): Build document upload and checklist item attachment UI.
- [ ] [ADM-EP1-US2-FE2](tasks/ADM-EP1-US2-FE2.md): Add accept, reject, and correction note controls for Admission users.
- [ ] [ADM-EP1-US2-FE3](tasks/ADM-EP1-US2-FE3.md): Add tests for upload, rejection, correction request, and accepted states.
- [ ] [ADM-EP1-US2-BE1](tasks/ADM-EP1-US2-BE1.md): Implement document metadata, upload reference, and checklist item attachment APIs.
- [ ] [ADM-EP1-US2-BE2](tasks/ADM-EP1-US2-BE2.md): Add document verification service with audit log entries.
- [ ] [ADM-EP1-US2-BE3](tasks/ADM-EP1-US2-BE3.md): Add tests for document status transitions and role-specific access.
- [ ] [ADM-EP2-US1-FE1](tasks/ADM-EP2-US1-FE1.md): Build university application submission panel in the admission workspace.
- [ ] [ADM-EP2-US1-FE2](tasks/ADM-EP2-US1-FE2.md): Show document and payment blockers before allowing submission.
- [ ] [ADM-EP2-US1-FE3](tasks/ADM-EP2-US1-FE3.md): Add tests for blocked and successful submission states.
- [ ] [ADM-EP2-US1-BE1](tasks/ADM-EP2-US1-BE1.md): Add admission application record with submission date and expected response fields.
- [ ] [ADM-EP2-US1-BE2](tasks/ADM-EP2-US1-BE2.md): Enforce document completeness and payment clearance before submission.
- [ ] [ADM-EP2-US1-BE3](tasks/ADM-EP2-US1-BE3.md): Add integration tests for admission submission gates.
- [ ] [ADM-EP2-US2-FE1](tasks/ADM-EP2-US2-FE1.md): Build offer letter upload and admission approval controls.
- [ ] [ADM-EP2-US2-FE2](tasks/ADM-EP2-US2-FE2.md): Show approval confirmation with next-stage visa handoff.
- [ ] [ADM-EP2-US2-FE3](tasks/ADM-EP2-US2-FE3.md): Add tests for offer upload, approval blocking, and visa handoff state.
- [ ] [ADM-EP2-US2-BE1](tasks/ADM-EP2-US2-BE1.md): Implement offer letter attachment and admission approval APIs.
- [ ] [ADM-EP2-US2-BE2](tasks/ADM-EP2-US2-BE2.md): Add file status transition from admission approved to visa processing with audit log and notification.
- [ ] [ADM-EP2-US2-BE3](tasks/ADM-EP2-US2-BE3.md): Add integration tests for approval requirements and status transition.

## Folder Completion Rules

- [ ] Every EPIC file is complete.
- [ ] Every story file is accepted.
- [ ] Every task implementation plan is completed or explicitly deferred with an approved blocker.
- [ ] Module row is updated in [Progress Tracker](../../progress_tracker.md).
- [ ] Completion log records meaningful milestone completion.
