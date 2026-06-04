# ADM-EP1-US1: Generate Admission Checklist
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

As an Admission user, I want to generate the required admission checklist so that consultants know exactly what documents to collect.

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

- [ ] Checklist is linked to the student file and admission stage.
- [ ] Checklist items can be marked required, optional, pending, submitted, accepted, or rejected.
- [ ] Consultant receives a task or notification when documents are requested.

## Business Rules

- Admission approval requires documents and payment clearance.
- Admission users cannot see commission data.
- All document status changes are logged.

## Dependencies and Preconditions

- Depends on FIL file status and PAY clearance.

## Frontend Tasks

- [ ] [ADM-EP1-US1-FE1](../tasks/ADM-EP1-US1-FE1.md): Build admission checklist view with required and optional items.
- [ ] [ADM-EP1-US1-FE2](../tasks/ADM-EP1-US1-FE2.md): Add document request action with consultant notification preview.
- [ ] [ADM-EP1-US1-FE3](../tasks/ADM-EP1-US1-FE3.md): Add tests for checklist creation and consultant request visibility.

## Backend Tasks

- [ ] [ADM-EP1-US1-BE1](../tasks/ADM-EP1-US1-BE1.md): Create admission checklist and checklist item models linked to file.
- [ ] [ADM-EP1-US1-BE2](../tasks/ADM-EP1-US1-BE2.md): Implement checklist generation and document request APIs.
- [ ] [ADM-EP1-US1-BE3](../tasks/ADM-EP1-US1-BE3.md): Add tests for checklist persistence, role access, and notification event creation.

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
