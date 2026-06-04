# VIS-EP2-US1: Record Visa Outcome
## Detailed User Story

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `VIS` - Visa Processing |
| EPIC | [VIS-EP2: Visa Outcome and File Completion](../epics/VIS-EP2_visa_outcome_and_file_completion.md) |

## Story Statement

As a Visa user, I want to record the visa outcome so that the file reflects the real application result.

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

- [ ] Outcome can be approved or rejected.
- [ ] Approved outcome records issue date and expiry date when available.
- [ ] Rejected outcome records rejection reason and does not delete previous records.

## Business Rules

- Visa approval/completion requires documents and payment clearance.
- Visa rejection preserves history.
- Visa users cannot see commission data.

## Dependencies and Preconditions

- Depends on ADM approval, offer letter, and PAY clearance.

## Frontend Tasks

- [ ] [VIS-EP2-US1-FE1](../tasks/VIS-EP2-US1-FE1.md): Build visa outcome form with approved and rejected branches.
- [ ] [VIS-EP2-US1-FE2](../tasks/VIS-EP2-US1-FE2.md): Show rejection reason and reapplication decision placeholder for Owner review.
- [ ] [VIS-EP2-US1-FE3](../tasks/VIS-EP2-US1-FE3.md): Add tests for approved and rejected outcome states.

## Backend Tasks

- [ ] [VIS-EP2-US1-BE1](../tasks/VIS-EP2-US1-BE1.md): Implement visa outcome API with approved/rejected fields and validation.
- [ ] [VIS-EP2-US1-BE2](../tasks/VIS-EP2-US1-BE2.md): Add status transition to `Visa Approved` or `Visa Rejected` with audit log and notification.
- [ ] [VIS-EP2-US1-BE3](../tasks/VIS-EP2-US1-BE3.md): Add tests for outcome validation, rejection history, and notification creation.

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
