# ADM-EP1-US2: Submit and Verify Admission Documents
## Detailed User Story

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `ADM` - Admission Processing |
| EPIC | [ADM-EP1: Admission Document Checklist](../epics/ADM-EP1_admission_document_checklist.md) |

## Story Statement

As Admission staff, I want to verify submitted documents so that incomplete or invalid files do not move forward.

## Business Expectation

This story must convert the business expectation into a working system behavior that staff can use without relying on manual spreadsheets, side notes, or hidden process knowledge. The implementation must preserve the role boundaries, lifecycle rules, and data ownership described in the source business flow.

## Primary Actors

- Admission Department
- Consultant
- Student
- Accounts
- University
- Owner, oversight

## Source Documents

- [Admission Processing Flow](../../../../business/flows/05_admission_processing_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [Admission Workbench Design](../../../../design-guide/10-admission-workbench.html)

## Acceptance Criteria

- [ ] Consultant can upload or attach documents for requested checklist items.
- [ ] Admission can accept, reject, or request correction with notes.
- [ ] Accepted document state is visible in file detail according to role scope.

## Business Rules

- Admission approval requires documents and payment clearance.
- Admission users cannot see commission data.
- All document status changes are logged.

## Dependencies and Preconditions

- Depends on FIL file status and PAY clearance.

## Frontend Tasks

- [ ] [ADM-EP1-US2-FE1](../tasks/ADM-EP1-US2-FE1.md): Build document upload and checklist item attachment UI.
- [ ] [ADM-EP1-US2-FE2](../tasks/ADM-EP1-US2-FE2.md): Add accept, reject, and correction note controls for Admission users.
- [ ] [ADM-EP1-US2-FE3](../tasks/ADM-EP1-US2-FE3.md): Add tests for upload, rejection, correction request, and accepted states.

## Backend Tasks

- [ ] [ADM-EP1-US2-BE1](../tasks/ADM-EP1-US2-BE1.md): Implement document metadata, upload reference, and checklist item attachment APIs.
- [ ] [ADM-EP1-US2-BE2](../tasks/ADM-EP1-US2-BE2.md): Add document verification service with audit log entries.
- [ ] [ADM-EP1-US2-BE3](../tasks/ADM-EP1-US2-BE3.md): Add tests for document status transitions and role-specific access.

## Cross-Agent Contract

- Backend owns persistence, authorization, workflow gates, audit events, and role-scoped API responses.
- Frontend owns the staff-facing workflow, visible states, validation feedback, and clear blocked-state messaging.
- QA/review owns acceptance verification across frontend, backend, and access-control behavior.
- If the frontend and backend agents disagree on API shape, pause the story and add a blocker to [Progress Tracker](../../../progress_tracker.md).

## Detailed Acceptance Review Checklist

- [ ] User can complete the happy path described by the story statement.
- [ ] User sees clear feedback when required data is missing or a workflow gate blocks progress.
- [ ] Unauthorized roles cannot perform the action through UI or API.
- [ ] Restricted data is not returned from the backend and is not rendered by the frontend.
- [ ] Important state changes create audit log or notification events where required by the business rules.
- [ ] Automated tests cover the success path and at least one failure or restricted path.

## Completion Rules

- [ ] All linked frontend tasks are complete.
- [ ] All linked backend tasks are complete.
- [ ] Acceptance criteria are verified by QA/review.
- [ ] Story count is updated in [Progress Tracker](../../../progress_tracker.md).
- [ ] EPIC progress is recalculated after this story is accepted.
