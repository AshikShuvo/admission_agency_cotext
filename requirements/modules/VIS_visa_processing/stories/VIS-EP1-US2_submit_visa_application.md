# VIS-EP1-US2: Submit Visa Application
## Detailed User Story

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `VIS` - Visa Processing |
| EPIC | [VIS-EP1: Visa Documents and Submission](../epics/VIS-EP1_visa_documents_and_submission.md) |

## Story Statement

As a Visa user, I want to record visa application submission so that the agency can track embassy processing.

## Business Expectation

This story must convert the business expectation into a working system behavior that staff can use without relying on manual spreadsheets, side notes, or hidden process knowledge. The implementation must preserve the role boundaries, lifecycle rules, and data ownership described in the source business flow.

## Primary Actors

- Visa Department
- Consultant
- Student
- Accounts
- Embassy / Immigration Authority
- Owner

## Source Documents

- [Visa Processing Flow](../../../../business/flows/06_visa_processing_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [Visa Workbench Design](../../../../design-guide/11-visa-workbench.html)

## Acceptance Criteria

- [ ] Visa submission requires complete visa documents.
- [ ] Visa submission requires visa-stage financial clearance.
- [ ] Submission date and application reference can be recorded.

## Business Rules

- Visa approval/completion requires documents and payment clearance.
- Visa rejection preserves history.
- Visa users cannot see commission data.

## Dependencies and Preconditions

- Depends on ADM approval, offer letter, and PAY clearance.

## Frontend Tasks

- [ ] [VIS-EP1-US2-FE1](../tasks/VIS-EP1-US2-FE1.md): Build visa submission panel with submission date and reference fields.
- [ ] [VIS-EP1-US2-FE2](../tasks/VIS-EP1-US2-FE2.md): Show document and payment blockers before submission.
- [ ] [VIS-EP1-US2-FE3](../tasks/VIS-EP1-US2-FE3.md): Add tests for blocked and successful visa submission states.

## Backend Tasks

- [ ] [VIS-EP1-US2-BE1](../tasks/VIS-EP1-US2-BE1.md): Create visa application record with submission date and reference fields.
- [ ] [VIS-EP1-US2-BE2](../tasks/VIS-EP1-US2-BE2.md): Enforce document completeness and visa payment clearance before submission.
- [ ] [VIS-EP1-US2-BE3](../tasks/VIS-EP1-US2-BE3.md): Add integration tests for visa submission gates.

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
