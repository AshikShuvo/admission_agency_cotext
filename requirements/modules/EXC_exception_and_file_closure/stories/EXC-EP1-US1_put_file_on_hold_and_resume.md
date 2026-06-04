# EXC-EP1-US1: Put File On Hold and Resume
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

As an authorized staff user, I want to place a file on hold and resume it later so that temporary business blockers are tracked without losing progress.

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

- [ ] On-hold action records reason, actor, and timestamp.
- [ ] Existing payments, documents, and activity history remain unchanged.
- [ ] Resume action restores the file to the appropriate previous active stage.

## Business Rules

- Files are not deleted.
- Cancelled and completed files are locked from normal edits.
- Visa reapplication preserves previous history.

## Dependencies and Preconditions

- Depends on FIL status model, VIS rejection, and COM completion eligibility.

## Frontend Tasks

- [ ] [EXC-EP1-US1-FE1](../tasks/EXC-EP1-US1-FE1.md): Build on-hold action and reason form in file detail.
- [ ] [EXC-EP1-US1-FE2](../tasks/EXC-EP1-US1-FE2.md): Show on-hold banner, reason, and resume action where authorized.
- [ ] [EXC-EP1-US1-FE3](../tasks/EXC-EP1-US1-FE3.md): Add tests for hold, hold banner, and resume states.

## Backend Tasks

- [ ] [EXC-EP1-US1-BE1](../tasks/EXC-EP1-US1-BE1.md): Implement hold status transition with reason and previous-stage metadata.
- [ ] [EXC-EP1-US1-BE2](../tasks/EXC-EP1-US1-BE2.md): Implement resume transition with authorization and audit log.
- [ ] [EXC-EP1-US1-BE3](../tasks/EXC-EP1-US1-BE3.md): Add tests for hold/resume history preservation.

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
