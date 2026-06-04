# EXC-EP1-US2-FE1: Build cancel action with confirmation and required reason.
## Detailed Frontend Task Plan

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `EXC` - Exception and File Closure |
| EPIC | [EXC-EP1: Hold and Cancellation](../epics/EXC-EP1_hold_and_cancellation.md) |
| User Story | [EXC-EP1-US2: Cancel File Without Deletion](../stories/EXC-EP1-US2_cancel_file_without_deletion.md) |
| Task Type | `FE` |

## Business Context

As an Owner or authorized user, I want to cancel a file without deleting it so that business records stay auditable.

This task supports the module goal: Handle files that pause, cancel, complete, or receive visa rejection without deleting business history, payments, documents, or audit records.

## Source Documents

- [Exception and File Closure Flow](../../../../business/flows/11_exception_and_file_closure_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [Exception Closure Workbench Design](../../../../design-guide/18-exception-closure-workbench.html)
- [Locked File State Design](../../../../design-guide/20-locked-file-state.html)

## Acceptance Criteria Impact

- [ ] Cancellation records reason, actor, and timestamp.
- [ ] Cancelled files are locked from normal edits.
- [ ] File deletion is not available as a normal business action.

## Business Rules To Preserve

- Files are not deleted.
- Cancelled and completed files are locked from normal edits.
- Visa reapplication preserves previous history.

## Dependencies To Check First

- Depends on FIL status model, VIS rejection, and COM completion eligibility.

## Implementation Plan

1. Locate or create the File Detail Workspaces route or workspace section that owns this behavior.
2. Create typed UI models for the data needed by the story; keep field names aligned with the backend DTO/API contract.
3. Build the screen, panel, form, table, queue, or state component described by the task with loading, empty, success, and error states.
4. Apply role-aware behavior using authenticated user role and backend permission response; do not rely on visual hiding for security decisions.
5. Connect mutation actions to API calls only after backend contract exists; otherwise document the missing contract as a blocker.
6. Add user-visible validation for required fields, invalid transitions, duplicate warnings, and blocked workflow states mentioned by acceptance criteria.
7. Add frontend coverage for the happy path and at least one blocked/error path. Prefer Playwright for full role flows and component tests only for risky reusable pieces.

## UI and Contract Expectations

- Frontend workspace: `File Detail Workspaces`.
- Use Next.js, TypeScript, Tailwind CSS, and React Query patterns when implementation begins.
- Prefer API-driven permissions and response fields over hardcoded role assumptions.
- Required states: loading, empty, successful data, validation error, authorization-restricted, and server error.
- Design reference: `../../../../design-guide/18-exception-closure-workbench.html and ../../../../design-guide/20-locked-file-state.html`.

## Data, State, and Error Handling

- Identify all required fields from the story acceptance criteria before implementation.
- Keep IDs stable and use backend-generated identifiers for persisted records.
- Handle not found, forbidden, validation error, duplicate/conflict, and workflow-blocked responses.
- Preserve historical records when the business flow says data must not be deleted or overwritten.
- Do not expose restricted fields in UI state, API responses, logs, or test fixtures.

## Test Plan

- [ ] Add or update automated tests for the normal successful path.
- [ ] Add or update tests for at least one blocked or invalid path.
- [ ] Add role/access tests when task touches restricted data or actions.
- [ ] Confirm test data includes the minimum business objects needed for this story.
- [ ] Record the test command in the agent handoff note.

## Definition of Done

- [ ] Implementation matches this task plan and the linked story acceptance criteria.
- [ ] Required UI/API/service behavior is implemented in the correct module boundary.
- [ ] Authorization and data visibility are enforced where applicable.
- [ ] Tests are added or an explicit test gap is recorded as a blocker.
- [ ] This task checkbox is marked complete in the story file and source module summary.
- [ ] [Progress Tracker](../../../progress_tracker.md) is updated with the completed task count.

## Handoff Note Template

```text
Module: EXC
Story: EXC-EP1-US2
Completed task: EXC-EP1-US2-FE1
Files changed:
Tests run:
Tracker updated:
Open blockers:
Next recommended task:
```
