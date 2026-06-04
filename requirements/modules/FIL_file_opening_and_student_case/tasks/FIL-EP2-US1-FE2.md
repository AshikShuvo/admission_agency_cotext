# FIL-EP2-US1-FE2: Show file-specific stage fee totals in file detail.
## Detailed Frontend Task Plan

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `FIL` - File Opening and Student Case |
| EPIC | [FIL-EP2: Package Snapshot and File Detail](../epics/FIL-EP2_package_snapshot_and_file_detail.md) |
| User Story | [FIL-EP2-US1: Snapshot Package Fees](../stories/FIL-EP2-US1_snapshot_package_fees.md) |
| Task Type | `FE` |

## Business Context

As a Consultant, I want selected package fees copied into the file so that future fee changes do not change existing student agreements.

This task supports the module goal: Create the central student file, copy the selected package fees into immutable file fee records, assign the consultant, and prepare the file for payment confirmation and admission processing.

## Source Documents

- [File Opening Flow](../../../../business/flows/03_file_opening_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [File Opening Design](../../../../design-guide/07-file-opening.html)
- [Student File Detail Design](../../../../design-guide/08-student-file-detail.html)

## Acceptance Criteria Impact

- [ ] File fee records are created from the active package at file creation time.
- [ ] Stage totals are visible for File Opening, Admission, and Visa.
- [ ] Later package edits do not change the file fee snapshot.

## Business Rules To Preserve

- Consultants only manage assigned files.
- File numbers are unique.
- Package fees are copied at creation time.
- File history is preserved.

## Dependencies To Check First

- Depends on CAT active package and CNS selected program context.

## Implementation Plan

1. Locate or create the Consultant File Workspace route or workspace section that owns this behavior.
2. Create typed UI models for the data needed by the story; keep field names aligned with the backend DTO/API contract.
3. Build the screen, panel, form, table, queue, or state component described by the task with loading, empty, success, and error states.
4. Apply role-aware behavior using authenticated user role and backend permission response; do not rely on visual hiding for security decisions.
5. Connect mutation actions to API calls only after backend contract exists; otherwise document the missing contract as a blocker.
6. Add user-visible validation for required fields, invalid transitions, duplicate warnings, and blocked workflow states mentioned by acceptance criteria.
7. Add frontend coverage for the happy path and at least one blocked/error path. Prefer Playwright for full role flows and component tests only for risky reusable pieces.

## UI and Contract Expectations

- Frontend workspace: `Consultant File Workspace`.
- Use Next.js, TypeScript, Tailwind CSS, and React Query patterns when implementation begins.
- Prefer API-driven permissions and response fields over hardcoded role assumptions.
- Required states: loading, empty, successful data, validation error, authorization-restricted, and server error.
- Design reference: `../../../../design-guide/07-file-opening.html and ../../../../design-guide/08-student-file-detail.html`.

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
Module: FIL
Story: FIL-EP2-US1
Completed task: FIL-EP2-US1-FE2
Files changed:
Tests run:
Tracker updated:
Open blockers:
Next recommended task:
```
