# CNS-EP2-US2: Start File Opening from Selected Program
## Detailed User Story

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `CNS` - Counselling and Program Selection |
| EPIC | [CNS-EP2: Student Fit and Proceed Decision](../epics/CNS-EP2_student_fit_and_proceed_decision.md) |

## Story Statement

As a Consultant, I want to start file opening from the selected program so that the file uses the correct active package.

## Business Expectation

This story must convert the business expectation into a working system behavior that staff can use without relying on manual spreadsheets, side notes, or hidden process knowledge. The implementation must preserve the role boundaries, lifecycle rules, and data ownership described in the source business flow.

## Primary Actors

- Consultant
- Student
- Owner, oversight

## Source Documents

- [Counselling and Program Selection Flow](../../../../business/flows/02_counselling_and_program_selection_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [Counselling Program Selection Design](../../../../design-guide/06-counselling-program-selection.html)

## Acceptance Criteria

- [ ] Proceed action is enabled only when the program has an active package.
- [ ] Selected program, university, and package are carried into file opening.
- [ ] Consultant sees a clear warning when Owner configuration is missing.

## Business Rules

- Consultants cannot edit catalog records.
- File opening requires active package.
- Counselling can exist before formal file creation.

## Dependencies and Preconditions

- Depends on CAT active catalog and active package lookup.

## Frontend Tasks

- [ ] [CNS-EP2-US2-FE1](../tasks/CNS-EP2-US2-FE1.md): Add proceed-to-file-opening action from program detail.
- [ ] [CNS-EP2-US2-FE2](../tasks/CNS-EP2-US2-FE2.md): Pre-fill file opening context with selected country, university, program, and package.
- [ ] [CNS-EP2-US2-FE3](../tasks/CNS-EP2-US2-FE3.md): Add tests for enabled and blocked proceed states.

## Backend Tasks

- [ ] [CNS-EP2-US2-BE1](../tasks/CNS-EP2-US2-BE1.md): Add selected-program validation endpoint for file-opening eligibility.
- [ ] [CNS-EP2-US2-BE2](../tasks/CNS-EP2-US2-BE2.md): Return active package snapshot preview for the file opening flow.
- [ ] [CNS-EP2-US2-BE3](../tasks/CNS-EP2-US2-BE3.md): Add tests for missing active package and inactive program blocking.

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
