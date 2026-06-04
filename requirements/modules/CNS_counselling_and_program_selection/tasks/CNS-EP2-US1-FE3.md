# CNS-EP2-US1-FE3: Add tests for saving inputs without creating a file.
## Detailed Frontend Task Plan

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `CNS` - Counselling and Program Selection |
| EPIC | [CNS-EP2: Student Fit and Proceed Decision](../epics/CNS-EP2_student_fit_and_proceed_decision.md) |
| User Story | [CNS-EP2-US1: Capture Counselling Inputs](../stories/CNS-EP2-US1_capture_counselling_inputs.md) |
| Task Type | `FE` |

## Business Context

As a Consultant, I want to capture student preferences and background during counselling so that the selected program is based on clear inputs.

This task supports the module goal: Help consultants search programs, compare package costs, check student fit, and start file opening only when a selected program has an active package.

## Source Documents

- [Counselling and Program Selection Flow](../../../../business/flows/02_counselling_and_program_selection_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [Counselling Program Selection Design](../../../../design-guide/06-counselling-program-selection.html)

## Acceptance Criteria Impact

- [ ] Inputs include academic background, target country, budget, intake interest, and notes.
- [ ] Inputs can be used before a formal file is opened.
- [ ] No permanent file is created until the consultant confirms the proceed decision.

## Business Rules To Preserve

- Consultants cannot edit catalog records.
- File opening requires active package.
- Counselling can exist before formal file creation.

## Dependencies To Check First

- Depends on CAT active catalog and active package lookup.

## Implementation Plan

1. Locate or create the Consultant File Workspace route or workspace section that owns this behavior.
2. Create typed UI models for the data needed by the story; keep field names aligned with the backend DTO/API contract.
3. Build the screen, panel, form, table, queue, or state component described by the task with loading, empty, success, and error states.
4. Apply role-aware behavior using authenticated user role and backend permission response; do not rely on visual hiding for security decisions.
5. Connect mutation actions to API calls only after backend contract exists; otherwise document the missing contract as a blocker.
6. Add user-visible validation for required fields, invalid transitions, duplicate warnings, and blocked workflow states mentioned by acceptance criteria.
7. Add frontend coverage for the happy path and at least one blocked/error path. Prefer Playwright for full role flows and component tests only for risky reusable pieces.
8. Write tests that assert the visible business outcome, not only that components render.

## UI and Contract Expectations

- Frontend workspace: `Consultant File Workspace`.
- Use Next.js, TypeScript, Tailwind CSS, and React Query patterns when implementation begins.
- Prefer API-driven permissions and response fields over hardcoded role assumptions.
- Required states: loading, empty, successful data, validation error, authorization-restricted, and server error.
- Design reference: `../../../../design-guide/06-counselling-program-selection.html`.

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
Module: CNS
Story: CNS-EP2-US1
Completed task: CNS-EP2-US1-FE3
Files changed:
Tests run:
Tracker updated:
Open blockers:
Next recommended task:
```
