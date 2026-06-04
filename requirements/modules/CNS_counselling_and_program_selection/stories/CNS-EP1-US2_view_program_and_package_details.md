# CNS-EP1-US2: View Program and Package Details
## Detailed User Story

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `CNS` - Counselling and Program Selection |
| EPIC | [CNS-EP1: Program Discovery for Counselling](../epics/CNS-EP1_program_discovery_for_counselling.md) |

## Story Statement

As a Consultant, I want to view program and package details so that I can explain the full cost and process to the student.

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

- [ ] Program details include university, duration, intake, and entry requirement notes.
- [ ] Package summary shows stage-wise fee line items and totals.
- [ ] Commission defaults are never visible to consultants.

## Business Rules

- Consultants cannot edit catalog records.
- File opening requires active package.
- Counselling can exist before formal file creation.

## Dependencies and Preconditions

- Depends on CAT active catalog and active package lookup.

## Frontend Tasks

- [ ] [CNS-EP1-US2-FE1](../tasks/CNS-EP1-US2-FE1.md): Build program detail panel with package cost summary.
- [ ] [CNS-EP1-US2-FE2](../tasks/CNS-EP1-US2-FE2.md): Add stage-wise fee display for File Opening, Admission, and Visa.
- [ ] [CNS-EP1-US2-FE3](../tasks/CNS-EP1-US2-FE3.md): Add tests that consultant package details exclude commission fields.

## Backend Tasks

- [ ] [CNS-EP1-US2-BE1](../tasks/CNS-EP1-US2-BE1.md): Add program detail API with active package summary for counselling.
- [ ] [CNS-EP1-US2-BE2](../tasks/CNS-EP1-US2-BE2.md): Remove owner-only commission data from consultant responses.
- [ ] [CNS-EP1-US2-BE3](../tasks/CNS-EP1-US2-BE3.md): Add tests for package summary calculation and commission hiding.

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
