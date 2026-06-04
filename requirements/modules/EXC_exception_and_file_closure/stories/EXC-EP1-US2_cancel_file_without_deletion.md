# EXC-EP1-US2: Cancel File Without Deletion
## Detailed User Story

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `EXC` - Exception and File Closure |
| EPIC | [EXC-EP1: Hold and Cancellation](../epics/EXC-EP1_hold_and_cancellation.md) |

## Story Statement

As an Owner or authorized user, I want to cancel a file without deleting it so that business records stay auditable.

## Business Expectation

This story must convert the business expectation into a working system behavior that staff can use without relying on manual spreadsheets, side notes, or hidden process knowledge. The implementation must preserve the role boundaries, lifecycle rules, and data ownership described in the source business flow.

## Primary Actors

- Owner
- Consultant
- Admission
- Visa
- Accounts, financial visibility only

## Source Documents

- [Exception and File Closure Flow](../../../../business/flows/11_exception_and_file_closure_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [Exception Closure Workbench Design](../../../../design-guide/18-exception-closure-workbench.html)
- [Locked File State Design](../../../../design-guide/20-locked-file-state.html)

## Acceptance Criteria

- [ ] Cancellation records reason, actor, and timestamp.
- [ ] Cancelled files are locked from normal edits.
- [ ] File deletion is not available as a normal business action.

## Business Rules

- Files are not deleted.
- Cancelled and completed files are locked from normal edits.
- Visa reapplication preserves previous history.

## Dependencies and Preconditions

- Depends on FIL status model, VIS rejection, and COM completion eligibility.

## Frontend Tasks

- [ ] [EXC-EP1-US2-FE1](../tasks/EXC-EP1-US2-FE1.md): Build cancel action with confirmation and required reason.
- [ ] [EXC-EP1-US2-FE2](../tasks/EXC-EP1-US2-FE2.md): Show cancelled locked-file state with preserved history.
- [ ] [EXC-EP1-US2-FE3](../tasks/EXC-EP1-US2-FE3.md): Add tests for cancel flow and blocked normal edits.

## Backend Tasks

- [ ] [EXC-EP1-US2-BE1](../tasks/EXC-EP1-US2-BE1.md): Implement cancellation transition with reason and audit log.
- [ ] [EXC-EP1-US2-BE2](../tasks/EXC-EP1-US2-BE2.md): Enforce cancelled-file edit restrictions and no-delete business rule.
- [ ] [EXC-EP1-US2-BE3](../tasks/EXC-EP1-US2-BE3.md): Add tests for cancellation, edit blocking, and record preservation.

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
