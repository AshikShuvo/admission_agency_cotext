# ADM-EP2-US1: Submit University Application
## Detailed User Story

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `ADM` - Admission Processing |
| EPIC | [ADM-EP2: University Application and Admission Approval](../epics/ADM-EP2_university_application_and_admission_approval.md) |

## Story Statement

As an Admission user, I want to record university application submission so that the agency can track when the application was sent.

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

- [ ] Application submission requires complete admission documents.
- [ ] Application submission requires admission-stage financial clearance.
- [ ] Submission date and expected response timeline are recorded.

## Business Rules

- Admission approval requires documents and payment clearance.
- Admission users cannot see commission data.
- All document status changes are logged.

## Dependencies and Preconditions

- Depends on FIL file status and PAY clearance.

## Frontend Tasks

- [ ] [ADM-EP2-US1-FE1](../tasks/ADM-EP2-US1-FE1.md): Build university application submission panel in the admission workspace.
- [ ] [ADM-EP2-US1-FE2](../tasks/ADM-EP2-US1-FE2.md): Show document and payment blockers before allowing submission.
- [ ] [ADM-EP2-US1-FE3](../tasks/ADM-EP2-US1-FE3.md): Add tests for blocked and successful submission states.

## Backend Tasks

- [ ] [ADM-EP2-US1-BE1](../tasks/ADM-EP2-US1-BE1.md): Add admission application record with submission date and expected response fields.
- [ ] [ADM-EP2-US1-BE2](../tasks/ADM-EP2-US1-BE2.md): Enforce document completeness and payment clearance before submission.
- [ ] [ADM-EP2-US1-BE3](../tasks/ADM-EP2-US1-BE3.md): Add integration tests for admission submission gates.

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
