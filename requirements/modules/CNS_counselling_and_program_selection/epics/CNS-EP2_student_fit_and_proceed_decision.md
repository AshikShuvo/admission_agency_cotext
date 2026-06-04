# CNS-EP2: Student Fit and Proceed Decision
## Detailed EPIC

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Module Context

| Field | Value |
|---|---|
| Module ID | `CNS` |
| Module | Counselling and Program Selection |
| Frontend Workspace | Consultant File Workspace |
| Backend Module Boundary | Catalog, Students, Files / Cases |

## EPIC Goal

Deliver this capability area as a coherent business workflow, not as isolated screens or endpoints. The EPIC is complete only when every linked user story is accepted, tested, and reflected in the progress tracker.

## Functional Scope

- Consultant can record temporary counselling inputs for student fit.
- Consultant can mark a selected program as ready for file opening.
- System blocks file opening if the selected program has no active package.

## Business Rules To Preserve

- Consultants cannot edit catalog records.
- File opening requires active package.
- Counselling can exist before formal file creation.

## Dependencies

- Depends on CAT active catalog and active package lookup.

## User Stories

- [ ] [CNS-EP2-US1: Capture Counselling Inputs](../stories/CNS-EP2-US1_capture_counselling_inputs.md)
- [ ] [CNS-EP2-US2: Start File Opening from Selected Program](../stories/CNS-EP2-US2_start_file_opening_from_selected_program.md)

## Implementation Expectations

- Frontend and backend agents should work story by story.
- Backend contracts should be stabilized before frontend final integration.
- Access control must be implemented in backend services and query scopes, not only by hiding UI elements.
- Task completion must be reflected in task files, story files, this EPIC file, and [Progress Tracker](../../../progress_tracker.md).

## EPIC Acceptance Criteria

- [ ] All linked user stories are complete.
- [ ] All frontend and backend tasks under those stories are complete.
- [ ] Automated tests cover the highest-risk workflow rules in this EPIC.
- [ ] Role access and sensitive-data behavior are verified.
- [ ] No open blocker remains for this EPIC.
- [ ] EPIC completion is recorded in [Progress Tracker](../../../progress_tracker.md).
